# 言語処理学会 第27回年次大会 発表資料

## スクリプト情報
| 名前            | リンク | 備考 |
|----------------|-------|-----|
| けやきツリーバンク  | [kmineshima/Keyaki, master@66285c1](https://github.com/kmineshima/Keyaki/commit/66285c1339363234886231c2e77d7560e318c46a) | 復号済み，非公開 |
| ABCT-toolkit   | [ABCTreebank/ABCT-toolkit, mod/NLP27@7af8848](https://github.com/ABCTreebank/ABCT-toolkit/commit/7af884819bcd784c59aaacb5cc74c245b2002851)  | |
| ccg2lambda     | [kmineshima/ABCTreebank, master@e891828](https://github.com/kmineshima/abctreebank/commit/e8918282f1e8a94160fb7ee60873bd5bc40cf6e1) | 未公開，スクリプトは`ccg2lambda`フォルダにある |

## 説明
| ファイル名               | 説明                              |
|-----------------------|----------------------------------|
| `README.md`           | 本ファイル．                        |
| `gold.txt`            | ABCパーサの評価のために選ばれたKeyaki文（GOLD文）が行ごとに並んでいる．先頭はID，その後に文が続く．スペース区切り．`*pro*`などの空範疇は削除されている． |
| `gold_parsed.psd.txt` | GOLD文を，ABCパーサで解析したもの．     |

## 手順
### シェル変数
| 変数名                  | 説明                              |
|-----------------------|----------------------------------|
| `${KEYAKI}`           | けやきツリーバンクのパス               |
| `${ABCTB}`            | 変換して得られるABC Treebankのパス     |
| `${ABCTB_ML_PREP}`    | パーサの訓練のための下準備（下記参照）における，生成されたデータの出力フォルダ |
| `${ABCTB_ML}`         | パーサの訓練の結果生成される，モデルとパーサ設定が入っているフォルダ |
| `${ABCT-toolkit}`     | ABCT-toolkitのパス                 |

### 前準備
ABCT-toolkitのために必要な環境があらかじめ整っているものとする．
```sh
cd ${ABCT-toolkit}
poetry env use python3.6
```

### けやきツリーバンクからABC Treebankへの変換
```sh 
cd ${ABCT-toolkit}
ls -d ${KEYAKI}/*.psd | poetry run abctk conv --source filelist --destination ${ABCTB}
```

補足：

- GOLDとして選ばれている木は，パーサの訓練において取り除かれていなければならないので，
    パイプラインの中の `${ABCT-toolkit}/abctk/ext_scripts/simplify-tag.sed` において生成されないようにした．
- パーサの訓練において不適格である，子が3つ以上あるような部分木は，
    （変換のコアである）CCG範疇作成のプログラム `${ABCT-toolkit}/ext_src/abc-hs` の一部を改変することで，
    排除してある．
- パーサの訓練において不要である，
    変換時情報（`#role=a`などの文法役割，`#deriv=unary`などの特殊な派生のマーキング）や，
    木のID（例：`(ID textbook_particles_xxx）`）は，
    同上のプログラムを一部改変することで，出力されないようにしている．
- 空範疇である語彙項目（例： `... (X (Y *pro*) (Y\X ...)) ...` は，
    パーサの訓練の前に削除する（`... (X#unary）必要があるが，失念した．
    このため，パーサの訓練の前準備の段階で，[depccg](https://github.com/masashi-y/depccg/blob/9d375edf9b74e22f8d7dcdf78dab5fcbad170e85/depccg/tools/ja/keyaki_reader.py#L192)
    によって，少なくない木が，不必要にまるごと捨てられてしまった．

### ABCパーサの訓練
#### 追加パッケージのインストール
パーサの訓練でGPUを使用をするが，そのためにはドライバーをインストールする必要がある．
2021年1月時点では，次のQiita記事が参考になる．

- [NVIDIA Docker って今どうなってるの？ (19.11版)](https://qiita.com/ksasaki/items/b20a785e1a0f610efa08)
- [Ubuntu 20.04へのCUDAインストール方法](https://qiita.com/yukoba/items/c4a45435c6ee5d66706d)

`$PATH`にcuda関連のものをあらかじめ入れないと，pycudaの（pipなどを通しての）インストールが上手くいかない．
```sh
export PATH=/usr/local/cuda/bin:${PATH}
```

パーサの訓練に関連するPythonパッケージを追加する．
```sh
cd ${abctk}
poetry install --extras "ml"
```

#### 訓練
パーサの訓練の下準備をし，データを準備する．
```sh
cd ${abctk}
cat ${ABCTB}/*.psd \
    | sed -e '/^\s*$/d' \
    | poetry run abctk ml prepare --destination ${ABCTK_ML_PREP}
```
注：上の変換プログラムにおいて，不必要な空行が木と木の間に入ってしまっており，（上のsedの行で）削除しなければ不具合が生じる．

訓練をする．`nohup ... &` 構文を用いると，バックグラウンドで学習が始まり，
（HUPシグナルの無視によって）シェルから退出しても学習が続けられる．
```sh
nohup poetry run abctk ml train ${ABCTK_ML_PREP} --destination ${ABCTB_ML} &
```

### ABCパーサの評価1：（正解であるところの）ABC TreebankのGOLD木の意味表示の生成

### ABCパーサの評価2：（正解であるところの）ABC TreebankのGOLD文の再解析
- IDの消去と補い
- NPq -> NP, Ns -> N
- Question: extract_by_genre.pyで，非ランダム抽出はどのようにしてできたのか？

### ABCパーザの評価3：再解析によって得られたGOLD木の意味表示の生成と，正解との比較

### 統計情報

文についての情報


```sh
# 意味割り当ての全件数
cat semantics_abc.yaml | grep 'category' | grep -v "child" | grep -v "#" | wc -l
176

# unary規則に対する割り当ての数
cat semantics_abc.yaml | grep 'unary' | grep -v "#" | wc -l
46

# base (lemma)に対する割り当ての数
cat semantics_abc.yaml | grep 'base' | grep -v "#" | wc -l
22

# pos に対する割り当ての数
cat semantics_abc.yaml | grep 'pos' | grep -v "#" | grep -v "semantics" | wc -l
43

# 単語に対する割り当ての数
# 22 + 46 = 68
# カテゴリに対する割り当ての数
# 176 - (46 + 68) = 62
```
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
| `${abctk}`            | ABCT-toolkitのパス                 |

### 前準備
ABCT-toolkitのために必要な環境があらかじめ整っているものとする．
```sh
cd ${ABCT}
poetry env use python3.6
```

### けやきツリーバンクからABC Treebankへの変換
```sh 
cd ${ABCT}
ls -d ${KEYAKI}/*.psd | poetry run abctk conv --source filelist --destination ${ABCTB}
```
なお：GOLDとなっている木と，二分木になっていないために不適格である木は，
ABCT-toolkitの，今回のために特別に修正されたバージョンによって，この段階で既に排除されている．

### ABCパーサの訓練
- extra packageのインストール
- proを消す
- IDを消す
- 訓練セットの準備
- 訓練

### ABCパーサの評価1：（正解であるところの）ABC TreebankのGOLD木の意味表示の生成

### ABCパーサの評価2：（正解であるところの）ABC TreebankのGOLD文の再解析
- IDの消去と補い
- NPq -> NP, Ns -> N
- Question: extract_by_genre.pyで，非ランダム抽出はどのようにしてできたのか？

### ABCパーザの評価3：再解析によって得られたGOLD木の意味表示の生成と，正解との比較

### 統計情報

文についての情報


```
意味割り当ての全件数
$ cat semantics_abc.yaml | grep 'category' | grep -v "child" | grep -v "#" | wc -l
176
unary規則に対する割り当ての数
$ cat semantics_abc.yaml | grep 'unary' | grep -v "#" | wc -l
46
base (lemma)に対する割り当ての数
$ cat semantics_abc.yaml | grep 'base' | grep -v "#" | wc -l
22
pos に対する割り当ての数
$ cat semantics_abc.yaml | grep 'pos' | grep -v "#" | grep -v "semantics" | wc -l
43
単語に対する割り当ての数
22 + 46 = 68
カテゴリに対する割り当ての数
176 - (46 + 68) = 62
```
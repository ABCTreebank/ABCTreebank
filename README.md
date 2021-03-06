# ABCツリーバンク

## 概要
ABCツリーバンクとは、理論言語学と自然言語処理の両分野での研究資源として活用されることを目的とした、
汎用的な範疇文法のツリーバンクです。

## ダウンロード
[リリースページ](https://github.com/ABCTreebank/ABCTreebank/releases)からダウンロードしてください。

## 種類
ABCツリーバンクは、用途に応じて複数の種類のものを用意しております。

- 通常版：等位接続がフラットな構造になっているものです。
- 等位接続二分木化版（binconj）：等位接続構造が二分木に変換されているものです。

## マニュアル
ABCツリーバンクで枠組みとされているABC文法や注目する現象については[マニュアル](https://github.com/kmineshima/abctreebank/wiki/manual)を参照してください。

## ライセンス
明記されている場合を除き、全てのコンテンツは Creative Commons Attribution 4.0 International の下でライセンスされています。

[![CC4](https://licensebuttons.net/l/by/4.0/88x31.png)](https://creativecommons.org/licenses/by/4.0/)

ただし、以下に挙げる有料の言語資源に基づくデータに関しては、
ツリーの終端ノードにある語を見えなくしています。
復元のためにはそれぞれのライセンスが必要です。

- [CD-毎日新聞'95データ集](https://www.nichigai.co.jp/sales/mainichi/mainichi-data.html)
- [日本語話し言葉コーパス（CSJ）](https://pj.ninjal.ac.jp/corpus_center/csj/)
- [現代日本語書き言葉均衡コーパス（BCCWJ）](https://pj.ninjal.ac.jp/corpus_center/bccwj/)
- [同時通訳データベース（SIDB）](http://sidb.jp/)


## ツール類
- [変換スクリプト](https://github.com/ABCTreebank/ABCT-toolkit)
    - ABCツリーバンクは[けやきツリーバンク](http://www.compling.jp/keyaki/)(Butler et al. 2018)からの変換によって構築されました。その際に用いられたスクリプトです。
- 復元スクリプト
    - 有料の言語資源由来のデータを復元するためのスクリプトです。

## 参考文献

- Alastair Butler, Kei Yoshimoto, Shota Hiyama, Stephen Wright Horn, Iku Nagasaki, and Ai Kubota. 2018. The Keyaki Treebank Parsed Corpus, Version 1.1 (http://www.compling.jp/keyaki/ accessed 2021/03/31)
- Yusuke Kubota, Koji Mineshima, Noritsugu Hayashi, and Shinya Okano. Development of a general-purpose categorial grammar treebank. In Proceedings of the 12th Language Resources and Evaluation Conference, pp. 5195–5201, 2020.
- 窪田悠介, 峯島宏次, 林則序, 岡野伸哉. 汎用的な範疇文法ツリーバンクの構築. 言語処理学会第25回年次大会発表論文集, pp. 143–146, 2019.
- 窪田悠介, 峯島宏次, 林則序, 岡野伸哉. ABCツリーバンク：学際的な言語研究のための基盤資源. 言語処理学会第27回年次大会発表論文集, 2021.

## 履歴
- 2021/03/XX version 1.0のリリース
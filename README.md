# ABCツリーバンク

## 概要/About
ABCツリーバンクとは、理論言語学と自然言語処理の両分野での研究資源として活用されることを目的とした、
汎用的な範疇文法の日本語ツリーバンクです。

ABC Treebank is a general-purpose categorial grammar treebank for Japanese,
which is intended to be used as a research resource in both theoretical lingistics and natural language processing.


## ダウンロード/Download
[リリースページ](https://github.com/ABCTreebank/ABCTreebank/releases)からダウンロードしてください。

You can download the treebank from [the release page](https://github.com/ABCTreebank/ABCTreebank/releases).

## 種類/Editions
ABCツリーバンクは、用途に応じて複数の種類のものを用意しています。

- 通常版：等位接続がフラットな構造になっているものです。
- 等位接続二分木化版（binconj）：等位接続構造が二分木に変換されているものです。

We offer several types of ABC Treebank for different purposes.

- The standard edition: Conjunction structures are flatly annotated.
- The binarized edition (binconj): Conjunction structures are binarized.

## マニュアル/Manual
ABCツリーバンクで枠組みとされているABC文法や注目する現象については[マニュアル](https://github.com/kmineshima/abctreebank/wiki/manual)を参照してください。

See [the manual](https://github.com/kmineshima/abctreebank/wiki/manualfor) for an overview of ABC Grammar as the framework of ABC Treebank
as well as the phenomena it focuses on.

## ライセンス/Licenses
明記されている場合を除き、全てのコンテンツは Creative Commons Attribution 4.0 International の下でライセンスされています。

Unless otherwise noted, all content is licensed under Creative Commons Attribution 4.0 International.

[![CC4](https://licensebuttons.net/l/by/4.0/88x31.png)](https://creativecommons.org/licenses/by/4.0/)

ただし、以下に挙げる有料の言語資源に基づくデータに関しては、
ツリーの終端ノードにある語を見えなくしています。
復元のためにはそれぞれのライセンスが必要です。

However, for data based on the following purchasable language resources,
the words at the end nodes of the trees are invisiblized.
A license is required to restore words for each of the resources.

- [CD-毎日新聞'95データ集/Mainichi Shinbun 1995 CD-ROM data collection](https://www.nichigai.co.jp/sales/mainichi/mainichi-data.html)
- [日本語話し言葉コーパス/Corpus of Spontaneous Japanese (CSJ)](https://pj.ninjal.ac.jp/corpus_center/csj/)
- [現代日本語書き言葉均衡コーパス/Balanced Corpus of Contemporary Written Japanese (BCCWJ)](https://pj.ninjal.ac.jp/corpus_center/bccwj/)
- [同時通訳データベース/Simultaneous Interpretation Database (SIDB)](http://sidb.jp/)


## ツール類/Tools
- [変換スクリプト](https://github.com/ABCTreebank/ABCT-toolkit)
    - ABCツリーバンクは[けやきツリーバンク](http://www.compling.jp/keyaki/)(Butler et al. 2018)からの変換によって構築されました。その際に用いられたスクリプトです。
- 復元スクリプト
    - ライセンスがある場合に、有料の言語資源由来のデータを復元するためのスクリプトです。

- [Scripts for conversion](https://github.com/ABCTreebank/ABCT-toolkit)
    - ABC Treebank was obtained through conversion from [Keyaki Treebank](http://www.compling.jp/keyaki/)(Butler et al. 2018). These are the scripts used.
- Script for restoration
    - This is the script to restore words in data from purchasable language resources when you have a license.


## 参考文献/References

- Alastair Butler, Kei Yoshimoto, Shota Hiyama, Stephen Wright Horn, Iku Nagasaki, and Ai Kubota. 2018. The Keyaki Treebank Parsed Corpus, Version 1.1 (http://www.compling.jp/keyaki/ accessed 2021/03/31)
- Yusuke Kubota, Koji Mineshima, Noritsugu Hayashi, and Shinya Okano. Development of a general-purpose categorial grammar treebank. In Proceedings of the 12th Language Resources and Evaluation Conference, pp. 5195–5201, 2020.
- 窪田悠介, 峯島宏次, 林則序, 岡野伸哉. 汎用的な範疇文法ツリーバンクの構築. 言語処理学会第25回年次大会発表論文集, pp. 143–146, 2019.
- 窪田悠介, 峯島宏次, 林則序, 岡野伸哉. ABCツリーバンク：学際的な言語研究のための基盤資源. 言語処理学会第27回年次大会発表論文集, 2021.

## 謝辞/Acknowledgement
吉川将司氏(東北大)のサポートに感謝します。この研究は JSPS 科研費 18K00523, 15H210および国立国語研究所共同研究プロジェクト「対照言語学的観点か
ら見た日本語の音声と文法」の助成を受けています。


Our appreciation goes to Masashi Yoshikawa (Tohoku University) for his help and constructive suggestions. This work is supported by JSPS KAKENHI GRANTs 18K00523 and 15H03210, and the NINJAL collaborative research project ‘Cross-linguistic Studies of Japanese Prosody and Grammar’.

## 履歴/History
- 2021/03/XX version 1.0のリリース
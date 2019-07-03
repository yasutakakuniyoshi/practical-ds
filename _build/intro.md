---
title: 'Home'
prev_page:
  url: 
  title: ''
next_page:
  url: /https://github.com/uribo/practical-ds
  title: 'GitHub repository'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---
# 実践的データサイエンス

<img src="https://circleci.com/gh/jupyter/jupyter-book.svg?style=svg" class="left">

## はじめに

データ分析のためにコンピュータを利用する際、RおよびPython言語のいずれかを使うことが多いと思います(Julia言語は高レベル・高パフォーマンスな技術計算のための言語で今後期待が膨らみます）。これらの2つの言語では、データ操作や可視化、データ分析、モデリングに使われるライブラリが豊富にあり、
どれを使うのが良いのか迷うような状況が続いていました。しかしその状態は落ち着きを見せ、成熟期を迎えつつあります。

R言語ではパイプ演算子の登場によりデータフレームに対する操作に大きな変化が生じ、tidyverseによるデータ読み込みからデータ整形、可視化までが可能になりました。またtidyverseのような、機械や人間の双方が扱いやすいパッケージが増えてきました。特にR言語の強力な一面でもあったデータ分析の操作はtidymodelsに代表されるパッケージがユーザの操作性を改善し、より統一されたコードで処理を記述できるようになりつつあります。

Python言語ではデータフレームの操作にはpandasが欠かせないものとなっています。またscikit-learnは、データ分析や機械学習モデルの実行に必要な多くの関数を提供しています。これらのライブラリを抜きにしてデータ操作を行うのは考えにくい状況です。

RとPython、これらの違いは何でしょうか。データサイエンティストが扱う2つの言語は競争関係にあると言えますが、それは互いの言語を発展させるのに大いに役立っています。今やtidyverseのコアパッケージであるdplyrやggplot2がPythonに移植され、R言語からはPythonの強力なツールを利用するためのインターフェースが開発されています。2つの言語は排他的なものではなく、相互に補える関係にあると言えます。データ分析に必要な処理の多くはどちらのコアツールでも利用可能になっているのが現状でしょう。また、どちらかの言語で登場した優れたライブラリは、何らかの方法ですぐに取り入れられるでしょう。2つの言語を習得することは困難ではありますが、他方の言語での処理を知ることで多くのことが学べます。

このプロジェクトの目的は、データ分析に必要な操作・処理をRおよびPython双方で示すことを目指します。特に統計、機械学習モデルを扱う上で欠かせない特徴量エンジニアリングの処理を重点的に扱い、いずれの言語でも満足のいく形で分析を行えるようになることを目的とします。

## 目次

- [データ分析の流れ](01/readme)
    - [データ分析のプロセス](01/introduction)
    - [探索的データ分析](01/eda)
    - [tidyデータと前処理](01/tidy_data)
    - [モデルの構築から評価まで](01/tidymodels_workflow)
- [特徴量エンジニアリング](02/readme)
    - [数値データの取り扱い](02/numeric)
    - [カテゴリデータの取り扱い](02/categorical)
    - [テキストデータの取り扱い](02/text)
    - [日付・時間データの取り扱い](02/date-and-time)
    - [地理空間データの取り扱い(02/spatial-data)
- [より良いモデルを目指して](03/readme)
  - [欠損値の処理](03/handling-missing-data)
  - [次元削減](03/dimension-reduction)
  - [モデルの性能評価](03/model-performance)
  - [データ分割](03/data-splitting)
  - [変数重要度](03/feature-selection)
  - [モデルの解釈](03/interpretability)



### 参考文献

各章の末尾に掲載しています。

## データセットについて

### 地価公示データ (land price)

国土交通省 国土数値情報 （地価公示データ 第2.4版 L01 平成30年度 http://nlftp.mlit.go.jp/ksj/gml/datalist/KsjTmplt-L01-v2_5.html ）を使用し瓜生真也が作成・加工したものです。

うち関東一都六県のデータに対しては、該当する市区町村の夜間人口データを 平成27年度 国勢調査 従業地・通学地による人口・就業状態等集計 より付与しました。

### 土砂災害・雪崩メッシュデータ (hazard)

国土交通省 国土数値情報（土砂災害・雪崩メッシュデータ 第1.1版 A30a5 平成23年度 http://nlftp.mlit.go.jp/ksj/gml/datalist/KsjTmplt-A30a5.html ）を使用し瓜生真也が作成・加工したものです。

このうち九州地方のデータにおいては

各メッシュと対応する標高・傾斜度の情報を

同国土数値情報　標高・傾斜度3次メッシュデータ 第2.2版 G04a 平成21(2009)年度 http://nlftp.mlit.go.jp/ksj/gml/datalist/KsjTmplt-G04-a.html 

より、またメッシュ内に含まれる特殊土壌の情報を

特殊土壌地帯データ 第3.0版 平成28年 http://nlftp.mlit.go.jp/ksj/gml/datalist/KsjTmplt-A23-v3_0.html

より付属させています。

加えて気象庁ホームページ 過去の気象データ・ダウンロード http://www.data.jma.go.jp/gmd/risk/obsdl/index.php より対象地域、対象とする期間 (2016年7月) のデータを関連する気象データとして瓜生真也が加工・作成しました。

### ビールへの支出データ (beer)

総務省 家計調査 家計収支編 二人以上の世帯「1世帯当たり1か月間の日別支出 (表6-16)」の項目から「ビール」に対する支出金額のうち、2018年7月から同年9月 (3ヶ月)の日毎の値、および2015年1月から2018年12月の各月の平均値を利用しています。

また統計データに含まれる日付および月間の気象データを、気象庁ホームページ 過去の気象データ検索 http://www.data.jma.go.jp/obd/stats/etrn/index.php より、観測地点「東京」のデータとして瓜生真也が加工し結合しています。

各データはリポジトリには含まれません。`data-raw/`に含まれるRファイルを実行することでこれらのデータが生成されます。


## プロジェクトの情報

**執筆者**: Uryu Shinya ([\@uribo](https://github.com/uribo), Twitter: [\@u_ribo](http://twitter.com/u_ribo) )

**ライセンス**: BY-SA 4.0

**動作環境**

- [jupyter-book](https://github.com/jupyter/jupyter-book) 0.4.2
- R 3.6.0
- Python 3.7.4
- local (macOS Mojave)
- [Dockerfile](https://github.com/uribo/practical-ds/blob/master/Dockerfile)
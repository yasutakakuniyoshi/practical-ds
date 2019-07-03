---
interact_link: content/03/feature-selection.ipynb
kernel_name: ir
title: '変数重要度'
prev_page:
  url: /03/data-splitting
  title: 'データ分割'
next_page:
  url: /03/interpretability
  title: 'モデルの解釈'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---



{:.input_area}
```R
source(here::here("R/prepared_landprice.R"))
```


# 特徴量選択

<!-- 変数選択ではあっても、モデル選択 ~~とはどういう対応関係?~ ではないかもしれない。
モデルは構築されたもの、モデルで一つ。特徴量選択は個別の特徴量を取り扱う-->

<!-- 半自動的に... 数値による客観的評価。ドメイン知識がなくてOK --> 

モデルの性能評価とともに

モデルに組み込まれた説明変数が目的変数に対してどの程度の影響を持っているのか

* フィルタ法
* ラッパー法
* 組み込み法

<!-- フィルタ法については 01/tidy_data で -->

変数間の相関がもたらす問題は多重共線性と呼ばれます(?)

多重共線性への対策として、事前に共線性をもつ変数を削除しておくというものがあります。

これを変数選択と言います。

一方でモデルに重要な変数を削除してしまう恐れもあります。

> > 余分な変数をモデルに取り組むよりもリスクよりも重要な変数をモデルに取り込まないリスクの方が大きい

変数選択 (feature selection)は慎重に、かつ比較を十分に行うべきでしょう。

次元削減 (feature reduction)

真に必要な変数を探すための作業と言えるかもしれません。

## 高次元データの問題

- 学習に時間がかかる
- 多重共線性
- ノイズや過学習の原因
- 次元の呪い

## 多重共線性

多重共線性の問題は



{:.input_area}
```R
library(car)

vif(lm(prestige ~ income + education, data=Duncan))
vif(lm(prestige ~ income + education + type, data=Duncan))
```


明確な数値指標はありませんが、一般にはVIFが10以上の説明変数をモデルに組み込むと多重共線性が発生する可能性があると言われます。



{:.input_area}
```R
%%python
#Imports
import pandas as pd
import numpy as np
from patsy import dmatrices
import statsmodels.api as sm
from statsmodels.stats.outliers_influence import variance_inflation_factor

df = pd.read_csv('loan.csv')
df.dropna()
df = df._get_numeric_data() #drop non-numeric cols

df.head()
```


膨大な特徴量に

> LASSOやリッジ回帰のような正則化法は、モデル構築プロセスの一部として特徴の寄与を積極的に削除または割り引くことを積極的に求めているため、特徴量選択を組み込んだアルゴリズムと見なすこともできます。

計算コストを考慮して

1. 単変量特徴量選択... フィルタ法とも呼びます。 `tidy_data` で解説。前処理の段階で使用する変数を制限する
2. 反復特徴量選択... ラッパー法 (wrapper method)
3. モデルベース特徴量選択... 組み込み法 (emedded method)

## 反復特徴量選択

- 前向き法 (Forward stepwise selection)... 
- 後向き法 (Backward stepwise selection)... 関心のある特徴量を含めたモデルを構築。モデルに影響しない不要な特徴を一つずつ消していく

### 前向き法

回帰モデルを切片のみの状態の値から開始し、順次、推定結果を改善する説明変数を追加していく。

データ件数に対して変数が多くなる p >> Nの状況であっても計算が可能という利点がある。

モデルの改善が進まなくなったら停止

### 後向き法

- k個の特徴がある状態から、最も不要な特徴を一つずつ取りのぞく
- N > kのときのみ使用できる

<!-- 止まってしまうよりも色々見るのがベスト？ -->

## モデルベース特徴量選択

決定木、ランダムフォレスト、Lasso... feature importance
線形モデル, MARS... 回帰係数

モデルを構築していく段階で特徴量の重要度を数値化



{:.input_area}
```R
library(Boruta)

d <- df_lp_kanto_sp_baked %>% 
  select(-administrative_area_code, -starts_with(".")) %>% 
  verify(ncol(.) == 112L)

# 13 mins.
Bor_lp <- 
  Boruta(posted_land_price ~ ., data = d, doTrace = 2)
Bor_lp
plot(Bor_lp)
# plotImpHistory(Bor_lp)

df_bor_stats <- 
  attStats(Bor_lp) %>% 
  tibble::rownames_to_column() %>% 
  arrange(decision, desc(meanImp))

df_bor_stats %>% 
  count(decision)

df_bor_stats %>% 
  filter(decision == "Confirmed")
```


### 最初の第一歩としての変数重要度の確認

- 客観的な評価、思わぬ存在を発見できるかもしれない
    - 戦略としてはアリ
    - Kaggle... とりあえずGBMに
    - 思わぬ組み合わせ（新しい特徴量の生成）
- その結果を過大評価、他の変数を捨ててしまうことは避けたい

## まとめ

## 関連項目

- 重回帰分析
- PCA (線形変換系手法)
- t-SNE (非線形)
- 解釈

- `dimension-reducion`

## 参考文献

- Trevor Hastie, Robert Tibshirani and Jerome Friedman (2009). The Elements of Statistical Learning (**翻訳** 杉山将ほか訳 (2014). 統計的学習の基礎. (共立出版))
- 久保拓弥 (2012). データ解析のための統計モデリング入門 (岩波書店)
# Forecasting: Principles and Practice — Python での学習ノート

時系列予測の定番教科書 **『Forecasting: Principles and Practice』**（Rob J Hyndman, George Athanasopoulos 著）を読みながら、各章の内容を Python で実装した学習用のノートブックです。

原著のコードは R（`fable` / `tsibble`）で書かれていますが、ここでは Python 版（[the Pythonic Way](https://otexts.com/fpppy/)）を参考に、`statsforecast` / `statsmodels` などのライブラリを使って書き直しています。
あわせて、ARIMA モデルを実際の株価データに当てはめる練習もしています。

※ ノートブック内のコメントは主に中国語です。

---

## 内容

### 第2章 時系列のグラフ（`chapter2  Time series graphics`）

| ファイル | 内容 |
|---|---|
| `2.1 time series graphics.ipynb` | 時系列データの読み込みと日付の変換（オリンピックの記録、PBS 薬剤データ） |
| `2.2 Time plots.ipynb` | 時系列プロット（航空会社の乗客数、薬剤の売上、観光客数） |
| `2.10 exercise.ipynb` | 章末の演習：電力需要、GAFA 株価、売上データの可視化 |

### 第3章 時系列の分解（`chapter 3  Time series decomposition`）

- CPI（消費者物価指数）を使ったインフレ調整などのデータ変換
- 移動平均（5期・7期・2×12 移動平均など）によるトレンドの推定
- **STL 分解**（トレンド・季節性・残差への分解。`seasonal` / `trend` の窓幅や `robust` オプションの比較）

### 第4章 時系列の特徴量（`chapter 4 Time series features`）

- `tsfeatures` を使ったオーストラリア観光データの特徴量の抽出（統計量、ACF、STL ベースの特徴量など）
- 特徴量を**主成分分析（PCA）**で2次元に圧縮して可視化
- `LocalOutlierFactor` による外れ値の検出

### 第5章 予測の基本ツール（`chapter 5  The forecaster’s toolbox`）

- ベンチマーク手法：**平均法・ナイーブ法・季節ナイーブ法・ドリフト法**（`statsforecast`）
- 残差の診断：ACF プロット、**Ljung-Box 検定**
- 予測精度の評価：RMSE・MAE・MAPE・MASE（`utilsforecast`）
- 学習データとテストデータの分割による精度比較

### 第7章 時系列回帰モデル（`chapter 7`）

- 米国の消費・所得データ（`US_change`）を使った線形回帰
- `MLForecast` による回帰モデルの当てはめと、当てはめ値と実測値の比較

### ARIMA の実践（`ARIMA`）

教科書の内容をもとに、実際の株価・気象データで ARIMA モデルを一通り試しました。

| ファイル | 内容 |
|---|---|
| `src/ARIMA.ipynb` | 中国銀行の株価を使った ARIMA の一連の流れ：差分 → **ADF 検定**（定常性の確認）→ ACF / PACF による次数の目安 → BIC による (p, q) の探索とヒートマップ → 残差の検定 → 予測 |
| `src/arima_test01.ipynb` | 上記の流れを `statsmodels` の新しい API で書き直し、逐次的に再学習するローリング予測も試したもの |
| `src/arima_test02.ipynb` | Google の株価に ARIMA を当てはめ、次数ごとの予測結果を比較 |
| `src/arima_test03.ipynb` | Google・Microsoft の株価と都市の湿度・気圧データを使い、移動平均・移動標準偏差、季節分解、STL、ADF 検定、予測誤差の計算を練習 |
| `src/everything-you-can-do-with-a-time-series.ipynb` | Kaggle の公開ノートブック「Everything you can do with a time series」を写経しながら学んだもの |

---

## 使用技術

- **言語**：Python 3（Jupyter Notebook）
- **時系列予測**：statsforecast, mlforecast, utilsforecast, statsmodels, tsfeatures
- **データ処理・機械学習**：pandas, NumPy, SciPy, scikit-learn
- **可視化**：matplotlib, seaborn, plotly

## 実行方法

```bash
pip install pandas numpy scipy scikit-learn matplotlib seaborn plotly \
            statsmodels statsforecast mlforecast utilsforecast tsfeatures fpppy

# 各章のフォルダに移動してからノートブックを開きます（データは相対パス data/ から読み込んでいます）
cd "chapter 5  The forecaster’s toolbox"
jupyter notebook
```

## 参考

- Hyndman, R.J., & Athanasopoulos, G. *Forecasting: Principles and Practice* (3rd ed). https://otexts.com/fpp3/
- *Forecasting: Principles and Practice, the Pythonic Way*. https://otexts.com/fpppy/
- 使用しているデータの多くは、上記の教科書で使われているデータセットです。

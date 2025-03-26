# NumPyとPandasの基礎：データ分析の第一歩

こんにちは、皆さん！今回のブログでは、くるみとジャービスが科学計算の世界への扉を開きます。NumPyとPandasという強力なライブラリを使って、データ分析の基礎を学んでいきましょう。

## くるみとジャービスの対話

**くるみ**: 「ジャービス、最近プログラミングで数値計算をしようとしたんだけど、普通のPythonのリストだと遅くて大変だったよ。もっと効率的な方法はないのかな？」

**ジャービス**: 「それはNumPyを使うべきタイミングですね！NumPyは科学計算のための基本的なライブラリで、多次元配列を効率的に扱えます。実際に見てみましょう。」

```python
import numpy as np

# 普通のPythonリスト
python_list = [1, 2, 3, 4, 5]
print(f"Pythonリスト: {python_list}")

# NumPy配列
numpy_array = np.array([1, 2, 3, 4, 5])
print(f"NumPy配列: {numpy_array}")

# 計算の比較
print(f"Pythonリスト x 2: {[x * 2 for x in python_list]}")
print(f"NumPy配列 x 2: {numpy_array * 2}")
```

**くるみ**: 「わぁ、NumPy配列だと一行で全要素に2を掛けられるんだね！でも、NumPyの本当の強みって何なの？」

**ジャービス**: 「NumPyの強みは多次元配列の効率的な操作、メモリ使用の最適化、そして豊富な数学関数にあります。例えば、マグロの体重データを分析してみましょう。」

```python
# マグロの体重データ（kg）
tuna_weights = np.array([78.5, 82.1, 85.3, 79.8, 77.2, 83.5, 81.9, 84.7])

print(f"平均体重: {np.mean(tuna_weights):.2f} kg")
print(f"最大体重: {np.max(tuna_weights):.2f} kg")
print(f"最小体重: {np.min(tuna_weights):.2f} kg")
print(f"標準偏差: {np.std(tuna_weights):.2f} kg")
```

**くるみ**: 「すごい！簡単に統計情報が得られるんだね。でも、もっと複雑なデータを扱うときはどうするの？例えば、魚の種類や価格なども含めたデータセットとか。」

**ジャービス**: 「そこでPandasの出番です。Pandasは表形式のデータを扱うための強力なライブラリで、NumPyを基盤としています。実際に日本の魚のデータセットを作ってみましょう。」

```python
import pandas as pd

# 日本の魚のデータ
fish_data = {
    '名前': ['マグロ', 'サケ', 'タイ', 'サバ', 'アジ'],
    '重さ(kg)': [80, 5, 3, 1, 0.5],
    '長さ(cm)': [180, 70, 40, 30, 25],
    '生息地': ['太平洋', '北太平洋', '日本海', '太平洋', '日本海'],
    '価格(円/kg)': [3000, 2000, 4000, 1000, 1500]
}

# DataFrameの作成
df = pd.DataFrame(fish_data)
print("魚のデータフレーム:")
print(df)
```

**くるみ**: 「わぁ、きれいな表になったね！これでデータを整理できるけど、特定の情報を取り出したりフィルタリングしたりするにはどうするの？」

**ジャービス**: 「Pandasは直感的なデータ操作方法を提供しています。例えば、特定の列の選択やフィルタリングを見てみましょう。」

```python
# 特定の列を選択
print("\n魚の名前と重さ:")
print(df[['名前', '重さ(kg)']])

# 条件に基づくフィルタリング
heavy_fish = df[df['重さ(kg)'] > 3]
print("\n3kgより重い魚:")
print(heavy_fish)

# 生息地ごとの平均重さ
print("\n生息地ごとの平均重さ:")
print(df.groupby('生息地')['重さ(kg)'].mean())
```

**くるみ**: 「便利だね！でも、このデータを視覚的に理解するにはどうしたらいいの？グラフとかで見られるといいんだけど。」

**ジャービス**: 「Matplotlibというライブラリを使えば、データを様々なグラフで可視化できます。いくつか例を見てみましょう。」

```python
import matplotlib.pyplot as plt

# 棒グラフ：魚の重さ
plt.figure(figsize=(10, 6))
plt.bar(df['名前'], df['重さ(kg)'], color='skyblue')
plt.title('魚の重さ比較')
plt.xlabel('魚の種類')
plt.ylabel('重さ (kg)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# 散布図：重さと長さの関係
plt.figure(figsize=(10, 6))
plt.scatter(df['重さ(kg)'], df['長さ(cm)'], s=df['価格(円/kg)']/50, alpha=0.7)
plt.title('魚の重さと長さの関係')
plt.xlabel('重さ (kg)')
plt.ylabel('長さ (cm)')
for i, name in enumerate(df['名前']):
    plt.annotate(name, (df['重さ(kg)'][i], df['長さ(cm)'][i]))
plt.grid(True, linestyle='--', alpha=0.7)
plt.tight_layout()
plt.show()
```

**くるみ**: 「わぁ、グラフがきれい！マグロは他の魚と比べてとても大きいんだね。でも、これらのライブラリをどう組み合わせて使うのがベストなの？」

**ジャービス**: 「良い質問です。一般的なワークフローとしては、NumPyで数値計算、Pandasでデータ操作と分析、Matplotlibで可視化という流れになります。実際の分析例を見てみましょう。」

## 実践例：日本の魚の市場分析

**ジャービス**: 「より現実的な例として、日本の魚市場のデータを分析してみましょう。まず、より大きなデータセットを作成します。」

```python
# より大きなデータセット
np.random.seed(42)  # 再現性のため

fish_types = ['マグロ', 'サケ', 'タイ', 'サバ', 'アジ', 'ブリ', 'カツオ', 'イワシ', 'サンマ', 'ヒラメ']
habitats = ['太平洋', '日本海', '瀬戸内海', '東シナ海']
months = ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月']

# データの生成
n_samples = 50
data = {
    '魚の種類': np.random.choice(fish_types, n_samples),
    '重さ(kg)': np.random.exponential(5, n_samples),
    '生息地': np.random.choice(habitats, n_samples),
    '月': np.random.choice(months, n_samples),
    '価格(円/kg)': np.random.normal(2000, 500, n_samples)
}

market_df = pd.DataFrame(data)
market_df['総価値(円)'] = market_df['重さ(kg)'] * market_df['価格(円/kg)']

print("魚市場データ（先頭5行）:")
print(market_df.head())
```

**くるみ**: 「おお、本格的なデータセットだね！これでどんな分析ができるの？」

**ジャービス**: 「例えば、月ごとの総漁獲量や魚の種類ごとの平均価格などを分析できます。いくつかの分析を見てみましょう。」

```python
# 月ごとの総漁獲量
monthly_catch = market_df.groupby('月')['重さ(kg)'].sum().reindex(months)
print("\n月ごとの総漁獲量:")
print(monthly_catch)

# 魚の種類ごとの平均価格
fish_prices = market_df.groupby('魚の種類')['価格(円/kg)'].mean().sort_values(ascending=False)
print("\n魚の種類ごとの平均価格:")
print(fish_prices)

# 生息地ごとの魚の分布
habitat_distribution = pd.crosstab(market_df['生息地'], market_df['魚の種類'])
print("\n生息地ごとの魚の分布:")
print(habitat_distribution)
```

**くるみ**: 「データからいろんな情報が得られるんだね！これをグラフで見るとどうなるの？」

**ジャービス**: 「いくつかの可視化を見てみましょう。まず、月ごとの総漁獲量の折れ線グラフです。」

```python
# 月ごとの総漁獲量の折れ線グラフ
plt.figure(figsize=(12, 6))
monthly_catch.plot(kind='line', marker='o')
plt.title('月ごとの総漁獲量')
plt.xlabel('月')
plt.ylabel('総漁獲量 (kg)')
plt.grid(True)
plt.tight_layout()
plt.show()

# 魚の種類ごとの平均価格の棒グラフ
plt.figure(figsize=(12, 6))
fish_prices.plot(kind='bar', color='salmon')
plt.title('魚の種類ごとの平均価格')
plt.xlabel('魚の種類')
plt.ylabel('平均価格 (円/kg)')
plt.grid(axis='y')
plt.tight_layout()
plt.show()

# 生息地ごとの魚の分布のヒートマップ
plt.figure(figsize=(12, 8))
sns.heatmap(habitat_distribution, annot=True, cmap='YlGnBu', fmt='d')
plt.title('生息地ごとの魚の分布')
plt.tight_layout()
plt.show()
```

**くるみ**: 「すごい！データが視覚的に理解しやすくなったね。これを見ると、タイが最も高価で、日本海には様々な種類の魚がいることがわかるよ。」

**ジャービス**: 「そうですね。データ分析の力はまさにここにあります。数値だけでは見えなかったパターンや関係性を視覚化によって発見できるのです。」

## まとめ：NumPyとPandasの威力

**くるみ**: 「今日はNumPyとPandasについて多くのことを学んだね！これらのライブラリを使えば、データ分析がずっと簡単になりそう。」

**ジャービス**: 「その通りです。NumPyとPandasは現代のデータ分析の基盤となるライブラリで、科学計算から機械学習、画像処理まで幅広い分野で活用されています。今日学んだ基礎を応用すれば、より複雑なデータ分析も行えるようになりますよ。」

**くるみ**: 「次は何を学ぶべきかな？」

**ジャービス**: 「次のステップとしては、より高度な可視化ライブラリであるSeabornや、機械学習ライブラリのScikit-learnなどがおすすめです。また、実際のデータセットを使った実践的なプロジェクトに取り組むのも良いでしょう。」

**くるみ**: 「わかった！これからもデータ分析の勉強を続けるよ。今日はありがとう、ジャービス！」

**ジャービス**: 「いつでも質問してくださいね。データ分析の旅を楽しんでください！」

---

このブログでは、NumPyとPandasの基礎から実践的な使い方まで幅広く紹介しました。これらのライブラリを使いこなせるようになれば、データ分析の世界で大きな可能性が広がります。次回のブログもお楽しみに！

[次のセクション：ファイル操作と例外処理](section6_file_operations_blog.html) | [前のセクション：オブジェクト指向プログラミング](section4_oop_blog.html)

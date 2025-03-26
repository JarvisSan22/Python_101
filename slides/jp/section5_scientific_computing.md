# セクション5: 科学計算 - NumPyとPandasの基礎

![科学計算](../../../assets/images/section5_header.jpg)

## 目次

1. [NumPyの基礎](#numpy-の基礎)
   - NumPyとは
   - 配列の作成と操作
   - ブロードキャスティング
   - 数学関数と統計関数
   - 線形代数

2. [Pandasの基礎](#pandas-の基礎)
   - Pandasとは
   - Series と DataFrame
   - データの読み込みと書き込み
   - データの選択と操作
   - データの集計と分析

3. [Matplotlibによる可視化](#matplotlib-による可視化)
   - プロットの基本
   - 様々なグラフの種類
   - グラフのカスタマイズ
   - 複数のサブプロット

---

# NumPy の基礎

## NumPyとは

NumPy（Numerical Python）は、Pythonで科学計算を行うための基本的なパッケージです。以下の機能を提供します：

- 効率的な多次元配列オブジェクト（ndarray）
- 配列に対する高速な数学的操作
- 線形代数、フーリエ変換、乱数生成などのツール

NumPyは、データ分析、機械学習、画像処理など、多くの科学技術分野で広く使用されています。

```python
# NumPyのインポート
import numpy as np
```

## 配列の作成と操作

### 配列の作成

```python
# リストから配列を作成
arr1 = np.array([1, 2, 3, 4, 5])
print("1次元配列:", arr1)

# 多次元配列の作成
arr2 = np.array([[1, 2, 3], [4, 5, 6]])
print("2次元配列:\n", arr2)

# 特殊な配列の作成
zeros = np.zeros((3, 4))  # 0で満たされた3x4配列
print("ゼロ配列:\n", zeros)

ones = np.ones((2, 3))  # 1で満たされた2x3配列
print("1の配列:\n", ones)

identity = np.eye(3)  # 3x3の単位行列
print("単位行列:\n", identity)

# 等間隔の値を持つ配列
linear = np.linspace(0, 10, 5)  # 0から10まで5等分
print("線形間隔配列:", linear)

# 範囲を指定した配列
range_arr = np.arange(0, 10, 2)  # 0から10未満まで2ステップ
print("範囲配列:", range_arr)

# 乱数配列
random_arr = np.random.rand(3, 3)  # 0〜1の一様乱数
print("乱数配列:\n", random_arr)
```

### 配列の属性と情報

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

print("形状:", arr.shape)  # 配列の形状
print("次元数:", arr.ndim)  # 配列の次元数
print("サイズ:", arr.size)  # 要素の総数
print("データ型:", arr.dtype)  # 要素のデータ型
```

### 配列の操作

```python
# 配列の再形成
arr = np.arange(12)
print("元の配列:", arr)

reshaped = arr.reshape(3, 4)  # 3行4列に再形成
print("再形成後:\n", reshaped)

# 配列の転置
transposed = reshaped.T  # 行と列を入れ替え
print("転置後:\n", transposed)

# 配列の結合
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])

vertical = np.vstack((a, b))  # 垂直方向に結合
print("垂直結合:\n", vertical)

horizontal = np.hstack((a, b))  # 水平方向に結合
print("水平結合:\n", horizontal)

# 配列の分割
arr = np.arange(16).reshape(4, 4)
print("元の配列:\n", arr)

# 水平方向に分割
h_split = np.hsplit(arr, 2)
print("水平分割1:\n", h_split[0])
print("水平分割2:\n", h_split[1])

# 垂直方向に分割
v_split = np.vsplit(arr, 2)
print("垂直分割1:\n", v_split[0])
print("垂直分割2:\n", v_split[1])
```

### インデックスとスライス

```python
arr = np.arange(10)
print("元の配列:", arr)

# インデックスによるアクセス
print("インデックス5の要素:", arr[5])

# スライス
print("スライス [2:7]:", arr[2:7])
print("スライス [::2]:", arr[::2])  # 2ステップ

# 多次元配列のインデックス
arr_2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print("2次元配列:\n", arr_2d)

print("要素 (1,2):", arr_2d[1, 2])  # 2行3列の要素
print("1行目:", arr_2d[0])  # 1行目全体

# 多次元スライス
print("部分配列:\n", arr_2d[0:2, 1:3])

# ブール型インデックス
mask = arr > 5
print("マスク:", mask)
print("5より大きい要素:", arr[mask])

# 条件に基づくフィルタリング
print("偶数要素:", arr[arr % 2 == 0])
```

## ブロードキャスティング

ブロードキャスティングは、形状の異なる配列間で算術演算を行うためのNumPyの機能です。

```python
# スカラーと配列の演算
arr = np.array([1, 2, 3, 4])
print("元の配列:", arr)
print("スカラー加算:", arr + 10)
print("スカラー乗算:", arr * 2)

# 異なる形状の配列間の演算
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([10, 20, 30])

print("配列 a:\n", a)
print("配列 b:", b)
print("a + b:\n", a + b)  # bは各行に対してブロードキャスト

# 列ベクトルとのブロードキャスト
c = np.array([[10], [20]])
print("配列 c:\n", c)
print("a + c:\n", a + c)  # cは各列に対してブロードキャスト
```

## 数学関数と統計関数

NumPyには多くの数学関数と統計関数が用意されています。

```python
arr = np.array([1, 2, 3, 4, 5])
print("配列:", arr)

# 基本的な統計
print("合計:", np.sum(arr))
print("平均:", np.mean(arr))
print("標準偏差:", np.std(arr))
print("分散:", np.var(arr))
print("最小値:", np.min(arr))
print("最大値:", np.max(arr))
print("最小値のインデックス:", np.argmin(arr))
print("最大値のインデックス:", np.argmax(arr))

# 多次元配列の統計
arr_2d = np.array([[1, 2, 3], [4, 5, 6]])
print("2次元配列:\n", arr_2d)

print("行ごとの合計:", np.sum(arr_2d, axis=1))
print("列ごとの合計:", np.sum(arr_2d, axis=0))

# 数学関数
angles = np.array([0, np.pi/4, np.pi/2, np.pi])
print("角度:", angles)
print("サイン:", np.sin(angles))
print("コサイン:", np.cos(angles))
print("指数:", np.exp(arr))
print("自然対数:", np.log(arr))
print("平方根:", np.sqrt(arr))
```

## 線形代数

NumPyは線形代数演算のための関数も提供しています。

```python
# 行列の作成
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
print("行列 A:\n", A)
print("行列 B:\n", B)

# 行列の乗算
C = np.dot(A, B)  # または A @ B (Python 3.5以降)
print("行列の積 A・B:\n", C)

# 行列式
det_A = np.linalg.det(A)
print("Aの行列式:", det_A)

# 逆行列
inv_A = np.linalg.inv(A)
print("Aの逆行列:\n", inv_A)
print("A・A^(-1):\n", np.dot(A, inv_A))  # 単位行列に近い結果

# 固有値と固有ベクトル
eigenvalues, eigenvectors = np.linalg.eig(A)
print("Aの固有値:", eigenvalues)
print("Aの固有ベクトル:\n", eigenvectors)

# 行列の分解
U, S, V = np.linalg.svd(A)  # 特異値分解
print("U:\n", U)
print("S:", S)
print("V:\n", V)
```

---

# Pandas の基礎

## Pandasとは

Pandas は、データ分析のための高性能で使いやすいデータ構造とデータ分析ツールを提供するPythonライブラリです。主な特徴：

- データの読み込み、操作、分析のための強力なツール
- 表形式データを扱うための `DataFrame` オブジェクト
- 時系列データの処理に優れた機能
- SQLライクなデータ操作

```python
# Pandasのインポート
import pandas as pd
```

## Series と DataFrame

### Series

Series は、ラベル付きの1次元配列です。

```python
# Seriesの作成
s = pd.Series([1, 3, 5, 7, 9], index=['a', 'b', 'c', 'd', 'e'])
print("Series:\n", s)

# インデックスとデータへのアクセス
print("インデックス:", s.index)
print("データ:", s.values)

# 要素へのアクセス
print("インデックス 'c' の値:", s['c'])
print("複数のインデックス:", s[['a', 'c', 'e']])

# スライス
print("スライス a から c:", s['a':'c'])

# 辞書からSeriesを作成
fish_weights = {'マグロ': 80, 'サケ': 5, 'タイ': 3, 'サバ': 1}
fish_series = pd.Series(fish_weights)
print("魚の重さ:\n", fish_series)
```

### DataFrame

DataFrame は、ラベル付きの2次元表形式データ構造です。

```python
# DataFrameの作成
data = {
    '名前': ['マグロ', 'サケ', 'タイ', 'サバ', 'アジ'],
    '重さ(kg)': [80, 5, 3, 1, 0.5],
    '長さ(cm)': [180, 70, 40, 30, 25],
    '生息地': ['太平洋', '北太平洋', '日本海', '太平洋', '日本海']
}

df = pd.DataFrame(data)
print("魚のデータフレーム:\n", df)

# 基本情報
print("\nデータフレームの情報:")
print("形状:", df.shape)
print("列名:", df.columns)
print("インデックス:", df.index)
print("データ型:\n", df.dtypes)

# 統計情報
print("\n数値データの統計情報:\n", df.describe())

# 先頭/末尾の行を表示
print("\n先頭3行:\n", df.head(3))
print("\n末尾2行:\n", df.tail(2))
```

## データの読み込みと書き込み

Pandasは様々な形式のデータを読み書きできます。

```python
# CSVファイルへの書き込み
df.to_csv('fish_data.csv', index=False)
print("CSVファイルに書き込みました")

# CSVファイルの読み込み
df_from_csv = pd.read_csv('fish_data.csv')
print("\nCSVから読み込んだデータ:\n", df_from_csv)

# Excelファイルへの書き込み
df.to_excel('fish_data.xlsx', index=False)
print("Excelファイルに書き込みました")

# Excelファイルの読み込み
df_from_excel = pd.read_excel('fish_data.xlsx')
print("\nExcelから読み込んだデータ:\n", df_from_excel)

# JSONファイルへの書き込み
df.to_json('fish_data.json', orient='records')
print("JSONファイルに書き込みました")

# JSONファイルの読み込み
df_from_json = pd.read_json('fish_data.json')
print("\nJSONから読み込んだデータ:\n", df_from_json)
```

## データの選択と操作

### 列の選択

```python
# 単一列の選択
names = df['名前']
print("名前の列:\n", names)

# 複数列の選択
size_data = df[['名前', '重さ(kg)', '長さ(cm)']]
print("\n魚のサイズデータ:\n", size_data)
```

### 行の選択

```python
# インデックスによる行の選択
third_row = df.iloc[2]
print("3行目:\n", third_row)

# 複数行の選択
first_three = df.iloc[0:3]
print("\n最初の3行:\n", first_three)

# 条件に基づく行の選択
heavy_fish = df[df['重さ(kg)'] > 3]
print("\n3kgより重い魚:\n", heavy_fish)

pacific_fish = df[df['生息地'] == '太平洋']
print("\n太平洋に生息する魚:\n", pacific_fish)

# 複合条件
large_pacific_fish = df[(df['重さ(kg)'] > 3) & (df['生息地'] == '太平洋')]
print("\n重くて太平洋に生息する魚:\n", large_pacific_fish)
```

### 行と列の両方を選択

```python
# loc: ラベルベースのインデックス
fish_weights = df.loc[0:2, ['名前', '重さ(kg)']]
print("最初の3つの魚の名前と重さ:\n", fish_weights)

# iloc: 位置ベースのインデックス
subset = df.iloc[1:4, 0:2]
print("\n行1-3, 列0-1の部分集合:\n", subset)
```

### データの追加と変更

```python
# 新しい列の追加
df['価格(円/kg)'] = [3000, 2000, 4000, 1000, 1500]
print("価格列を追加したデータフレーム:\n", df)

# 計算に基づく列の追加
df['総価値(円)'] = df['重さ(kg)'] * df['価格(円/kg)']
print("\n総価値を計算したデータフレーム:\n", df)

# 条件に基づく値の設定
df.loc[df['重さ(kg)'] > 10, 'サイズ'] = '大型'
df.loc[(df['重さ(kg)'] <= 10) & (df['重さ(kg)'] > 2), 'サイズ'] = '中型'
df.loc[df['重さ(kg)'] <= 2, 'サイズ'] = '小型'
print("\nサイズ分類を追加したデータフレーム:\n", df)
```

### データの削除

```python
# 列の削除
df_no_price = df.drop('価格(円/kg)', axis=1)
print("価格列を削除したデータフレーム:\n", df_no_price)

# 行の削除
df_no_small = df.drop(df[df['サイズ'] == '小型'].index)
print("\n小型魚を削除したデータフレーム:\n", df_no_small)
```

## データの集計と分析

### グループ化と集計

```python
# 生息地ごとのグループ化
grouped = df.groupby('生息地')

# グループごとの統計
print("生息地ごとの平均値:\n", grouped.mean())
print("\n生息地ごとの合計:\n", grouped.sum())
print("\n生息地ごとの数:\n", grouped.count())

# 複数列でのグループ化
grouped_size = df.groupby(['生息地', 'サイズ'])
print("\n生息地とサイズごとの平均値:\n", grouped_size.mean())

# 特定の集計関数の適用
aggregations = {
    '重さ(kg)': ['min', 'max', 'mean'],
    '長さ(cm)': ['min', 'max', 'mean'],
    '総価値(円)': ['sum']
}
print("\n複数の集計関数:\n", grouped.agg(aggregations))
```

### ピボットテーブル

```python
# ピボットテーブルの作成
pivot = pd.pivot_table(df, 
                       values=['重さ(kg)', '総価値(円)'],
                       index='生息地',
                       columns='サイズ',
                       aggfunc={'重さ(kg)': 'mean', '総価値(円)': 'sum'})
print("ピボットテーブル:\n", pivot)
```

### データの結合

```python
# 追加データの作成
more_fish = pd.DataFrame({
    '名前': ['ブリ', 'カツオ', 'イワシ'],
    '重さ(kg)': [8, 4, 0.3],
    '長さ(cm)': [90, 60, 20],
    '生息地': ['日本海', '太平洋', '日本海']
})

# 縦方向の結合
all_fish = pd.concat([df, more_fish], ignore_index=True)
print("縦方向に結合したデータフレーム:\n", all_fish)

# 魚の栄養データ
nutrition = pd.DataFrame({
    '名前': ['マグロ', 'サケ', 'タイ', 'サバ', 'ブリ'],
    'タンパク質(g/100g)': [23, 20, 18, 22, 21],
    '脂質(g/100g)': [5, 10, 2, 12, 15]
})

# マージ（結合）
fish_with_nutrition = pd.merge(all_fish, nutrition, on='名前', how='left')
print("\n栄養データとマージしたデータフレーム:\n", fish_with_nutrition)
```

### 欠損値の処理

```python
# 欠損値の確認
print("欠損値の数:\n", fish_with_nutrition.isna().sum())

# 欠損値の埋め合わせ
filled = fish_with_nutrition.fillna({
    'タンパク質(g/100g)': fish_with_nutrition['タンパク質(g/100g)'].mean(),
    '脂質(g/100g)': fish_with_nutrition['脂質(g/100g)'].mean()
})
print("\n欠損値を埋めたデータフレーム:\n", filled)

# 欠損値のある行の削除
dropped = fish_with_nutrition.dropna()
print("\n欠損値のある行を削除したデータフレーム:\n", dropped)
```

### データの変換

```python
# カテゴリ変数への変換
filled['生息地'] = filled['生息地'].astype('category')
print("生息地のカテゴリ:\n", filled['生息地'].cat.categories)

# ダミー変数への変換
dummies = pd.get_dummies(filled['生息地'], prefix='生息地')
print("\n生息地のダミー変数:\n", dummies)

# データフレームへの結合
with_dummies = pd.concat([filled, dummies], axis=1)
print("\nダミー変数を追加したデータフレーム:\n", with_dummies.head())
```

---

# Matplotlib による可視化

Matplotlib は、Pythonでデータを可視化するための広く使用されているライブラリです。

```python
import matplotlib.pyplot as plt
```

## プロットの基本

### 線グラフ

```python
# 基本的な線グラフ
plt.figure(figsize=(10, 6))
plt.plot(df['名前'], df['重さ(kg)'], marker='o', linestyle='-', color='b', label='重さ(kg)')
plt.plot(df['名前'], df['長さ(cm)'] / 10, marker='s', linestyle='--', color='r', label='長さ(dm)')
plt.title('魚の重さと長さの比較')
plt.xlabel('魚の種類')
plt.ylabel('測定値')
plt.grid(True)
plt.legend()
plt.xticks(rotation=45)
plt.tight_layout()
plt.savefig('fish_measurements.png')
plt.show()
```

### 棒グラフ

```python
# 棒グラフ
plt.figure(figsize=(10, 6))
plt.bar(df['名前'], df['総価値(円)'] / 1000, color='green', alpha=0.7)
plt.title('魚の総価値比較')
plt.xlabel('魚の種類')
plt.ylabel('総価値（千円）')
plt.xticks(rotation=45)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.tight_layout()
plt.savefig('fish_values.png')
plt.show()
```

### 散布図

```python
# 散布図
plt.figure(figsize=(10, 6))
plt.scatter(df['重さ(kg)'], df['長さ(cm)'], s=df['総価値(円)']/5000, c=df.index, cmap='viridis', alpha=0.7)
plt.title('魚の重さと長さの関係')
plt.xlabel('重さ (kg)')
plt.ylabel('長さ (cm)')
plt.grid(True, linestyle='--', alpha=0.7)
plt.colorbar(label='インデックス')

# 各点にラベルを追加
for i, name in enumerate(df['名前']):
    plt.annotate(name, (df['重さ(kg)'][i], df['長さ(cm)'][i]), 
                 xytext=(5, 5), textcoords='offset points')

plt.tight_layout()
plt.savefig('fish_scatter.png')
plt.show()
```

### 円グラフ

```python
# 円グラフ
plt.figure(figsize=(10, 6))
plt.pie(df['総価値(円)'], labels=df['名前'], autopct='%1.1f%%', 
        startangle=90, shadow=True, explode=[0.1, 0, 0, 0, 0])
plt.title('魚の総価値の割合')
plt.axis('equal')  # 円を真円に保つ
plt.tight_layout()
plt.savefig('fish_pie.png')
plt.show()
```

## 複数のサブプロット

```python
# 複数のサブプロット
fig, axes = plt.subplots(2, 2, figsize=(12, 10))

# 1. 重さの棒グラフ
axes[0, 0].bar(df['名前'], df['重さ(kg)'], color='blue', alpha=0.7)
axes[0, 0].set_title('魚の重さ')
axes[0, 0].set_xlabel('魚の種類')
axes[0, 0].set_ylabel('重さ (kg)')
axes[0, 0].tick_params(axis='x', rotation=45)

# 2. 長さの棒グラフ
axes[0, 1].bar(df['名前'], df['長さ(cm)'], color='green', alpha=0.7)
axes[0, 1].set_title('魚の長さ')
axes[0, 1].set_xlabel('魚の種類')
axes[0, 1].set_ylabel('長さ (cm)')
axes[0, 1].tick_params(axis='x', rotation=45)

# 3. 総価値の円グラフ
axes[1, 0].pie(df['総価値(円)'], labels=df['名前'], autopct='%1.1f%%', 
              startangle=90, shadow=True)
axes[1, 0].set_title('総価値の割合')
axes[1, 0].axis('equal')

# 4. 重さと長さの散布図
scatter = axes[1, 1].scatter(df['重さ(kg)'], df['長さ(cm)'], 
                            s=df['総価値(円)']/5000, c=df.index, cmap='viridis', alpha=0.7)
axes[1, 1].set_title('重さと長さの関係')
axes[1, 1].set_xlabel('重さ (kg)')
axes[1, 1].set_ylabel('長さ (cm)')
axes[1, 1].grid(True, linestyle='--', alpha=0.7)

# カラーバーを追加
cbar = fig.colorbar(scatter, ax=axes[1, 1])
cbar.set_label('インデックス')

# レイアウトの調整
plt.tight_layout()
plt.savefig('fish_dashboard.png')
plt.show()
```

## Pandasとの統合

Pandasは、Matplotlibを使用した可視化メソッドを提供しています。

```python
# Pandasの組み込みプロット機能
df.plot(x='名前', y=['重さ(kg)', '長さ(cm)'], kind='bar', figsize=(10, 6))
plt.title('魚の重さと長さ')
plt.ylabel('測定値')
plt.xticks(rotation=45)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.tight_layout()
plt.savefig('fish_pandas_bar.png')
plt.show()

# 散布図行列
pd.plotting.scatter_matrix(df[['重さ(kg)', '長さ(cm)', '総価値(円)']], 
                          figsize=(10, 8), diagonal='kde')
plt.tight_layout()
plt.savefig('fish_scatter_matrix.png')
plt.show()

# 箱ひげ図
df.boxplot(column=['重さ(kg)', '長さ(cm)'], by='生息地', figsize=(10, 6))
plt.suptitle('生息地別の魚のサイズ分布')
plt.tight_layout()
plt.savefig('fish_boxplot.png')
plt.show()
```

---

# 実践例: 魚のデータ分析

以下は、これまで学んだNumPy、Pandas、Matplotlibを使用した実践的なデータ分析の例です。

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns  # より美しい可視化のために

# より大きなデータセットを作成
np.random.seed(42)  # 再現性のため

# 魚の種類
fish_types = ['マグロ', 'サケ', 'タイ', 'サバ', 'アジ', 'ブリ', 'カツオ', 'イワシ', 
              'サンマ', 'ヒラメ', 'タコ', 'イカ', 'エビ', 'カニ', 'ウニ']

# 生息地
habitats = ['太平洋', '日本海', '瀬戸内海', '東シナ海', '北大西洋']

# データの生成
n_samples = 100
data = {
    '名前': np.random.choice(fish_types, n_samples),
    '重さ(kg)': np.random.exponential(5, n_samples),
    '長さ(cm)': np.random.normal(50, 20, n_samples),
    '生息地': np.random.choice(habitats, n_samples),
    '捕獲日': pd.date_range(start='2023-01-01', periods=n_samples),
    '価格(円/kg)': np.random.normal(2000, 500, n_samples)
}

# DataFrameの作成
fish_df = pd.DataFrame(data)

# データの前処理
fish_df['総価値(円)'] = fish_df['重さ(kg)'] * fish_df['価格(円/kg)']

# サイズカテゴリの追加
fish_df.loc[fish_df['重さ(kg)'] > 10, 'サイズ'] = '大型'
fish_df.loc[(fish_df['重さ(kg)'] <= 10) & (fish_df['重さ(kg)'] > 2), 'サイズ'] = '中型'
fish_df.loc[fish_df['重さ(kg)'] <= 2, 'サイズ'] = '小型'

# 月情報の抽出
fish_df['月'] = fish_df['捕獲日'].dt.month

# データの概要
print("データの概要:")
print(fish_df.info())
print("\n基本統計量:")
print(fish_df.describe())

# 魚の種類ごとの集計
fish_summary = fish_df.groupby('名前').agg({
    '重さ(kg)': ['count', 'mean', 'std', 'min', 'max'],
    '長さ(cm)': ['mean', 'min', 'max'],
    '総価値(円)': ['sum', 'mean']
})
print("\n魚の種類ごとの集計:")
print(fish_summary)

# 生息地ごとの集計
habitat_summary = fish_df.groupby('生息地').agg({
    '名前': pd.Series.nunique,
    '重さ(kg)': ['mean', 'sum'],
    '総価値(円)': ['sum', 'mean']
})
print("\n生息地ごとの集計:")
print(habitat_summary)

# 月ごとの集計
monthly_summary = fish_df.groupby('月').agg({
    '重さ(kg)': 'sum',
    '総価値(円)': 'sum'
})
print("\n月ごとの集計:")
print(monthly_summary)

# データの可視化

# テーマの設定
sns.set_theme(style="whitegrid")

# 1. 魚の種類ごとの平均重量
plt.figure(figsize=(12, 6))
avg_weight = fish_df.groupby('名前')['重さ(kg)'].mean().sort_values(ascending=False)
sns.barplot(x=avg_weight.index, y=avg_weight.values)
plt.title('魚の種類ごとの平均重量')
plt.xlabel('魚の種類')
plt.ylabel('平均重量 (kg)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.savefig('avg_weight_by_fish.png')
plt.show()

# 2. 生息地ごとの魚の分布
plt.figure(figsize=(12, 6))
habitat_counts = fish_df.groupby(['生息地', '<response clipped><NOTE>To save on context only part of this file has been shown to you. You should retry this tool after you have searched inside the file with `grep -n` in order to find the line numbers of what you are looking for.</NOTE>
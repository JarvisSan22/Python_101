# セクション1: Python の基礎 - スライド

## Python とは？

---

### Python の概要

- 高水準プログラミング言語
- 読みやすく、書きやすい構文
- 多目的言語（Web開発、データ分析、AI、自動化など）
- 豊富なライブラリとフレームワーク
- 活発なコミュニティ
- 初心者に優しい

---

### Python の歴史

- 1991年にグイド・ヴァン・ロッサムによって開発
- 名前はイギリスのコメディグループ「モンティ・パイソン」から
- Python 2.x と Python 3.x の主要バージョン
- Python 2 は 2020年1月1日にサポート終了
- 現在は Python 3 を使用すべき

---

### なぜ Python を学ぶのか？

- 初心者に優しい構文
- 幅広い用途
- 高い需要のあるスキル
- 豊富なライブラリとフレームワーク
- 強力なコミュニティサポート
- 生産性の高さ

---

## Python のインストールと設定

---

### Python のインストール

- [python.org](https://www.python.org/downloads/) から公式インストーラーをダウンロード
- インストール時に「Add Python to PATH」オプションを選択
- コマンドラインで確認:
  ```
  python --version
  ```
  または
  ```
  python3 --version
  ```

---

### 統合開発環境（IDE）とコードエディタ

- **IDLE**: Python に付属する基本的な IDE
- **VS Code**: 軽量で拡張可能なエディタ
- **PyCharm**: Python 専用の強力な IDE
- **Jupyter Notebook**: インタラクティブな開発に最適
- **Google Colab**: クラウドベースの Jupyter 環境

---

### 仮想環境

- プロジェクト固有の依存関係を管理
- 異なるプロジェクト間の競合を防止
- 作成方法:
  ```
  python -m venv myenv
  ```
- 有効化方法 (Windows):
  ```
  myenv\Scripts\activate
  ```
- 有効化方法 (macOS/Linux):
  ```
  source myenv/bin/activate
  ```

---

## Python の基本構文

---

### 最初の Python プログラム

```python
# これは私の最初の Python プログラムです
print("こんにちは、世界！")
print("Python プログラミングへようこそ！")
```

実行方法:
1. ファイルに保存 (例: `hello.py`)
2. コマンドラインで実行:
   ```
   python hello.py
   ```

---

### コメント

```python
# これは一行コメントです

"""
これは複数行コメントです。
ドキュメンテーション文字列（docstring）としても使用されます。
"""
```

---

### 変数と代入

```python
# 変数の宣言と代入
name = "コイ"
age = 3
length = 25.5
is_healthy = True

# 変数の使用
print(name)
print(age)
print(length)
print(is_healthy)
```

---

### 変数の命名規則

- 文字、数字、アンダースコアを使用可能
- 数字で始めることはできない
- 大文字と小文字は区別される
- 予約語（if, for, while など）は使用できない

```python
# 良い変数名
fish_name = "マグロ"
fish_count = 5
total_length = 120.5

# 避けるべき変数名
1fish = "タイ"  # 数字で始まる（エラー）
fish-type = "淡水"  # ハイフンを含む（エラー）
```

---

### データ型

- **整数 (int)**: `1`, `100`, `-10`
- **浮動小数点数 (float)**: `3.14`, `-0.001`
- **文字列 (str)**: `"こんにちは"`, `'Python'`
- **ブール値 (bool)**: `True`, `False`
- **リスト (list)**: `[1, 2, 3]`, `["コイ", "フグ", "タイ"]`
- **タプル (tuple)**: `(1, 2, 3)`, `("コイ", "フグ", "タイ")`
- **辞書 (dict)**: `{"name": "コイ", "age": 3}`
- **集合 (set)**: `{1, 2, 3}`, `{"コイ", "フグ", "タイ"}`
- **None**: 値がないことを表す

---

### 型の確認と変換

```python
# 型の確認
fish_name = "コイ"
fish_age = 3
fish_length = 25.5

print(type(fish_name))  # <class 'str'>
print(type(fish_age))   # <class 'int'>
print(type(fish_length))  # <class 'float'>

# 型変換
age_str = str(fish_age)  # 整数から文字列へ
length_int = int(fish_length)  # 浮動小数点数から整数へ
age_float = float(fish_age)  # 整数から浮動小数点数へ
```

---

## 基本的な演算

---

### 算術演算子

```python
# 基本的な算術演算
a = 10
b = 3

print(a + b)  # 加算: 13
print(a - b)  # 減算: 7
print(a * b)  # 乗算: 30
print(a / b)  # 除算: 3.3333...
print(a // b)  # 整数除算: 3
print(a % b)  # 剰余: 1
print(a ** b)  # べき乗: 1000
```

---

### 比較演算子

```python
a = 10
b = 3

print(a == b)  # 等しい: False
print(a != b)  # 等しくない: True
print(a > b)   # より大きい: True
print(a < b)   # より小さい: False
print(a >= b)  # 以上: True
print(a <= b)  # 以下: False
```

---

### 論理演算子

```python
x = True
y = False

print(x and y)  # 論理積 (AND): False
print(x or y)   # 論理和 (OR): True
print(not x)    # 否定 (NOT): False

# 実際の例
is_koi = True
is_large = False
is_healthy = True

is_valuable = is_koi and is_large  # False
needs_attention = is_large or not is_healthy  # False
```

---

### 代入演算子

```python
# 基本的な代入
x = 10

# 複合代入演算子
x += 5   # x = x + 5 と同じ (x は 15 になる)
x -= 3   # x = x - 3 と同じ (x は 12 になる)
x *= 2   # x = x * 2 と同じ (x は 24 になる)
x /= 4   # x = x / 4 と同じ (x は 6.0 になる)
x //= 2  # x = x // 2 と同じ (x は 3.0 になる)
x %= 2   # x = x % 2 と同じ (x は 1.0 になる)
x **= 3  # x = x ** 3 と同じ (x は 1.0 になる)
```

---

## 文字列操作

---

### 文字列の作成

```python
# 単一引用符または二重引用符を使用
single_quotes = '日本の魚'
double_quotes = "コイとフグ"

# 三重引用符で複数行の文字列を作成
multi_line = """これは
複数行の
文字列です。"""

print(single_quotes)
print(double_quotes)
print(multi_line)
```

---

### 文字列の連結

```python
# + 演算子を使用
first = "コイ"
second = "フグ"
combined = first + " と " + second

print(combined)  # "コイ と フグ"

# 文字列の繰り返し
repeated = "魚" * 3
print(repeated)  # "魚魚魚"
```

---

### 文字列のインデックスとスライス

```python
fish = "マグロ"

# インデックス（0から始まる）
print(fish[0])  # "マ"
print(fish[1])  # "グ"
print(fish[-1])  # "ロ" (負のインデックスは末尾から)

# スライス [開始:終了:ステップ]
fish_types = "マグロ、サバ、タイ、フグ"
print(fish_types[0:6])    # "マグロ、サ"
print(fish_types[4:])     # "サバ、タイ、フグ"
print(fish_types[:8])     # "マグロ、サバ"
print(fish_types[::2])    # "マロサタフ"
```

---

### 文字列メソッド

```python
fish = "コイ"
fish_types = "マグロ、サバ、タイ、フグ"

# 一般的なメソッド
print(len(fish))               # 長さ: 2
print(fish.upper())            # 大文字に: "コイ"
print(fish.lower())            # 小文字に: "こい"
print(fish_types.split("、"))   # 分割: ["マグロ", "サバ", "タイ", "フグ"]
print("  魚  ".strip())        # 前後の空白を削除: "魚"
print(fish_types.replace("マグロ", "カツオ"))  # 置換: "カツオ、サバ、タイ、フグ"
print("タイ" in fish_types)     # 含まれているか: True
```

---

### 文字列フォーマット

```python
# % 演算子（古い方法）
fish = "コイ"
age = 3
length = 25.5
print("%sは%d歳で、長さは%.1fcmです。" % (fish, age, length))

# str.format() メソッド
print("{}は{}歳で、長さは{:.1f}cmです。".format(fish, age, length))

# f-strings (Python 3.6+)
print(f"{fish}は{age}歳で、長さは{length:.1f}cmです。")
```

---

## 入力と出力

---

### print() 関数

```python
# 基本的な使用法
print("こんにちは")

# 複数の値を出力
name = "コイ"
age = 3
print(name, age)  # "コイ 3"

# sep パラメータで区切り文字を指定
print(name, age, sep=": ")  # "コイ: 3"

# end パラメータで終端文字を指定
print(name, end=" -> ")
print(age)  # "コイ -> 3"
```

---

### input() 関数

```python
# ユーザーからの入力を取得
name = input("魚の名前を入力してください: ")
print(f"こんにちは、{name}さん！")

# 数値入力（文字列から変換が必要）
age_str = input("魚の年齢を入力してください: ")
age = int(age_str)
print(f"その魚は{age}歳です。")

# 一行で書く場合
length = float(input("魚の長さ（cm）を入力してください: "))
print(f"その魚は{length}cmです。")
```

---

## 条件文

---

### if 文

```python
fish_length = 25

if fish_length > 20:
    print("これは大きな魚です。")
```

---

### if-else 文

```python
fish_length = 15

if fish_length > 20:
    print("これは大きな魚です。")
else:
    print("これは小さな魚です。")
```

---

### if-elif-else 文

```python
fish_length = 15

if fish_length > 30:
    print("これはとても大きな魚です。")
elif fish_length > 20:
    print("これは大きな魚です。")
elif fish_length > 10:
    print("これは中くらいの魚です。")
else:
    print("これは小さな魚です。")
```

---

### 条件式（三項演算子）

```python
fish_length = 25
size = "大きい" if fish_length > 20 else "小さい"
print(f"この魚は{size}です。")
```

---

### 論理演算子を使った複合条件

```python
fish_type = "コイ"
fish_length = 25
fish_weight = 3.5

if fish_type == "コイ" and fish_length > 20:
    print("これは大きなコイです。")

if fish_length > 20 or fish_weight > 4:
    print("これは大きな魚です。")

if not (fish_length < 10):
    print("これは小さな魚ではありません。")
```

---

## ループ

---

### for ループ

```python
# リストの各要素に対して繰り返し
fish_types = ["コイ", "フグ", "タイ", "サバ"]
for fish in fish_types:
    print(fish)

# 範囲に対して繰り返し
for i in range(5):  # 0, 1, 2, 3, 4
    print(i)

# 開始、終了、ステップを指定
for i in range(1, 10, 2):  # 1, 3, 5, 7, 9
    print(i)
```

---

### while ループ

```python
# 条件が True である限り繰り返し
count = 0
while count < 5:
    print(count)
    count += 1

# break を使用して早期終了
count = 0
while True:
    print(count)
    count += 1
    if count >= 5:
        break
```

---

### ループ制御ステートメント

```python
# break: ループを終了
for i in range(10):
    if i == 5:
        break
    print(i)  # 0, 1, 2, 3, 4

# continue: 現在の反復をスキップして次へ
for i in range(10):
    if i % 2 == 0:  # 偶数の場合
        continue
    print(i)  # 1, 3, 5, 7, 9

# else 節: ループが正常に完了した場合に実行
for i in range(5):
    print(i)
else:
    print("ループ完了")  # ループが break されなければ実行される
```

---

### ネストしたループ

```python
# 2次元の繰り返し
for i in range(3):
    for j in range(2):
        print(f"i={i}, j={j}")

# 実際の例: 魚のサイズ表
fish_types = ["コイ", "フグ", "タイ"]
sizes = ["小", "中", "大"]

for fish in fish_types:
    for size in sizes:
        print(f"{size}サイズの{fish}")
```

---

## まとめ

---

### 学んだこと

- Python の基本と環境設定
- 変数とデータ型
- 基本的な演算子
- 文字列操作
- 入力と出力
- 条件文
- ループ

---

### 次のステップ

- データ構造（リスト、タプル、辞書、集合）
- 関数とモジュール
- ファイル操作
- エラー処理
- オブジェクト指向プログラミング
- 外部ライブラリの使用

---

### 練習問題

1. 魚の名前と長さを入力として受け取り、サイズ（小/中/大）を判定するプログラムを作成する
2. 1から100までの数字を出力し、3の倍数では「Fizz」、5の倍数では「Buzz」、両方の倍数では「FizzBuzz」を出力する
3. ユーザーが「終了」と入力するまで、魚の名前を入力し続けるプログラムを作成する

---

### 参考資料

- [Python 公式ドキュメント](https://docs.python.org/ja/3/)
- [Python チュートリアル](https://docs.python.org/ja/3/tutorial/index.html)
- [Real Python](https://realpython.com/)
- [W3Schools Python チュートリアル](https://www.w3schools.com/python/)

---

## ご質問はありますか？

---

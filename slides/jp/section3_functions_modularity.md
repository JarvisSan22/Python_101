# セクション3: 関数とモジュール性 - スライド

## 関数とモジュール性

---

### 関数とは？

- コードの再利用可能なブロック
- 特定のタスクを実行するためのまとまった命令群
- 入力（引数）を受け取り、出力（戻り値）を返すことができる
- コードの整理と再利用性の向上に役立つ

---

### 関数を定義する

```python
def 関数名(引数1, 引数2, ...):
    """ドキュメンテーション文字列（docstring）"""
    # 関数の本体
    # 処理を記述
    return 戻り値  # 省略可能
```

例：

```python
def greet_fish(fish_name):
    """魚に挨拶する関数"""
    return f"こんにちは、{fish_name}さん！"

# 関数の呼び出し
message = greet_fish("マグロ")
print(message)  # こんにちは、マグロさん！
```

---

### 引数と戻り値

```python
# 複数の引数
def describe_fish(name, weight, length):
    """魚の説明を返す関数"""
    return f"{name}は重さ{weight}kg、長さ{length}cmです。"

# 関数の呼び出し
description = describe_fish("マグロ", 80, 150)
print(description)  # マグロは重さ80kg、長さ150cmです。
```

---

### 戻り値なしの関数

```python
def print_fish_info(name, type):
    """魚の情報を表示する関数（戻り値なし）"""
    print(f"名前: {name}")
    print(f"種類: {type}")
    # return文がない場合、Noneを返す

# 関数の呼び出し
result = print_fish_info("マグロ", "大型魚")
print(f"戻り値: {result}")  # 戻り値: None
```

---

### 引数の種類

1. **必須引数**: 関数定義の順序通りに渡す必要がある
2. **キーワード引数**: 名前を指定して渡す引数
3. **デフォルト引数**: デフォルト値を持つ引数
4. **可変長引数**: 任意の数の引数を受け取る

---

### キーワード引数

```python
def describe_fish(name, weight, length):
    return f"{name}は重さ{weight}kg、長さ{length}cmです。"

# キーワード引数を使用
description = describe_fish(length=150, name="マグロ", weight=80)
print(description)  # マグロは重さ80kg、長さ150cmです。
```

---

### デフォルト引数

```python
def describe_fish(name, weight=0, length=0):
    """デフォルト値を持つ引数を使用した関数"""
    return f"{name}は重さ{weight}kg、長さ{length}cmです。"

# デフォルト値を使用
print(describe_fish("サケ"))  # サケは重さ0kg、長さ0cmです。

# 一部の引数を指定
print(describe_fish("タイ", length=40))  # タイは重さ0kg、長さ40cmです。

# すべての引数を指定
print(describe_fish("マグロ", 80, 150))  # マグロは重さ80kg、長さ150cmです。
```

---

### 可変長引数 (*args)

```python
def fish_average(*lengths):
    """任意の数の魚の長さの平均を計算する関数"""
    total = sum(lengths)
    count = len(lengths)
    return total / count if count > 0 else 0

# 異なる数の引数で呼び出し
print(fish_average(10, 20, 30))  # 20.0
print(fish_average(15, 25, 10, 30, 20))  # 20.0
```

---

### キーワード可変長引数 (**kwargs)

```python
def fish_details(**kwargs):
    """魚の詳細情報を表示する関数"""
    print("魚の詳細:")
    for key, value in kwargs.items():
        print(f"  {key}: {value}")

# 異なるキーワード引数で呼び出し
fish_details(name="マグロ", weight=80, length=150, habitat="太平洋")
# 魚の詳細:
#   name: マグロ
#   weight: 80
#   length: 150
#   habitat: 太平洋
```

---

### 引数の組み合わせ

```python
def fish_report(name, *args, location="不明", **kwargs):
    """魚のレポートを生成する関数"""
    print(f"魚名: {name}")
    print(f"場所: {location}")
    
    if args:
        print("測定値:")
        for i, value in enumerate(args, 1):
            print(f"  測定{i}: {value}")
    
    if kwargs:
        print("追加情報:")
        for key, value in kwargs.items():
            print(f"  {key}: {value}")

# 様々な引数の組み合わせで呼び出し
fish_report("マグロ", 80, 150, 3, location="太平洋", 
           color="赤身", season="冬", price=3000)
```

---

### 関数のスコープ

- **ローカルスコープ**: 関数内で定義された変数
- **グローバルスコープ**: 関数の外で定義された変数
- **ビルトインスコープ**: Python の組み込み関数や例外など

```python
fish_type = "マグロ"  # グローバル変数

def change_fish():
    fish_type = "サケ"  # ローカル変数
    print(f"関数内: {fish_type}")

change_fish()  # 関数内: サケ
print(f"関数外: {fish_type}")  # 関数外: マグロ
```

---

### global キーワード

```python
fish_count = 0  # グローバル変数

def add_fish():
    global fish_count  # グローバル変数を使用することを宣言
    fish_count += 1
    print(f"魚を追加しました。現在の数: {fish_count}")

add_fish()  # 魚を追加しました。現在の数: 1
add_fish()  # 魚を追加しました。現在の数: 2
print(f"合計: {fish_count}")  # 合計: 2
```

---

### 関数内関数（ネストした関数）

```python
def fish_processor(fish_list):
    """魚のリストを処理する関数"""
    
    def filter_big_fish(fish):
        """大きな魚（50cm以上）をフィルタリングする内部関数"""
        return fish["length"] >= 50
    
    big_fish = [fish for fish in fish_list if filter_big_fish(fish)]
    return big_fish

# 関数の使用
fishes = [
    {"name": "マグロ", "length": 150},
    {"name": "サケ", "length": 80},
    {"name": "タイ", "length": 40}
]
result = fish_processor(fishes)
print(result)  # [{'name': 'マグロ', 'length': 150}, {'name': 'サケ', 'length': 80}]
```

---

### 再帰関数

自分自身を呼び出す関数

```python
def countdown(n):
    """再帰的なカウントダウン関数"""
    if n <= 0:
        print("発射！")
    else:
        print(n)
        countdown(n - 1)  # 自分自身を呼び出す

countdown(3)
# 3
# 2
# 1
# 発射！
```

---

### 再帰関数の例：階乗

```python
def factorial(n):
    """階乗を計算する再帰関数"""
    if n <= 1:
        return 1
    else:
        return n * factorial(n - 1)

print(factorial(5))  # 120 (5 * 4 * 3 * 2 * 1)
```

---

### ラムダ関数（無名関数）

```python
# 通常の関数
def square(x):
    return x ** 2

# 同等のラムダ関数
square_lambda = lambda x: x ** 2

print(square(5))       # 25
print(square_lambda(5))  # 25

# ラムダ関数の使用例（ソート）
fish_data = [
    {"name": "マグロ", "weight": 80},
    {"name": "サケ", "weight": 5},
    {"name": "タイ", "weight": 3}
]

# 重さでソート
sorted_fish = sorted(fish_data, key=lambda fish: fish["weight"])
for fish in sorted_fish:
    print(f"{fish['name']}: {fish['weight']}kg")
```

---

## モジュール

---

### モジュールとは？

- 関連する関数、クラス、変数をまとめたファイル
- コードを論理的に整理するための仕組み
- 再利用可能なコードライブラリを作成できる
- Python の標準ライブラリは多数のモジュールで構成されている

---

### モジュールのインポート

```python
# モジュール全体をインポート
import math

# モジュールの関数を使用
radius = 5
area = math.pi * math.pow(radius, 2)
print(f"円の面積: {area}")  # 円の面積: 78.53981633974483
```

---

### 特定の関数やオブジェクトをインポート

```python
# 特定の関数やオブジェクトをインポート
from math import pi, sqrt

# 直接使用（モジュール名なしで）
radius = 5
area = pi * radius ** 2
print(f"円の面積: {area}")  # 円の面積: 78.53981633974483

# 平方根の計算
print(f"2の平方根: {sqrt(2)}")  # 2の平方根: 1.4142135623730951
```

---

### 別名を付けてインポート

```python
# モジュールに別名を付ける
import math as m

print(f"円周率: {m.pi}")  # 円周率: 3.141592653589793

# 関数に別名を付ける
from math import sqrt as square_root

print(f"3の平方根: {square_root(3)}")  # 3の平方根: 1.7320508075688772
```

---

### すべてのオブジェクトをインポート

```python
# すべてのオブジェクトをインポート（非推奨）
from math import *

print(f"円周率: {pi}")
print(f"2の平方根: {sqrt(2)}")
print(f"3の3乗: {pow(3, 3)}")
```

注意: この方法は名前の衝突を引き起こす可能性があるため、一般的には推奨されません。

---

### 標準ライブラリのモジュール

Python には多数の標準ライブラリモジュールが含まれています：

- **math**: 数学関数
- **random**: 乱数生成
- **datetime**: 日付と時間の操作
- **os**: オペレーティングシステムとの対話
- **sys**: システム固有のパラメータと関数
- **json**: JSON データの処理
- **re**: 正規表現
- **collections**: 特殊なコンテナデータ型
- **itertools**: 効率的なループのためのイテレータ

---

### math モジュール

```python
import math

# 基本的な数学関数
print(f"円周率: {math.pi}")
print(f"自然対数の底: {math.e}")
print(f"2の平方根: {math.sqrt(2)}")
print(f"3の3乗: {math.pow(3, 3)}")
print(f"5の絶対値: {math.fabs(-5)}")
print(f"7の階乗: {math.factorial(7)}")

# 三角関数（ラジアン単位）
print(f"sin(π/2): {math.sin(math.pi/2)}")
print(f"cos(π): {math.cos(math.pi)}")

# 角度変換
print(f"30度をラジアンに: {math.radians(30)}")
print(f"π/4ラジアンを度に: {math.degrees(math.pi/4)}")

# 対数関数
print(f"log(100, 10): {math.log(100, 10)}")  # 底が10の対数
print(f"log(e^2): {math.log(math.exp(2))}")  # 自然対数
```

---

### random モジュール

```python
import random

# 乱数生成
print(f"0から1の乱数: {random.random()}")
print(f"1から10の整数乱数: {random.randint(1, 10)}")
print(f"0から100の一様分布: {random.uniform(0, 100)}")

# リストからのランダムな選択
fish_types = ["マグロ", "サケ", "タイ", "フグ", "サバ"]
print(f"ランダムな魚: {random.choice(fish_types)}")
print(f"ランダムな3種類の魚: {random.sample(fish_types, 3)}")

# リストのシャッフル
fish_copy = fish_types.copy()
random.shuffle(fish_copy)
print(f"シャッフルした魚のリスト: {fish_copy}")
```

---

### datetime モジュール

```python
from datetime import datetime, date, time, timedelta

# 現在の日時
now = datetime.now()
print(f"現在の日時: {now}")

# 特定の日時の作成
fishing_date = datetime(2023, 5, 15, 8, 30, 0)
print(f"釣り日: {fishing_date}")

# 日付のフォーマット
print(f"フォーマット済み日付: {fishing_date.strftime('%Y年%m月%d日 %H時%M分')}")

# 日時の計算
tomorrow = now + timedelta(days=1)
print(f"明日の日時: {tomorrow}")

# 日時の差分
diff = tomorrow - now
print(f"差分（秒）: {diff.total_seconds()}")
```

---

### 自作モジュールの作成

fish_utils.py:
```python
"""魚に関するユーティリティ関数を提供するモジュール"""

# 定数
WATER_TYPES = ["淡水", "海水", "汽水"]

def calculate_fish_price(weight, price_per_kg):
    """魚の価格を計算する関数"""
    return weight * price_per_kg

def is_big_fish(length):
    """大きな魚かどうかを判定する関数"""
    return length >= 100

class Fish:
    """魚を表すクラス"""
    def __init__(self, name, weight, length):
        self.name = name
        self.weight = weight
        self.length = length
    
    def describe(self):
        """魚の説明を返すメソッド"""
        return f"{self.name}は重さ{self.weight}kg、長さ{self.length}cmです。"
```

---

### 自作モジュールの使用

```python
# 自作モジュールのインポート
import fish_utils

# 定数の使用
print(f"水の種類: {fish_utils.WATER_TYPES}")

# 関数の使用
price = fish_utils.calculate_fish_price(5, 2000)
print(f"魚の価格: {price}円")

# クラスの使用
tuna = fish_utils.Fish("マグロ", 80, 150)
print(tuna.describe())
```

---

### パッケージ

- 複数のモジュールを階層的に整理したもの
- ディレクトリとして表現され、`__init__.py` ファイルを含む
- 大規模なプロジェクトのコードを整理するのに役立つ

```
fish_package/
│
├── __init__.py
├── freshwater.py
├── saltwater.py
└── utils.py
```

---

### パッケージの使用

```python
# パッケージ全体をインポート
import fish_package

# 特定のモジュールをインポート
from fish_package import freshwater

# 特定のモジュールから特定の関数をインポート
from fish_package.saltwater import get_tuna_info

# サブパッケージからのインポート
from fish_package.utils.math import calculate_weight
```

---

### \_\_name\_\_ 変数

- 各モジュールには `__name__` という特殊な変数がある
- モジュールが直接実行された場合、`__name__` は `"__main__"` になる
- モジュールがインポートされた場合、`__name__` はモジュール名になる

```python
# fish_module.py
def get_fish_info():
    return "これは魚の情報です。"

print(f"モジュール名: {__name__}")

if __name__ == "__main__":
    print("このモジュールは直接実行されています。")
    print(get_fish_info())
else:
    print("このモジュールはインポートされています。")
```

---

### \_\_name\_\_ の使用例

```python
# main.py
import fish_module

print("main.py の実行")
info = fish_module.get_fish_info()
print(info)
```

実行結果:
```
# fish_module.py を直接実行した場合:
モジュール名: __main__
このモジュールは直接実行されています。
これは魚の情報です。

# main.py を実行した場合:
モジュール名: fish_module
このモジュールはインポートされています。
main.py の実行
これは魚の情報です。
```

---

### モジュールの検索パス

Python はモジュールを以下の順序で検索します：

1. 現在のディレクトリ
2. PYTHONPATH 環境変数で指定されたディレクトリ
3. インストールされた標準ライブラリのディレクトリ
4. サードパーティのパッケージがインストールされたディレクトリ

```python
import sys

# モジュールの検索パスを表示
for path in sys.path:
    print(path)
```

---

### サードパーティのパッケージ

- Python Package Index (PyPI) から入手可能
- `pip` コマンドを使用してインストール

```bash
# パッケージのインストール
pip install numpy

# 特定のバージョンをインストール
pip install pandas==1.3.0

# パッケージのアップグレード
pip install --upgrade matplotlib

# インストール済みパッケージの一覧表示
pip list
```

---

### 仮想環境

- プロジェクトごとに独立した Python 環境を作成
- パッケージの依存関係の衝突を避ける
- `venv` モジュールを使用して作成

```bash
# 仮想環境の作成
python -m venv myenv

# 仮想環境のアクティベート（Windows）
myenv\Scripts\activate

# 仮想環境のアクティベート（macOS/Linux）
source myenv/bin/activate

# 仮想環境の非アクティベート
deactivate
```

---

### requirements.txt

- プロジェクトの依存関係を記録するファイル
- 他の開発者と環境を共有するのに役立つ

```bash
# 現在の依存関係を requirements.txt に出力
pip freeze > requirements.txt

# requirements.txt からパッケージをインストール
pip install -r requirements.txt
```

---

## 関数型プログラミング

---

### 関数型プログラミングとは？

- 関数を第一級オブジェクトとして扱うプログラミングパラダイム
- 状態の変更や可変データを避ける
- 副作用のない純粋関数を使用
- Python は関数型プログラミングの要素をサポート

---

### 高階関数

他の関数を引数として受け取るか、関数を戻り値として返す関数

```python
# 高階関数の例
def apply_operation(x, y, operation):
    """2つの数値に操作を適用する関数"""
    return operation(x, y)

# 各種操作を定義
def add(a, b): return a + b
def subtract(a, b): return a - b
def multiply(a, b): return a * b
def divide(a, b): return a / b if b != 0 else "エラー: ゼロ除算"

# 高階関数の使用
print(apply_operation(10, 5, add))      # 15
print(apply_operation(10, 5, subtract)) # 5
print(apply_operation(10, 5, multiply)) # 50
print(apply_operation(10, 5, divide))   # 2.0
```

---

### map 関数

```python
# map関数: イテラブルの各要素に関数を適用
fish_weights = [5, 10, 15, 20, 25]

# キログラムをグラムに変換
weights_in_grams = map(lambda w: w * 1000, fish_weights)
print(list(weights_in_grams))  # [5000, 10000, 15000, 20000, 25000]

# 複数のイテラブルを使用
fish_names = ["マグロ", "サケ", "タイ", "フグ"]
fish_prices = [3000, 2000, 4000, 8000]

# 魚の名前と価格を組み合わせる
fish_info = map(lambda name, price: f"{name}: {price}円", 
                fish_names, fish_prices)
print(list(fish_info))  # ['マグロ: 3000円', 'サケ: 2000円', 'タイ: 4000円', 'フグ: 8000円']
```

---

### filter 関数

```python
# filter関数: 条件に合う要素だけを抽出
fish_lengths = [15, 25, 10, 30, 20, 35, 5]

# 20cm以上の魚をフィルタリング
big_fish = filter(lambda length: length >= 20, fish_lengths)
print(list(big_fish))  # [25, 30, 20, 35]

# 辞書のリストでのフィルタリング
fish_data = [
    {"name": "マグロ", "price": 3000, "stock": 5},
    {"name": "サケ", "price": 2000, "stock": 10},
    {"name": "タイ", "price": 4000, "stock": 3},
    {"name": "フグ", "price": 8000, "stock": 2},
    {"name": "サバ", "price": 600, "stock": 20}
]

# 高価な魚（3000円以上）をフィルタリング
expensive_fish = filter(lambda fish: fish["price"] >= 3000, fish_data)
for fish in expensive_fish:
    print(f"{fish['name']}: {fish['price']}円")
```

---

### reduce 関数

```python
from functools import reduce

# reduce関数: イテラブルの要素を累積的に処理
fish_weights = [5, 10, 15, 20, 25]

# 合計重量を計算
total_weight = reduce(lambda x, y: x + y, fish_weights)
print(f"合計重量: {total_weight}kg")  # 合計重量: 75kg

# 最大値を見つける
max_weight = reduce(lambda x, y: x if x > y else y, fish_weights)
print(f"最大重量: {max_weight}kg")  # 最大重量: 25kg

# 初期値を指定
total_with_initial = reduce(lambda x, y: x + y, fish_weights, 10)
print(f"初期値付き合計: {total_with_initial}kg")  # 初期値付き合計: 85kg
```

---

### 関数合成

```python
# 関数合成の例
def compose(f, g):
    """2つの関数を合成する関数"""
    return lambda x: f(g(x))

# 個別の関数
def double(x): return x * 2
def increment(x): return x + 1

# 関数の合成
double_then_increment = compose(increment, double)
increment_then_double = compose(double, increment)

# 合成関数の使用
print(double_then_increment(5))  # 11 (5*2 + 1)
print(increment_then_double(5))  # 12 ((5+1) * 2)
```

---

### 部分適用と関数のカリー化

```python
from functools import partial

# 部分適用の例
def multiply(x, y):
    return x * y

# 2倍にする関数を作成
double = partial(multiply, 2)
print(double(5))  # 10

# 3倍にする関数を作成
triple = partial(multiply, 3)
print(triple(5))  # 15

# カリー化の例
def curry_multiply(x):
    def inner(y):
        return x * y
    return inner

# カリー化された関数の使用
double_curry = curry_multiply(2)
triple_curry = curry_multiply(3)

print(double_curry(5))  # 10
print(triple_curry(5))  # 15
```

---

### デコレータ

- 既存の関数を修正せずに機能を拡張する方法
- 関数を引数として受け取り、新しい関数を返す
- `@` 記号を使用して適用

```python
# デコレータの定義
def log_function_call(func):
    """関数の呼び出しをログに記録するデコレータ"""
    def wrapper(*args, **kwargs):
        print(f"関数 {func.__name__} が呼び出されました。引数: {args}, {kwargs}")
        result = func(*args, **kwargs)
        print(f"関数 {func.__name__} が {result} を返しました。")
        return result
    return wrapper

# デコレータの適用
@log_function_call
def add(a, b):
    return a + b

# 関数の呼び出し
add(3, 5)
# 関数 add が呼び出されました。引数: (3, 5), {}
# 関数 add が 8 を返しました。
```

---

### 引数を持つデコレータ

```python
# 引数を持つデコレータの定義
def repeat(n):
    """関数をn回繰り返すデコレータ"""
    def decorator(func):
        def wrapper(*args, **kwargs):
            results = []
            for _ in range(n):
                results.append(func(*args, **kwargs))
            return results
        return wrapper
    return decorator

# デコレータの適用
@repeat(3)
def greet(name):
    return f"こんにちは、{name}さん！"

# 関数の呼び出し
print(greet("マグロ"))
# ['こんにちは、マグロさん！', 'こんにちは、マグロさん！', 'こんにちは、マグロさん！']
```

---

### 複数のデコレータ

```python
# 複数のデコレータの定義
def bold(func):
    def wrapper(*args, **kwargs):
        return f"<b>{func(*args, **kwargs)}</b>"
    return wrapper

def italic(func):
    def wrapper(*args, **kwargs):
        return f"<i>{func(*args, **kwargs)}</i>"
    return wrapper

# 複数のデコレータの適用（下から上に適用される）
@bold
@italic
def format_fish(name):
    return name

# 関数の呼び出し
print(format_fish("マグロ"))  # <b><i>マグロ</i></b>
```

---

## まとめ

---

### 関数とモジュールの重要性

- **コードの再利用性**: 同じコードを複数回書く必要がない
- **モジュール性**: コードを論理的な単位に分割できる
- **可読性**: 適切に名前付けされた関数はコードの理解を助ける
- **保守性**: 機能ごとに分離されたコードは修正が容易
- **テスト容易性**: 独立した関数は単体テストが容易

---

### 学んだこと

- 関数の定義と呼び出し
- 引数の種類（必須、キーワード、デフォルト、可変長）
- スコープとグローバル変数
- 再帰関数とラムダ関数
- モジュールのインポートと作成
- パッケージの構造と使用
- 関数型プログラミングの概念
- 高階関数（map, filter, reduce）
- デコレータの使用

---

### 次のステップ

- 標準ライブラリの探索
- サードパーティのパッケージの使用
- 独自のモジュールとパッケージの作成
- より複雑な関数型プログラミングの技術の習得
- デコレータを使用したコードの拡張

---

## ご質問はありますか？

---

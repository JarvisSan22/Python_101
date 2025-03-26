# セクション3: 関数とモジュール性 - Pythonの構造化プログラミングへの第一歩

![Python関数とモジュール](../../../assets/images/section3_header.jpg)

こんにちは、Pythonプログラミングの旅を続けている皆さん！今回のブログでは、Pythonの強力な機能である「関数」と「モジュール性」について探求していきます。クルミとジャービスが、日本の魚を例に使いながら、コードを整理して再利用可能にする方法を紹介します。

## 関数の基本 - コードの再利用性を高める

<div class="dialogue">
<p class="kurumi">ねえジャービス、私のPythonコードがどんどん長くなってきて、同じような処理を何度も書いているの。もっと効率的な方法はないかな？</p>

<p class="jarvis">それは関数を使うべきタイミングですね、クルミさん。関数は再利用可能なコードブロックで、プログラムを整理するのに最適です。</p>
</div>

関数とは、特定のタスクを実行するためにまとめられたコードのブロックです。一度定義すれば、何度でも呼び出すことができます。これにより、コードの重複を減らし、メンテナンスを容易にします。

### 関数の定義と呼び出し

Pythonでの関数の基本的な構造は次のとおりです：

```python
def 関数名(引数1, 引数2, ...):
    """ドキュメンテーション文字列（docstring）"""
    # 関数の本体
    # 処理を記述
    return 戻り値  # 省略可能
```

<div class="dialogue">
<p class="kurumi">具体的な例があると理解しやすいな。例えば、魚に関する関数を作ってみてよ！</p>

<p class="jarvis">では、マグロの価格を計算する関数を作ってみましょう：</p>
</div>

```python
def calculate_tuna_price(weight, price_per_kg=3000):
    """マグロの価格を計算する関数
    
    引数:
        weight (float): マグロの重さ（kg）
        price_per_kg (int, optional): 1kgあたりの価格。デフォルトは3000円。
        
    戻り値:
        float: 計算された価格
    """
    return weight * price_per_kg

# 関数の呼び出し
tuna_weight = 5.5  # 5.5kgのマグロ
price = calculate_tuna_price(tuna_weight)
print(f"{tuna_weight}kgのマグロの価格: {price}円")

# デフォルト値を上書きして呼び出し
premium_price = calculate_tuna_price(tuna_weight, 5000)
print(f"{tuna_weight}kgの高級マグロの価格: {premium_price}円")
```

<div class="dialogue">
<p class="kurumi">なるほど！関数を使えば、同じ計算を何度も書かなくて済むんだね。でも、引数って何種類かあるって聞いたことがあるよ？</p>

<p class="jarvis">鋭い質問です！Pythonには様々な種類の引数があります。順番に見ていきましょう。</p>
</div>

## 引数の種類 - 柔軟な関数設計

### 位置引数とキーワード引数

```python
def describe_fish(name, weight, length):
    """魚の説明を返す関数"""
    return f"{name}は重さ{weight}kg、長さ{length}cmです。"

# 位置引数（順序が重要）
print(describe_fish("マグロ", 80, 150))

# キーワード引数（順序は関係ない）
print(describe_fish(length=40, name="タイ", weight=3))
```

### デフォルト引数

```python
def describe_fish(name, weight=0, length=0, habitat="不明"):
    """デフォルト値を持つ引数を使用した関数"""
    return f"{name}は重さ{weight}kg、長さ{length}cm、生息地は{habitat}です。"

# 必須引数のみ指定
print(describe_fish("フグ"))

# 一部の引数を指定
print(describe_fish("サケ", 5, habitat="北海道"))
```

<div class="dialogue">
<p class="kurumi">これは便利！でも、引数の数が事前にわからない場合はどうするの？例えば、任意の数の魚の平均体重を計算したいとか。</p>

<p class="jarvis">その場合は、可変長引数を使います。`*args`と`**kwargs`という特殊な構文があります。</p>
</div>

### 可変長引数 (*args と **kwargs)

```python
def fish_average(*weights):
    """任意の数の魚の重さの平均を計算する関数"""
    if not weights:
        return 0
    return sum(weights) / len(weights)

# 異なる数の引数で呼び出し
print(f"平均重量: {fish_average(5, 10, 15)}kg")
print(f"平均重量: {fish_average(3, 8, 12, 15, 20)}kg")

def fish_details(name, **attributes):
    """魚の詳細情報を表示する関数"""
    print(f"魚名: {name}")
    for key, value in attributes.items():
        print(f"  {key}: {value}")

# キーワード可変長引数の使用
fish_details("マグロ", weight=80, length=150, habitat="太平洋", color="赤身")
```

<div class="dialogue">
<p class="kurumi">すごい！これで任意の数の引数を扱えるんだね。ところで、関数の中で定義した変数は、関数の外からアクセスできるの？</p>

<p class="jarvis">良い質問です。それはスコープの概念に関わります。</p>
</div>

## 関数のスコープ - 変数の可視性を理解する

Pythonでは、変数のスコープ（有効範囲）が重要です：

- **ローカルスコープ**: 関数内で定義された変数は、その関数内でのみアクセス可能
- **グローバルスコープ**: 関数の外で定義された変数は、プログラム全体でアクセス可能

```python
fish_count = 0  # グローバル変数

def add_fish():
    fish_type = "マグロ"  # ローカル変数
    global fish_count  # グローバル変数を使用することを宣言
    fish_count += 1
    print(f"{fish_type}を追加しました。現在の数: {fish_count}")

add_fish()
add_fish()
print(f"合計: {fish_count}")
# print(fish_type)  # エラー: fish_typeはローカル変数なので外部からアクセスできない
```

<div class="dialogue">
<p class="kurumi">なるほど！関数内の変数は外からは見えないんだね。でも、関数の中に関数を定義することもできるの？</p>

<p class="jarvis">はい、それをネストした関数と呼びます。非常に強力な機能です。</p>
</div>

## 関数内関数とクロージャ - 高度な関数の使い方

```python
def fish_processor(fish_list):
    """魚のリストを処理する関数"""
    
    def filter_big_fish(fish):
        """大きな魚（50cm以上）をフィルタリングする内部関数"""
        return fish["length"] >= 50
    
    def calculate_price(fish):
        """魚の価格を計算する内部関数"""
        base_price = fish["weight"] * 1000
        if fish["length"] >= 100:
            return base_price * 1.5  # 大型魚は1.5倍の価格
        return base_price
    
    # 大きな魚をフィルタリング
    big_fish = [fish for fish in fish_list if filter_big_fish(fish)]
    
    # 価格を計算して追加
    for fish in big_fish:
        fish["price"] = calculate_price(fish)
    
    return big_fish

# 関数の使用
fishes = [
    {"name": "マグロ", "weight": 80, "length": 150},
    {"name": "サケ", "weight": 5, "length": 75},
    {"name": "タイ", "weight": 3, "length": 40}
]

result = fish_processor(fishes)
for fish in result:
    print(f"{fish['name']}: {fish['price']}円")
```

<div class="dialogue">
<p class="kurumi">関数の中に関数を定義するなんて、すごく柔軟だね！他にも特殊な関数の形はある？</p>

<p class="jarvis">はい、再帰関数とラムダ関数も重要な概念です。</p>
</div>

## 再帰関数とラムダ関数 - 特殊な関数形式

### 再帰関数

再帰関数は自分自身を呼び出す関数です。複雑な問題を小さな問題に分解するのに役立ちます。

```python
def factorial(n):
    """階乗を計算する再帰関数"""
    if n <= 1:
        return 1
    else:
        return n * factorial(n - 1)

print(f"5の階乗: {factorial(5)}")  # 120 (5 * 4 * 3 * 2 * 1)
```

### ラムダ関数（無名関数）

ラムダ関数は、小さな無名関数を作成するための簡潔な方法です。

```python
# 通常の関数
def square(x):
    return x ** 2

# 同等のラムダ関数
square_lambda = lambda x: x ** 2

print(f"square(5) = {square(5)}")
print(f"square_lambda(5) = {square_lambda(5)}")

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

<div class="dialogue">
<p class="kurumi">ラムダ関数はコンパクトで便利そう！でも、コードが長くなってきたら、どうやって整理するの？</p>

<p class="jarvis">それがモジュールの出番です。関連する関数をファイルにまとめて、再利用可能なライブラリを作成できます。</p>
</div>

## モジュールとパッケージ - コードの整理と再利用

### モジュールのインポート

Pythonでは、標準ライブラリやサードパーティのライブラリからモジュールをインポートして使用できます。

```python
# モジュール全体をインポート
import math

# モジュールの関数を使用
radius = 5
area = math.pi * math.pow(radius, 2)
print(f"円の面積: {area}")

# 特定の関数やオブジェクトをインポート
from random import choice, randint

# 直接使用（モジュール名なしで）
fish_types = ["マグロ", "サケ", "タイ", "フグ", "サバ"]
print(f"ランダムな魚: {choice(fish_types)}")
print(f"1から10の乱数: {randint(1, 10)}")
```

### 自作モジュールの作成

関連する関数をファイルにまとめて、独自のモジュールを作成できます。

```python
# fish_utils.py
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

```python
# main.py
# 自作モジュールのインポート
import fish_utils

# モジュールの使用
price = fish_utils.calculate_fish_price(5, 2000)
print(f"魚の価格: {price}円")

tuna = fish_utils.Fish("マグロ", 80, 150)
print(tuna.describe())
```

<div class="dialogue">
<p class="kurumi">モジュールを使えば、コードを整理できるんだね！でも、もっと大きなプロジェクトではどうするの？</p>

<p class="jarvis">その場合は、パッケージを使います。パッケージは複数のモジュールを階層的に整理したものです。</p>
</div>

### パッケージの構造

```
fish_package/
│
├── __init__.py
├── freshwater.py
├── saltwater.py
└── utils.py
```

<div class="dialogue">
<p class="kurumi">Pythonには標準ライブラリのモジュールもたくさんあるよね？よく使うものを教えて！</p>

<p class="jarvis">はい、Pythonには多数の便利な標準ライブラリがあります。いくつか紹介しましょう。</p>
</div>

## 標準ライブラリのモジュール - Pythonの宝庫

### math モジュール

```python
import math

print(f"円周率: {math.pi}")
print(f"2の平方根: {math.sqrt(2)}")
print(f"3の3乗: {math.pow(3, 3)}")
```

### random モジュール

```python
import random

print(f"0から1の乱数: {random.random()}")
print(f"1から10の整数乱数: {random.randint(1, 10)}")

fish_types = ["マグロ", "サケ", "タイ", "フグ", "サバ"]
print(f"ランダムな魚: {random.choice(fish_types)}")
print(f"ランダムな3種類の魚: {random.sample(fish_types, 3)}")
```

### datetime モジュール

```python
from datetime import datetime, timedelta

now = datetime.now()
print(f"現在の日時: {now}")

fishing_date = now + timedelta(days=3)
print(f"3日後の釣り日: {fishing_date}")
```

<div class="dialogue">
<p class="kurumi">標準ライブラリってすごく便利だね！ところで、関数型プログラミングについても聞いたことがあるけど、それって何？</p>

<p class="jarvis">関数型プログラミングは、関数を第一級オブジェクトとして扱うプログラミングパラダイムです。Pythonはその要素をサポートしています。</p>
</div>

## 関数型プログラミング - 新しいパラダイム

### 高階関数 (map, filter, reduce)

```python
# map: イテラブルの各要素に関数を適用
fish_weights = [5, 10, 15, 20, 25]
weights_in_grams = list(map(lambda w: w * 1000, fish_weights))
print(f"グラム単位の重さ: {weights_in_grams}")

# filter: 条件に合う要素だけを抽出
big_fish = list(filter(lambda w: w >= 15, fish_weights))
print(f"大きな魚の重さ: {big_fish}")

# reduce: イテラブルの要素を累積的に処理
from functools import reduce
total_weight = reduce(lambda x, y: x + y, fish_weights)
print(f"合計重量: {total_weight}kg")
```

### デコレータ - 関数を拡張する

デコレータは、既存の関数を修正せずに機能を拡張する方法です。

```python
def log_function_call(func):
    """関数の呼び出しをログに記録するデコレータ"""
    def wrapper(*args, **kwargs):
        print(f"関数 {func.__name__} が呼び出されました。引数: {args}, {kwargs}")
        result = func(*args, **kwargs)
        print(f"関数 {func.__name__} が {result} を返しました。")
        return result
    return wrapper

@log_function_call
def add(a, b):
    return a + b

# 関数の呼び出し
add(3, 5)
```

<div class="dialogue">
<p class="kurumi">デコレータって魔法みたい！関数を別の関数で包んで機能を追加できるんだね。</p>

<p class="jarvis">その通りです。Pythonの関数とモジュール性の概念を理解すると、コードの構造化と再利用性が大幅に向上します。</p>

<p class="kurumi">今日はたくさん学んだよ！関数を使って、もっと効率的なコードが書けそう。</p>

<p class="jarvis">素晴らしいです。次回は、オブジェクト指向プログラミングについて学びましょう。それでは、実践的な例で締めくくりましょう。</p>
</div>

## 実践例: 魚の在庫管理システム

以下は、これまで学んだ概念を使用した簡単な魚の在庫管理システムの例です：

```python
# 魚の在庫管理システム

# グローバル変数
inventory = {
    "マグロ": {"price": 3000, "stock": 5},
    "サケ": {"price": 2000, "stock": 10},
    "タイ": {"price": 4000, "stock": 3}
}

# デコレータ: 関数の実行時間を計測
def measure_time(func):
    import time
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"関数 {func.__name__} の実行時間: {end_time - start_time:.6f}秒")
        return result
    return wrapper

# 在庫を表示する関数
@measure_time
def display_inventory():
    """在庫を表示する関数"""
    print("\n在庫情報:")
    print("-" * 30)
    for fish_name, info in inventory.items():
        print(f"{fish_name}: {info['price']}円 (在庫: {info['stock']}個)")

# 魚を購入する関数
def buy_fish(fish_name, quantity):
    """魚を購入する関数"""
    if fish_name not in inventory:
        return f"申し訳ありません。{fish_name}は取り扱っていません。"
    
    fish = inventory[fish_name]
    
    if fish["stock"] < quantity:
        return f"申し訳ありません。{fish_name}の在庫が足りません。現在の在庫: {fish['stock']}個"
    
    # 在庫を減らす
    fish["stock"] -= quantity
    
    # 合計金額を計算
    total_price = fish["price"] * quantity
    
    return f"{fish_name}を{quantity}個購入しました。合計: {total_price}円"

# 高階関数: 条件に基づいて魚をフィルタリングする関数
def filter_fish(condition):
    """条件に基づいて魚をフィルタリングする関数"""
    return {name: info for name, info in inventory.items() if condition(info)}

# 在庫が少ない魚を見つける関数
def find_low_stock(threshold=5):
    """在庫が少ない魚を見つける関数"""
    low_stock = filter_fish(lambda info: info["stock"] < threshold)
    
    print(f"\n在庫が{threshold}個未満の魚:")
    if low_stock:
        for name, info in low_stock.items():
            print(f"{name}: {info['stock']}個")
    else:
        print("該当する魚はありません。")

# シミュレーションの実行
display_inventory()
find_low_stock()
print(buy_fish("マグロ", 2))
print(buy_fish("サケ", 5))
display_inventory()
```

## まとめ

この記事では、Pythonの関数とモジュール性について学びました：

- 関数の定義と呼び出し
- 様々な種類の引数（位置引数、キーワード引数、デフォルト引数、可変長引数）
- 関数のスコープとグローバル変数
- 関数内関数とクロージャ
- 再帰関数とラムダ関数
- モジュールとパッケージの使用
- 標準ライブラリの活用
- 関数型プログラミングの概念（高階関数、map/filter/reduce、デコレータ）

これらの概念を理解し、適切に使用することで、より整理された、再利用可能なコードを書くことができます。次回は、オブジェクト指向プログラミングについて探求していきます。お楽しみに！

---

次のセクションでは、オブジェクト指向プログラミングの基本概念とPythonでのクラスの使い方について学びます。クルミとジャービスが、日本の魚を例にしながら、オブジェクト指向の世界へ案内します。

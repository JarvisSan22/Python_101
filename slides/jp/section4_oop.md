# セクション4: オブジェクト指向プログラミング - スライド

## オブジェクト指向プログラミング

---

### オブジェクト指向プログラミングとは？

- データと機能（メソッド）を一つの単位（オブジェクト）にまとめるプログラミングパラダイム
- 現実世界のものをモデル化するのに適している
- コードの再利用性、保守性、拡張性を高める
- Pythonはオブジェクト指向言語の一つ

---

### オブジェクト指向の基本概念

- **クラス**: オブジェクトの設計図
- **オブジェクト**: クラスのインスタンス
- **属性**: オブジェクトが持つデータ
- **メソッド**: オブジェクトが持つ機能（関数）
- **継承**: 既存のクラスから新しいクラスを作成する仕組み
- **カプセル化**: データと機能を一つの単位に隠蔽する
- **ポリモーフィズム**: 同じインターフェースで異なる実装を提供する

---

### クラスとオブジェクト

```python
# クラスの定義
class Fish:
    # クラス変数（すべてのインスタンスで共有）
    species_count = 0
    
    # 初期化メソッド（コンストラクタ）
    def __init__(self, name, species, weight):
        # インスタンス変数（各インスタンス固有）
        self.name = name
        self.species = species
        self.weight = weight
        Fish.species_count += 1
    
    # インスタンスメソッド
    def swim(self):
        return f"{self.name}が泳いでいます。"
    
    def describe(self):
        return f"{self.name}は{self.species}で、重さは{self.weight}kgです。"

# オブジェクト（インスタンス）の作成
tuna = Fish("マグロ", "マグロ科", 80)
salmon = Fish("サケ", "サケ科", 5)

# メソッドの呼び出し
print(tuna.swim())
print(salmon.describe())

# クラス変数へのアクセス
print(f"魚の種類数: {Fish.species_count}")
```

---

### self パラメータ

- `self` はインスタンス自身を参照する
- インスタンスメソッドの最初のパラメータとして必須
- メソッド呼び出し時には明示的に渡す必要はない
- 慣習的に `self` という名前を使用するが、技術的には他の名前も可能

```python
class Fish:
    def __init__(self, name):
        self.name = name
    
    def swim(self):  # selfは必須
        return f"{self.name}が泳いでいます。"

tuna = Fish("マグロ")
print(tuna.swim())  # selfは自動的に渡される
```

---

### コンストラクタとデストラクタ

```python
class Fish:
    def __init__(self, name):
        """コンストラクタ: オブジェクト作成時に呼ばれる"""
        print(f"{name}オブジェクトを作成中...")
        self.name = name
    
    def __del__(self):
        """デストラクタ: オブジェクト破棄時に呼ばれる"""
        print(f"{self.name}オブジェクトを破棄中...")

# オブジェクトの作成
tuna = Fish("マグロ")

# オブジェクトの破棄
del tuna
```

---

### クラス変数とインスタンス変数

```python
class Fish:
    # クラス変数（すべてのインスタンスで共有）
    water_type = "海水"
    count = 0
    
    def __init__(self, name):
        # インスタンス変数（各インスタンス固有）
        self.name = name
        Fish.count += 1

# オブジェクトの作成
tuna = Fish("マグロ")
salmon = Fish("サケ")

# クラス変数へのアクセス
print(f"水の種類: {Fish.water_type}")
print(f"魚の数: {Fish.count}")

# インスタンス変数へのアクセス
print(f"名前: {tuna.name}")
print(f"名前: {salmon.name}")

# クラス変数の変更
Fish.water_type = "淡水"
print(f"新しい水の種類: {tuna.water_type}")  # すべてのインスタンスに影響
print(f"新しい水の種類: {salmon.water_type}")
```

---

### インスタンスメソッドとクラスメソッド

```python
class Fish:
    count = 0
    
    def __init__(self, name):
        self.name = name
        Fish.count += 1
    
    # インスタンスメソッド
    def swim(self):
        return f"{self.name}が泳いでいます。"
    
    # クラスメソッド
    @classmethod
    def get_count(cls):
        return f"現在の魚の数: {cls.count}"
    
    # スタティックメソッド
    @staticmethod
    def is_water_safe(temperature):
        return 5 <= temperature <= 30

# オブジェクトの作成
tuna = Fish("マグロ")
salmon = Fish("サケ")

# インスタンスメソッドの呼び出し
print(tuna.swim())

# クラスメソッドの呼び出し
print(Fish.get_count())

# スタティックメソッドの呼び出し
print(f"水は安全か: {Fish.is_water_safe(25)}")
```

---

### プロパティ

```python
class Fish:
    def __init__(self, name, weight):
        self.name = name
        self._weight = weight  # プライベート属性
    
    # ゲッター
    @property
    def weight(self):
        return self._weight
    
    # セッター
    @weight.setter
    def weight(self, value):
        if value <= 0:
            raise ValueError("重さは正の値でなければなりません")
        self._weight = value
    
    # デリーター
    @weight.deleter
    def weight(self):
        print(f"{self.name}の重さを削除します")
        del self._weight

# オブジェクトの作成
tuna = Fish("マグロ", 80)

# プロパティの使用
print(f"現在の重さ: {tuna.weight}kg")  # ゲッター

tuna.weight = 100  # セッター
print(f"新しい重さ: {tuna.weight}kg")

try:
    tuna.weight = -10  # 不正な値
except ValueError as e:
    print(f"エラー: {e}")

del tuna.weight  # デリーター
```

---

### 特殊メソッド（マジックメソッド）

```python
class Fish:
    def __init__(self, name, weight):
        self.name = name
        self.weight = weight
    
    # 文字列表現
    def __str__(self):
        return f"{self.name} ({self.weight}kg)"
    
    # デバッグ用の表現
    def __repr__(self):
        return f"Fish('{self.name}', {self.weight})"
    
    # 比較演算子
    def __eq__(self, other):
        if not isinstance(other, Fish):
            return False
        return self.name == other.name and self.weight == other.weight
    
    def __lt__(self, other):
        if not isinstance(other, Fish):
            return NotImplemented
        return self.weight < other.weight
    
    # 算術演算子
    def __add__(self, other):
        if isinstance(other, Fish):
            return Fish(f"{self.name}+{other.name}", self.weight + other.weight)
        return NotImplemented

# オブジェクトの作成
tuna = Fish("マグロ", 80)
salmon = Fish("サケ", 5)

# 特殊メソッドの使用
print(str(tuna))  # __str__
print(repr(tuna))  # __repr__

print(tuna == salmon)  # __eq__
print(tuna < salmon)  # __lt__

combined = tuna + salmon  # __add__
print(combined)
```

---

### 継承

```python
# 基底クラス（親クラス）
class Fish:
    def __init__(self, name, weight):
        self.name = name
        self.weight = weight
    
    def swim(self):
        return f"{self.name}が泳いでいます。"
    
    def describe(self):
        return f"{self.name}の重さは{self.weight}kgです。"

# 派生クラス（子クラス）
class Tuna(Fish):
    def __init__(self, name, weight, speed):
        # 親クラスの初期化
        super().__init__(name, weight)
        self.speed = speed
    
    # メソッドのオーバーライド
    def swim(self):
        return f"{self.name}が時速{self.speed}kmで高速に泳いでいます。"
    
    # 新しいメソッド
    def hunt(self):
        return f"{self.name}が獲物を追いかけています。"

# オブジェクトの作成
normal_fish = Fish("一般的な魚", 1)
tuna = Tuna("マグロ", 80, 70)

# メソッドの呼び出し
print(normal_fish.swim())
print(tuna.swim())  # オーバーライドされたメソッド
print(tuna.describe())  # 親クラスから継承したメソッド
print(tuna.hunt())  # 子クラス固有のメソッド
```

---

### 多重継承

```python
# 基底クラス1
class Swimmer:
    def swim(self):
        return "泳ぐことができます。"
    
    def float(self):
        return "水に浮くことができます。"

# 基底クラス2
class Predator:
    def hunt(self):
        return "獲物を捕まえることができます。"
    
    def eat(self):
        return "肉を食べることができます。"

# 多重継承
class Shark(Swimmer, Predator):
    def __init__(self, name):
        self.name = name
    
    def describe(self):
        return f"{self.name}はサメです。"

# オブジェクトの作成
shark = Shark("ホホジロザメ")

# メソッドの呼び出し
print(shark.describe())
print(shark.swim())  # Swimmerから継承
print(shark.hunt())  # Predatorから継承
```

---

### メソッド解決順序（MRO）

```python
class A:
    def method(self):
        return "A"

class B(A):
    def method(self):
        return "B"

class C(A):
    def method(self):
        return "C"

class D(B, C):
    pass

# メソッド解決順序の確認
print(D.__mro__)

# メソッドの呼び出し
d = D()
print(d.method())  # "B"（左から右への深さ優先探索）
```

---

### 抽象基底クラス

```python
from abc import ABC, abstractmethod

# 抽象基底クラス
class Animal(ABC):
    @abstractmethod
    def make_sound(self):
        pass
    
    @abstractmethod
    def move(self):
        pass
    
    def sleep(self):
        return "Zzz..."

# 具象クラス
class Fish(Animal):
    def make_sound(self):
        return "..."  # 魚は音を出さない
    
    def move(self):
        return "泳ぐ"
    
    def swim(self):
        return "水中を泳ぐ"

# 抽象クラスのインスタンス化はできない
# animal = Animal()  # エラー

# 具象クラスのインスタンス化
fish = Fish()
print(fish.make_sound())
print(fish.move())
print(fish.sleep())
```

---

### カプセル化

```python
class Fish:
    def __init__(self, name, weight):
        self.name = name  # パブリック属性
        self._weight = weight  # プロテクテッド属性（慣習的）
        self.__species = "不明"  # プライベート属性
    
    def get_species(self):
        return self.__species
    
    def set_species(self, species):
        self.__species = species
    
    def _internal_method(self):
        return "これは内部メソッドです。"
    
    def __private_method(self):
        return "これはプライベートメソッドです。"
    
    def public_method(self):
        return self.__private_method()

# オブジェクトの作成
tuna = Fish("マグロ", 80)

# 属性へのアクセス
print(tuna.name)  # パブリック属性
print(tuna._weight)  # プロテクテッド属性（アクセス可能だが推奨されない）
# print(tuna.__species)  # エラー: プライベート属性には直接アクセスできない

# 名前修飾によるアクセス
print(tuna._Fish__species)  # 名前修飾によるプライベート属性へのアクセス

# メソッドの呼び出し
print(tuna.get_species())
tuna.set_species("マグロ科")
print(tuna.get_species())
print(tuna.public_method())
```

---

### ポリモーフィズム

```python
# 基底クラス
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        pass

# 派生クラス1
class Dog(Animal):
    def speak(self):
        return f"{self.name}が「ワン！」と吠えました。"

# 派生クラス2
class Cat(Animal):
    def speak(self):
        return f"{self.name}が「ニャー！」と鳴きました。"

# 派生クラス3
class Fish(Animal):
    def speak(self):
        return f"{self.name}が「...」と沈黙しています。"

# ポリモーフィズムの例
def animal_sound(animal):
    return animal.speak()

# オブジェクトの作成
dog = Dog("ポチ")
cat = Cat("タマ")
fish = Fish("マグロ")

# 同じインターフェースで異なる実装
print(animal_sound(dog))
print(animal_sound(cat))
print(animal_sound(fish))
```

---

### ダックタイピング

```python
class Duck:
    def swim(self):
        return "アヒルが泳いでいます。"
    
    def quack(self):
        return "ガーガー！"

class Fish:
    def swim(self):
        return "魚が泳いでいます。"
    
    def quack(self):
        return "..."

def make_it_swim_and_quack(animal):
    print(animal.swim())
    print(animal.quack())

# オブジェクトの作成
duck = Duck()
fish = Fish()

# ダックタイピング: クラスではなくメソッドの存在で判断
make_it_swim_and_quack(duck)
make_it_swim_and_quack(fish)
```

---

### コンポジション

```python
# コンポジション: 「持つ」関係
class Engine:
    def __init__(self, power):
        self.power = power
    
    def start(self):
        return f"{self.power}馬力のエンジンが始動しました。"

class Boat:
    def __init__(self, name, engine_power):
        self.name = name
        self.engine = Engine(engine_power)  # コンポジション
    
    def start_engine(self):
        return f"{self.name}: {self.engine.start()}"

# オブジェクトの作成
fishing_boat = Boat("漁船", 200)

# メソッドの呼び出し
print(fishing_boat.start_engine())
```

---

### 集約

```python
# 集約: 「使う」関係
class FishingRod:
    def __init__(self, length):
        self.length = length
    
    def cast(self):
        return f"{self.length}mの釣り竿を投げました。"

class Fisherman:
    def __init__(self, name):
        self.name = name
        self.rod = None  # 初期状態では釣り竿を持っていない
    
    def set_rod(self, rod):
        self.rod = rod  # 集約
    
    def fish(self):
        if self.rod:
            return f"{self.name}: {self.rod.cast()}"
        else:
            return f"{self.name}は釣り竿を持っていません。"

# オブジェクトの作成
rod = FishingRod(3)
fisherman = Fisherman("太郎")

# 集約関係の確立
fisherman.set_rod(rod)

# メソッドの呼び出し
print(fisherman.fish())
```

---

### 例外処理

```python
class FishTankError(Exception):
    """水槽に関するエラーの基底クラス"""
    pass

class WaterLevelError(FishTankError):
    """水位に関するエラー"""
    pass

class TemperatureError(FishTankError):
    """水温に関するエラー"""
    pass

class FishTank:
    def __init__(self, name):
        self.name = name
        self.water_level = 100  # パーセント
        self.temperature = 25  # 摂氏
    
    def check_water_level(self):
        if self.water_level < 20:
            raise WaterLevelError(f"{self.name}の水位が危険です: {self.water_level}%")
    
    def check_temperature(self):
        if self.temperature < 20 or self.temperature > 30:
            raise TemperatureError(f"{self.name}の水温が適切ではありません: {self.temperature}℃")
    
    def status(self):
        try:
            self.check_water_level()
            self.check_temperature()
            return f"{self.name}の状態は正常です。"
        except FishTankError as e:
            return f"警告: {e}"

# オブジェクトの作成
tank = FishTank("メイン水槽")

# 正常な状態
print(tank.status())

# 水位を下げる
tank.water_level = 10
print(tank.status())

# 水位を戻して水温を変える
tank.water_level = 100
tank.temperature = 35
print(tank.status())
```

---

### コンテキストマネージャ

```python
class FishTank:
    def __init__(self, name):
        self.name = name
        print(f"{self.name}を準備中...")
    
    def __enter__(self):
        print(f"{self.name}に水を入れています...")
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        print(f"{self.name}の水を抜いています...")
        if exc_type:
            print(f"エラーが発生しました: {exc_val}")
            return True  # 例外を処理
    
    def add_fish(self, fish_name):
        print(f"{fish_name}を{self.name}に追加しました。")

# コンテキストマネージャとして使用
with FishTank("小型水槽") as tank:
    tank.add_fish("グッピー")
    tank.add_fish("ネオンテトラ")
    # エラーを発生させる
    # raise ValueError("何か問題が発生しました")

print("プログラムを続行します。")
```

---

### デスクリプタ

```python
class PositiveNumber:
    def __init__(self, name):
        self.name = name
    
    def __get__(self, instance, owner):
        if instance is None:
            return self
        return instance.__dict__.get(self.name, 0)
    
    def __set__(self, instance, value):
        if value <= 0:
            raise ValueError(f"{self.name}は正の値でなければなりません")
        instance.__dict__[self.name] = value

class Fish:
    weight = PositiveNumber("weight")
    length = PositiveNumber("length")
    
    def __init__(self, name, weight, length):
        self.name = name
        self.weight = weight
        self.length = length
    
    def __str__(self):
        return f"{self.name}: 重さ{self.weight}kg, 長さ{self.length}cm"

# オブジェクトの作成
try:
    tuna = Fish("マグロ", 80, 150)
    print(tuna)
    
    # 不正な値を設定
    tuna.weight = -10  # エラー
except ValueError as e:
    print(f"エラー: {e}")
```

---

### メタクラス

```python
# メタクラス
class FishMeta(type):
    def __new__(mcs, name, bases, attrs):
        # クラス名を大文字に変換
        attrs["CLASS_NAME"] = name.upper()
        
        # すべてのメソッドをログ出力するようにラップ
        for attr_name, attr_value in attrs.items():
            if callable(attr_value) and not attr_name.startswith("__"):
                attrs[attr_name] = mcs.log_method(attr_value)
        
        return super().__new__(mcs, name, bases, attrs)
    
    @staticmethod
    def log_method(method):
        def wrapper(*args, **kwargs):
            print(f"メソッド {method.__name__} が呼び出されました")
            return method(*args, **kwargs)
        return wrapper

# メタクラスを使用したクラス
class Tuna(metaclass=FishMeta):
    def swim(self):
        return "マグロが泳いでいます"
    
    def hunt(self):
        return "マグロが狩りをしています"

# オブジェクトの作成
tuna = Tuna()

# メソッドの呼び出し
print(tuna.swim())
print(tuna.hunt())
print(f"クラス名: {Tuna.CLASS_NAME}")
```

---

### データクラス（Python 3.7以降）

```python
from dataclasses import dataclass, field

@dataclass
class Fish:
    name: str
    species: str
    weight: float
    length: float
    tags: list = field(default_factory=list)
    
    def swim(self):
        return f"{self.name}が泳いでいます。"
    
    def __post_init__(self):
        self.size_category = "大型" if self.length >= 100 else "中型" if self.length >= 50 else "小型"

# オブジェクトの作成
tuna = Fish("マグロ", "マグロ科", 80, 150, ["回遊魚", "食用"])
salmon = Fish("サケ", "サケ科", 5, 75)

# 属性へのアクセス
print(tuna)
print(salmon)
print(f"マグロのサイズカテゴリ: {tuna.size_category}")
print(f"サケのサイズカテゴリ: {salmon.size_category}")
```

---

### 名前空間とスコープ

```python
# グローバル名前空間
fish_type = "マグロ"

class Aquarium:
    # クラス名前空間
    fish_type = "熱帯魚"
    
    def __init__(self, name):
        # インスタンス名前空間
        self.name = name
        self.fish_type = "金魚"
    
    def show_fish_types(self):
        # ローカル名前空間
        fish_type = "錦鯉"
        print(f"ローカル: {fish_type}")
        print(f"インスタンス: {self.fish_type}")
        print(f"クラス: {Aquarium.fish_type}")
        print(f"グローバル: {globals()['fish_type']}")

# オブジェクトの作成
aquarium = Aquarium("ホーム水槽")

# メソッドの呼び出し
aquarium.show_fish_types()
```

---

### オブジェクト指向設計の原則

- **S**ingle Responsibility Principle（単一責任の原則）
  - 1つのクラスは1つの責任のみを持つべき

- **O**pen/Closed Principle（開放/閉鎖の原則）
  - 拡張に対して開かれ、修正に対して閉じられているべき

- **L**iskov Substitution Principle（リスコフの置換原則）
  - サブクラスはその基底クラスと置換可能であるべき

- **I**nterface Segregation Principle（インターフェース分離の原則）
  - クライアントは使用しないインターフェースに依存すべきでない

- **D**ependency Inversion Principle（依存性逆転の原則）
  - 上位モジュールは下位モジュールに依存すべきでない

---

### オブジェクト指向プログラミングの利点

- **モジュール性**: コードを論理的な単位に分割
- **再利用性**: 既存のクラスを拡張して新しいクラスを作成
- **保守性**: カプセル化により実装の詳細を隠蔽
- **拡張性**: 新しい機能を追加しやすい
- **データの安全性**: カプセル化によりデータの整合性を保護
- **現実世界のモデリング**: 現実のオブジェクトを自然にモデル化

---

### オブジェクト指向プログラミ<response clipped><NOTE>To save on context only part of this file has been shown to you. You should retry this tool after you have searched inside the file with `grep -n` in order to find the line numbers of what you are looking for.</NOTE>
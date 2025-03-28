# セクション4: オブジェクト指向プログラミング - 宿題

## 理論問題

1. **オブジェクト指向プログラミングの主な特徴を4つ挙げ、それぞれについて簡単に説明してください。**

2. **クラスとオブジェクトの違いを説明してください。**

3. **以下のコードの問題点を指摘し、修正してください。**
   ```python
   class Fish:
       def __init__(name, weight):
           self.name = name
           self.weight = weight
       
       def swim():
           return f"{self.name}が泳いでいます。"
   ```

4. **クラス変数とインスタンス変数の違いを説明し、それぞれの例を示してください。**

5. **以下のコードの出力を予測してください。**
   ```python
   class Fish:
       water_type = "海水"
       
       def __init__(self, name):
           self.name = name
   
   tuna = Fish("マグロ")
   salmon = Fish("サケ")
   
   print(Fish.water_type)
   print(tuna.water_type)
   
   tuna.water_type = "深海"
   
   print(Fish.water_type)
   print(tuna.water_type)
   print(salmon.water_type)
   ```

6. **継承とは何ですか？継承を使用する利点を説明してください。**

7. **多重継承とは何ですか？多重継承を使用する際の潜在的な問題点を説明してください。**

8. **ポリモーフィズムの概念を説明し、Pythonでの例を示してください。**

9. **カプセル化とは何ですか？Pythonでカプセル化を実現する方法を説明してください。**

10. **抽象基底クラスとは何ですか？Pythonで抽象基底クラスを作成する方法を説明してください。**

## 実践問題

### 問題1: 基本的なクラスの作成
日本の魚を表す `Fish` クラスを作成してください。このクラスは以下の属性を持ちます：
- 名前（name）
- 種類（species）
- 重さ（weight）- キログラム単位
- 長さ（length）- センチメートル単位

また、以下のメソッドを実装してください：
- `swim()` - 魚が泳ぐことを表すメッセージを返す
- `describe()` - 魚の詳細情報を返す

```python
# ここにコードを書いてください
```

### 問題2: 特殊メソッドの実装
問題1で作成した `Fish` クラスに以下の特殊メソッドを追加してください：
- `__str__` - 魚の名前と種類を返す
- `__repr__` - クラスの再作成に使用できる文字列を返す
- `__eq__` - 2つの魚オブジェクトが同じ名前と種類を持つ場合に `True` を返す
- `__lt__` - 魚の重さに基づいて比較する

```python
# ここにコードを書いてください
```

### 問題3: プロパティの使用
問題2のクラスを拡張して、重さと長さの属性をプロパティとして実装してください。これらの属性は常に正の値でなければなりません。

```python
# ここにコードを書いてください
```

### 問題4: 継承
`Fish` クラスを継承して、以下の特殊な魚のクラスを作成してください：
- `Tuna`（マグロ）- 追加の属性として `speed`（速度）を持ち、`swim()` メソッドをオーバーライドして速度情報を含める
- `Salmon`（サケ）- 追加の属性として `river_name`（川の名前）を持ち、新しいメソッド `migrate()` を追加する

```python
# ここにコードを書いてください
```

### 問題5: 多重継承
以下の2つの基底クラスを作成してください：
- `Swimmer` - `swim()` メソッドを持つ
- `Jumper` - `jump()` メソッドを持つ

次に、これらの両方のクラスを継承する `FlyingFish`（トビウオ）クラスを作成してください。

```python
# ここにコードを書いてください
```

### 問題6: 抽象基底クラス
`Animal` という抽象基底クラスを作成してください。このクラスは以下の抽象メソッドを持ちます：
- `move()`
- `make_sound()`

次に、この抽象クラスを継承する `Fish`、`Bird`、`Mammal` クラスを作成してください。

```python
# ここにコードを書いてください
```

### 問題7: カプセル化
魚の水槽を表す `Aquarium` クラスを作成してください。このクラスは以下の機能を持ちます：
- プライベート属性として魚のリスト（`__fish_list`）を持つ
- 魚を追加するメソッド（`add_fish()`）
- 魚を削除するメソッド（`remove_fish()`）
- 水槽内のすべての魚を表示するメソッド（`display_fish()`）
- 水槽内の魚の総重量を計算するメソッド（`total_weight()`）

```python
# ここにコードを書いてください
```

### 問題8: ポリモーフィズム
以下の基底クラスを作成してください：
```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        pass
```

次に、この基底クラスを継承する `Dog`、`Cat`、`Fish` クラスを作成し、それぞれに適切な `speak()` メソッドを実装してください。最後に、これらのクラスのインスタンスのリストを作成し、ポリモーフィズムを示すコードを書いてください。

```python
# ここにコードを書いてください
```

### 問題9: データクラス
`dataclasses` モジュールを使用して、魚の情報を格納するデータクラス `FishData` を作成してください。このクラスは以下の属性を持ちます：
- 名前（name）
- 種類（species）
- 重さ（weight）
- 長さ（length）
- タグのリスト（tags）- デフォルトは空リスト

また、`__post_init__` メソッドを実装して、魚のサイズカテゴリ（小型、中型、大型）を自動的に設定してください。

```python
# ここにコードを書いてください
```

### 問題10: 総合問題 - 魚市場システム
魚市場システムを実装してください。このシステムは以下のクラスを含みます：

1. `Product`（抽象基底クラス）
   - 抽象メソッド: `get_price()`, `display_info()`

2. `Fish`（`Product` を継承）
   - 属性: 名前、種類、重さ、価格/kg
   - メソッド: `get_price()`, `display_info()`

3. `PremiumFish`（`Fish` を継承）
   - 追加の属性: 品質グレード（A+, A, B, C）
   - オーバーライドされたメソッド: `get_price()` - グレードに基づいて価格を調整

4. `Market`
   - 属性: 名前、製品リスト
   - メソッド: 製品の追加/削除、在庫の表示、総価値の計算

システムを実装し、いくつかの魚を作成して市場に追加し、在庫を表示してください。

```python
# ここにコードを書いてください
```

## 提出方法

1. すべての問題の解答を1つのPythonファイル（`section4_homework_solutions.py`）にまとめてください。
2. 理論問題の解答はコメントとして含めてください。
3. 各実践問題の解答の前に、問題番号と簡単な説明をコメントとして追加してください。
4. ファイルを提出する前に、すべてのコードが正しく動作することを確認してください。

## 評価基準

- 正確性: すべての問題が正しく解かれているか
- コードの品質: コードが読みやすく、効率的で、適切にコメントされているか
- オブジェクト指向の原則: クラス、継承、カプセル化などの概念が適切に適用されているか
- 創造性: 特に総合問題での解決策の独創性と完成度

頑張ってください！

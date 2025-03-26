# セクション2: データ構造 - スライド

## Python のデータ構造

---

### データ構造とは？

- データを効率的に格納・操作するための方法
- 異なるタイプのデータを整理する仕組み
- 適切なデータ構造の選択が効率的なプログラミングの鍵
- Python には強力な組み込みデータ構造がある

---

## リスト (Lists)

---

### リストの基本

- 順序付けられた変更可能なデータのコレクション
- 異なる型のデータを格納可能
- 角括弧 `[]` で作成
- インデックスは 0 から始まる

```python
# リストの作成
fish_types = ["マグロ", "サケ", "タイ", "フグ"]
mixed_list = ["コイ", 3, 25.5, True]

# インデックスによるアクセス
print(fish_types[0])  # "マグロ"
print(fish_types[-1])  # "フグ"
```

---

### リストの操作

```python
fish_types = ["マグロ", "サケ", "タイ", "フグ"]

# リストの長さ
print(len(fish_types))  # 4

# リストの結合
more_fish = ["サバ", "イワシ"]
all_fish = fish_types + more_fish
print(all_fish)  # ["マグロ", "サケ", "タイ", "フグ", "サバ", "イワシ"]

# リストの繰り返し
repeated = ["コイ"] * 3
print(repeated)  # ["コイ", "コイ", "コイ"]
```

---

### リストのスライス

```python
fish_types = ["マグロ", "サケ", "タイ", "フグ", "サバ", "イワシ"]

# スライス [開始:終了:ステップ]
print(fish_types[1:4])    # ["サケ", "タイ", "フグ"]
print(fish_types[:3])     # ["マグロ", "サケ", "タイ"]
print(fish_types[3:])     # ["フグ", "サバ", "イワシ"]
print(fish_types[::2])    # ["マグロ", "タイ", "サバ"]
print(fish_types[::-1])   # ["イワシ", "サバ", "フグ", "タイ", "サケ", "マグロ"]
```

---

### リストの変更

```python
fish_types = ["マグロ", "サケ", "タイ", "フグ"]

# 要素の変更
fish_types[1] = "カツオ"
print(fish_types)  # ["マグロ", "カツオ", "タイ", "フグ"]

# 要素の追加
fish_types.append("サバ")
print(fish_types)  # ["マグロ", "カツオ", "タイ", "フグ", "サバ"]

# 特定の位置に挿入
fish_types.insert(2, "イワシ")
print(fish_types)  # ["マグロ", "カツオ", "イワシ", "タイ", "フグ", "サバ"]
```

---

### リストからの削除

```python
fish_types = ["マグロ", "サケ", "タイ", "フグ", "サバ"]

# 要素の削除
fish_types.remove("タイ")
print(fish_types)  # ["マグロ", "サケ", "フグ", "サバ"]

# インデックスによる削除
del fish_types[1]
print(fish_types)  # ["マグロ", "フグ", "サバ"]

# 最後の要素を取り出して削除
last_fish = fish_types.pop()
print(last_fish)  # "サバ"
print(fish_types)  # ["マグロ", "フグ"]

# リストのクリア
fish_types.clear()
print(fish_types)  # []
```

---

### リストのメソッド

```python
fish_types = ["マグロ", "サケ", "タイ", "フグ", "サバ"]

# ソート
fish_types.sort()
print(fish_types)  # ["サケ", "サバ", "タイ", "フグ", "マグロ"]

# 逆順
fish_types.reverse()
print(fish_types)  # ["マグロ", "フグ", "タイ", "サバ", "サケ"]

# 要素のカウント
print(fish_types.count("タイ"))  # 1

# インデックスの検索
print(fish_types.index("フグ"))  # 1

# コピー
fish_copy = fish_types.copy()
```

---

### リストの内包表記

- 簡潔にリストを作成する方法
- 既存のリストから新しいリストを生成する際に便利

```python
# 基本的な内包表記
squares = [x**2 for x in range(10)]
print(squares)  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# 条件付き内包表記
even_squares = [x**2 for x in range(10) if x % 2 == 0]
print(even_squares)  # [0, 4, 16, 36, 64]

# 魚の例
fish_lengths = [15, 25, 10, 30, 20]
big_fish = [length for length in fish_lengths if length > 20]
print(big_fish)  # [25, 30]
```

---

## タプル (Tuples)

---

### タプルの基本

- 順序付けられた変更不可能なデータのコレクション
- リストと似ているが、作成後に変更できない
- 丸括弧 `()` で作成
- インデックスは 0 から始まる

```python
# タプルの作成
fish_data = ("マグロ", 25.5, 3)
single_item_tuple = ("コイ",)  # カンマが必要

# インデックスによるアクセス
print(fish_data[0])  # "マグロ"
print(fish_data[-1])  # 3
```

---

### タプルの操作

```python
fish_data = ("マグロ", 25.5, 3)
more_data = ("新鮮", True)

# タプルの結合
combined = fish_data + more_data
print(combined)  # ("マグロ", 25.5, 3, "新鮮", True)

# タプルの繰り返し
repeated = ("コイ",) * 3
print(repeated)  # ("コイ", "コイ", "コイ")

# タプルのスライス
print(combined[1:4])  # (25.5, 3, "新鮮")

# タプルの長さ
print(len(combined))  # 5
```

---

### タプルとリストの違い

- タプルは変更不可能（イミュータブル）
- タプルはハッシュ可能なので、辞書のキーとして使用可能
- タプルは通常、異なる型の関連データを格納するために使用
- リストは同じ型の項目のコレクションに適している

```python
# これは動作する
fish_data = ("マグロ", 25.5, 3)
print(fish_data[0])  # "マグロ"

# これはエラーになる
# fish_data[0] = "サケ"  # TypeError: 'tuple' object does not support item assignment
```

---

### タプルのアンパック

```python
fish_data = ("マグロ", 25.5, 3)

# タプルのアンパック
name, length, age = fish_data
print(name)    # "マグロ"
print(length)  # 25.5
print(age)     # 3

# 一部の要素を無視
name, _, _ = fish_data
print(name)  # "マグロ"

# 残りの要素をリストとして取得
first, *rest = fish_data
print(first)  # "マグロ"
print(rest)   # [25.5, 3]
```

---

### タプルの使用例

```python
# 関数から複数の値を返す
def get_fish_stats():
    return "マグロ", 25.5, 3

name, length, age = get_fish_stats()
print(f"{name}は{age}歳で、長さは{length}cmです。")

# 辞書のキーとしてのタプル
locations = {
    (35.6895, 139.6917): "東京",
    (34.6937, 135.5022): "大阪",
    (43.0618, 141.3545): "札幌"
}
print(locations[(35.6895, 139.6917)])  # "東京"
```

---

## 集合 (Sets)

---

### 集合の基本

- 順序なしの一意な要素のコレクション
- 重複を許さない
- 中括弧 `{}` で作成
- 数学的な集合演算をサポート

```python
# 集合の作成
fish_types = {"マグロ", "サケ", "タイ", "フグ", "マグロ"}
print(fish_types)  # {"マグロ", "サケ", "タイ", "フグ"} (重複は自動的に削除)

# 空の集合
empty_set = set()  # 注意: {} は空の辞書を作成する

# リストから集合を作成
fish_list = ["マグロ", "サケ", "タイ", "フグ", "マグロ"]
fish_set = set(fish_list)
print(fish_set)  # {"マグロ", "サケ", "タイ", "フグ"}
```

---

### 集合の操作

```python
# 要素の追加
fish_set = {"マグロ", "サケ", "タイ"}
fish_set.add("フグ")
print(fish_set)  # {"マグロ", "サケ", "タイ", "フグ"}

# 要素の削除
fish_set.remove("サケ")  # 要素が存在しない場合はエラー
print(fish_set)  # {"マグロ", "タイ", "フグ"}

fish_set.discard("サケ")  # 要素が存在しない場合もエラーにならない

# 要素の取り出し
item = fish_set.pop()  # 任意の要素を取り出す
print(item)
print(fish_set)

# 集合のクリア
fish_set.clear()
print(fish_set)  # set()
```

---

### 集合の演算

```python
freshwater_fish = {"コイ", "フナ", "ウナギ", "アユ"}
saltwater_fish = {"マグロ", "サケ", "タイ", "フグ", "ウナギ"}

# 和集合 (Union)
all_fish = freshwater_fish | saltwater_fish
# または: all_fish = freshwater_fish.union(saltwater_fish)
print(all_fish)  # {"コイ", "フナ", "ウナギ", "アユ", "マグロ", "サケ", "タイ", "フグ"}

# 積集合 (Intersection)
common_fish = freshwater_fish & saltwater_fish
# または: common_fish = freshwater_fish.intersection(saltwater_fish)
print(common_fish)  # {"ウナギ"}

# 差集合 (Difference)
only_freshwater = freshwater_fish - saltwater_fish
# または: only_freshwater = freshwater_fish.difference(saltwater_fish)
print(only_freshwater)  # {"コイ", "フナ", "アユ"}

# 対称差 (Symmetric Difference)
exclusive_fish = freshwater_fish ^ saltwater_fish
# または: exclusive_fish = freshwater_fish.symmetric_difference(saltwater_fish)
print(exclusive_fish)  # {"コイ", "フナ", "アユ", "マグロ", "サケ", "タイ", "フグ"}
```

---

### 集合の包含関係

```python
fish_types = {"マグロ", "サケ", "タイ", "フグ", "ウナギ"}
tuna_types = {"クロマグロ", "キハダマグロ", "ビンナガマグロ"}
sushi_fish = {"マグロ", "サケ", "タイ"}

# 部分集合 (Subset)
print(sushi_fish.issubset(fish_types))  # True
print(sushi_fish <= fish_types)         # True

# 真部分集合 (Proper Subset)
print(sushi_fish < fish_types)  # True

# 上位集合 (Superset)
print(fish_types.issuperset(sushi_fish))  # True
print(fish_types >= sushi_fish)           # True

# 真上位集合 (Proper Superset)
print(fish_types > sushi_fish)  # True

# 互いに素 (Disjoint)
print(fish_types.isdisjoint(tuna_types))  # True
```

---

### 集合の使用例

```python
# 重複の削除
fish_caught = ["マグロ", "サケ", "タイ", "マグロ", "サケ", "フグ"]
unique_fish = set(fish_caught)
print(unique_fish)  # {"マグロ", "サケ", "タイ", "フグ"}

# メンバーシップテスト（含まれているかの確認）
print("マグロ" in unique_fish)  # True
print("コイ" in unique_fish)    # False

# 共通の要素を見つける
fish_market1 = {"マグロ", "サケ", "タイ", "フグ"}
fish_market2 = {"サケ", "ブリ", "タイ", "サバ"}
common_fish = fish_market1 & fish_market2
print(common_fish)  # {"サケ", "タイ"}
```

---

## 辞書 (Dictionaries)

---

### 辞書の基本

- キーと値のペアのコレクション
- キーは一意で変更不可能
- 中括弧 `{}` とコロン `:` で作成
- 高速なルックアップを提供

```python
# 辞書の作成
fish_info = {
    "name": "マグロ",
    "weight": 80.5,
    "length": 150,
    "is_fresh": True
}

# 値へのアクセス
print(fish_info["name"])  # "マグロ"

# get() メソッドを使用（キーが存在しない場合はデフォルト値を返す）
print(fish_info.get("color", "不明"))  # "不明"
```

---

### 辞書の操作

```python
fish_info = {"name": "マグロ", "weight": 80.5}

# 項目の追加/更新
fish_info["length"] = 150
fish_info["weight"] = 85.2
print(fish_info)  # {"name": "マグロ", "weight": 85.2, "length": 150}

# 項目の削除
del fish_info["weight"]
print(fish_info)  # {"name": "マグロ", "length": 150}

# pop() メソッドを使用（値を返して削除）
length = fish_info.pop("length")
print(length)     # 150
print(fish_info)  # {"name": "マグロ"}

# 辞書のクリア
fish_info.clear()
print(fish_info)  # {}
```

---

### 辞書のメソッド

```python
fish_info = {
    "name": "マグロ",
    "weight": 80.5,
    "length": 150,
    "is_fresh": True
}

# キーの取得
keys = fish_info.keys()
print(keys)  # dict_keys(["name", "weight", "length", "is_fresh"])

# 値の取得
values = fish_info.values()
print(values)  # dict_values(["マグロ", 80.5, 150, True])

# キーと値のペアの取得
items = fish_info.items()
print(items)  # dict_items([("name", "マグロ"), ("weight", 80.5), ("length", 150), ("is_fresh", True)])

# 辞書の更新
fish_info.update({"color": "赤", "price": 3000})
print(fish_info)  # {"name": "マグロ", "weight": 80.5, "length": 150, "is_fresh": True, "color": "赤", "price": 3000}
```

---

### 辞書の内包表記

```python
# 基本的な辞書内包表記
squares = {x: x**2 for x in range(6)}
print(squares)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# 条件付き辞書内包表記
even_squares = {x: x**2 for x in range(6) if x % 2 == 0}
print(even_squares)  # {0: 0, 2: 4, 4: 16}

# 魚の例
fish_lengths = {"マグロ": 150, "サケ": 80, "タイ": 40, "フグ": 30}
big_fish = {name: length for name, length in fish_lengths.items() if length > 50}
print(big_fish)  # {"マグロ": 150, "サケ": 80}
```

---

### 辞書の使用例

```python
# 魚の在庫管理
fish_inventory = {
    "マグロ": {"price": 3000, "stock": 5, "origin": "太平洋"},
    "サケ": {"price": 2000, "stock": 10, "origin": "北海道"},
    "タイ": {"price": 4000, "stock": 3, "origin": "瀬戸内海"},
    "フグ": {"price": 8000, "stock": 2, "origin": "下関"}
}

# 特定の魚の情報にアクセス
print(fish_inventory["サケ"]["price"])  # 2000
print(fish_inventory["タイ"]["origin"])  # "瀬戸内海"

# 在庫の更新
fish_inventory["マグロ"]["stock"] -= 1
print(fish_inventory["マグロ"]["stock"])  # 4

# 新しい魚を追加
fish_inventory["サバ"] = {"price": 600, "stock": 20, "origin": "三陸"}
```

---

### ネストしたデータ構造

```python
# リストの辞書
fish_by_type = {
    "freshwater": ["コイ", "フナ", "ウナギ", "アユ"],
    "saltwater": ["マグロ", "サケ", "タイ", "フグ"]
}

# 辞書のリスト
fish_records = [
    {"name": "マグロ", "weight": 80.5, "length": 150},
    {"name": "サケ", "weight": 5.2, "length": 75},
    {"name": "タイ", "weight": 3.8, "length": 40}
]

# アクセス例
print(fish_by_type["freshwater"][2])  # "ウナギ"
print(fish_records[1]["name"])        # "サケ"
```

---

## データ構造の選択

---

### どのデータ構造を選ぶべきか？

- **リスト**: 順序付けられた項目のコレクション、変更可能
  - 例: 魚の名前のリスト、釣った魚の記録

- **タプル**: 順序付けられた項目のコレクション、変更不可能
  - 例: 魚の座標 (x, y, z)、RGB色値

- **集合**: 一意な項目の順序なしコレクション
  - 例: 釣った魚の種類（重複なし）、共通の魚を見つける

- **辞書**: キーと値のペアのコレクション
  - 例: 魚の詳細情報、在庫管理

---

### 選択の基準

1. **データの性質**:
   - 順序は重要か？
   - 重複は許容されるか？
   - データは変更されるか？

2. **操作の種類**:
   - 頻繁にアクセスするか？
   - 追加/削除は多いか？
   - 検索は重要か？

3. **パフォーマンス**:
   - 大量のデータを扱うか？
   - 速度は重要か？

---

### パフォーマンスの比較

| 操作 | リスト | タプル | 集合 | 辞書 |
|------|-------|-------|------|------|
| アクセス | O(1) | O(1) | - | O(1) |
| 検索 | O(n) | O(n) | O(1) | O(1) |
| 挿入 | O(1)* | - | O(1) | O(1) |
| 削除 | O(n) | - | O(1) | O(1) |

\* リストの末尾に挿入する場合。途中に挿入する場合は O(n)。

---

## まとめ

---

### 学んだこと

- **リスト**: 順序付けられた変更可能なコレクション `[1, 2, 3]`
- **タプル**: 順序付けられた変更不可能なコレクション `(1, 2, 3)`
- **集合**: 順序なしの一意な要素のコレクション `{1, 2, 3}`
- **辞書**: キーと値のペアのコレクション `{"a": 1, "b": 2}`

---

### 次のステップ

- これらのデータ構造を組み合わせて複雑なデータモデルを作成
- 関数とモジュールを使ってコードを整理
- ファイル操作でデータを永続化
- 外部ライブラリを使ってデータ処理を拡張

---

### 練習問題

1. 魚の名前のリストを作成し、アルファベット順にソートする
2. 淡水魚と海水魚の集合を作成し、両方に生息できる魚を見つける
3. 魚の名前をキー、その特性を値とする辞書を作成する
4. ネストしたデータ構造を使って魚の詳細な情報を管理する

---

### 参考資料

- [Python 公式ドキュメント - データ構造](https://docs.python.org/ja/3/tutorial/datastructures.html)
- [Real Python - Python データ構造](https://realpython.com/python-data-structures/)
- [W3Schools - Python データ構造](https://www.w3schools.com/python/python_lists.asp)

---

## ご質問はありますか？

---

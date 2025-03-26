# Pythonのファイル操作と例外処理を学ぼう！

こんにちは、みなさん！今日は**くるみ**と**ジャービス**と一緒に、Pythonのファイル操作と例外処理について学んでいきましょう。これらのスキルは、データの読み書きやエラー処理など、実用的なプログラミングには欠かせない知識です。

## ファイル操作の基本

![くるみとジャービス](../../assets/images/kurumi_jarvis_placeholder.jpg)

**くるみ**: ねえジャービス、私たちのプログラムでデータを保存したり読み込んだりするにはどうすればいいの？

**ジャービス**: それはファイル操作を学ぶ必要があるね、くるみさん。Pythonではファイルの読み書きがとても簡単にできるんだ。

**くるみ**: 本当？どうやるの？

**ジャービス**: まず基本から説明するね。Pythonでファイルを操作するには、`open()`関数を使ってファイルを開く必要があるんだ。

```python
# ファイルを開く基本構文
file = open('ファイル名', 'モード')

# 例: 書き込みモード('w')でファイルを開く
file = open('fish_data.txt', 'w')
file.write("マグロ,80kg,太平洋\n")
file.write("サケ,5kg,北太平洋\n")
file.close()  # ファイルを閉じる
```

**くるみ**: なるほど！でも、このモードって何？

**ジャービス**: いい質問だね。モードはファイルをどのように操作するかを指定するものだよ。主なモードには以下のようなものがあるんだ：

- `'r'`: 読み込み専用（デフォルト）
- `'w'`: 書き込み専用（既存の内容は上書き）
- `'a'`: 追加書き込み（ファイルの末尾に追加）
- `'r+'`: 読み書き両用
- `'b'`: バイナリモード（テキストモードと組み合わせて使用: 'rb', 'wb'など）

**くるみ**: わかった！でも、ファイルを開いたら必ず閉じなきゃいけないの？忘れちゃったらどうなるの？

**ジャービス**: それは重要なポイントだね。ファイルを開いたら、必ず`close()`メソッドで閉じる必要があるんだ。閉じ忘れると、リソースリークが発生したり、データが正しく保存されなかったりする可能性があるんだよ。

**くるみ**: それは大変！忘れないようにする方法はないの？

**ジャービス**: あるよ！Pythonでは`with`ステートメントを使うことで、ファイルを自動的に閉じることができるんだ。これがベストプラクティスとされているよ。

```python
# withステートメントを使用したファイル操作
with open('fish_data.txt', 'r') as file:
    content = file.read()
    print(content)
# ブロックを抜けると自動的にファイルが閉じられる
```

**くるみ**: すごい！これなら忘れる心配がないね。ところで、日本語のファイルを扱う場合は何か特別なことが必要なの？

**ジャービス**: いい質問だね。日本語などの非ASCII文字を含むファイルを扱う場合は、エンコーディングを指定するといいよ。

```python
# エンコーディングを指定してファイルを開く
with open('fish_data.txt', 'r', encoding='utf-8') as file:
    content = file.read()
    print(content)
```

## CSVファイルとJSONファイルの操作

**くるみ**: ねえジャービス、私たちの魚のデータを表形式で保存したいんだけど、どうすればいいかな？

**ジャービス**: それならCSVファイルがぴったりだね！Pythonには`csv`モジュールがあって、CSVファイルの読み書きが簡単にできるんだ。

```python
import csv

# CSVファイルへの書き込み
fish_data = [
    ['名前', '重さ(kg)', '生息地'],
    ['マグロ', 80, '太平洋'],
    ['サケ', 5, '北太平洋'],
    ['タイ', 3, '日本海']
]

with open('fish_data.csv', 'w', newline='') as file:
    writer = csv.writer(file)
    writer.writerows(fish_data)

# CSVファイルの読み込み
with open('fish_data.csv', 'r') as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

**くるみ**: わあ、これは便利！でも、もっと複雑なデータ構造を保存したい場合はどうするの？

**ジャービス**: その場合はJSONファイルがおすすめだよ。JSONはJavaScript Object Notationの略で、階層構造を持つデータを保存するのに適しているんだ。Pythonには`json`モジュールがあるよ。

```python
import json

# 辞書の作成
fish_dict = {
    'マグロ': {
        '重さ': 80,
        '生息地': '太平洋',
        '栄養素': ['タンパク質', 'オメガ3脂肪酸', 'ビタミンD']
    },
    'サケ': {
        '重さ': 5,
        '生息地': '北太平洋',
        '栄養素': ['タンパク質', 'オメガ3脂肪酸', 'ビタミンB12']
    }
}

# JSONファイルへの書き込み
with open('fish_data.json', 'w', encoding='utf-8') as file:
    json.dump(fish_dict, file, ensure_ascii=False, indent=4)

# JSONファイルの読み込み
with open('fish_data.json', 'r', encoding='utf-8') as file:
    loaded_fish = json.load(file)
    print(loaded_fish)
```

**くるみ**: すごい！これで複雑なデータも簡単に保存できるね！

## 例外処理の基本

**くるみ**: ねえジャービス、でもファイルが見つからなかったり、読み込めなかったりしたらどうなるの？

**ジャービス**: いい質問だね。そういう場合に備えて、Pythonには例外処理という仕組みがあるんだ。`try`、`except`、`else`、`finally`ブロックを使って、エラーを適切に処理することができるよ。

```python
try:
    # 例外が発生する可能性のあるコード
    with open('non_existent_file.txt', 'r') as file:
        content = file.read()
except FileNotFoundError:
    # ファイルが見つからない場合の処理
    print("ファイルが見つかりません。")
except PermissionError:
    # ファイルにアクセスする権限がない場合の処理
    print("ファイルにアクセスする権限がありません。")
else:
    # 例外が発生しなかった場合に実行
    print(f"ファイルの内容: {content}")
finally:
    # 例外の有無にかかわらず実行
    print("ファイル操作が完了しました。")
```

**くるみ**: なるほど！これで安全にファイル操作ができるね。でも、どんな種類の例外があるの？

**ジャービス**: Pythonには多くの組み込み例外があるよ。ファイル操作でよく遭遇する例外には以下のようなものがあるんだ：

- `FileNotFoundError`: ファイルが見つからない
- `PermissionError`: ファイルにアクセスする権限がない
- `IOError`: 入出力エラー
- `UnicodeDecodeError`: ファイルのデコードエラー

**くるみ**: わかった！でも、もっと具体的なエラーを処理したい場合はどうするの？

**ジャービス**: その場合は、独自の例外クラスを定義することができるよ。これをカスタム例外と呼ぶんだ。

```python
# カスタム例外クラスの定義
class FishError(Exception):
    """魚に関連するエラーの基底クラス"""
    pass

class InvalidWeightError(FishError):
    """無効な魚の重さに関するエラー"""
    pass

# カスタム例外の使用
def validate_fish_weight(weight):
    if weight <= 0:
        raise InvalidWeightError("魚の重さは正の値でなければなりません。")
    return weight

try:
    fish_weight = validate_fish_weight(-5)
except InvalidWeightError as e:
    print(f"エラー: {e}")
```

## 実践的な例：魚のデータベース

**くるみ**: これまでの知識を使って、実際に魚のデータベースを作ってみたいな！

**ジャービス**: いいね！それでは、ファイル操作と例外処理を組み合わせて、簡単な魚のデータベースを作ってみよう。

```python
import json
import os

class FishDatabase:
    def __init__(self, filename):
        self.filename = filename
        self.fish_data = {}
        self.load_data()
    
    def load_data(self):
        """データベースファイルからデータを読み込む"""
        try:
            if os.path.exists(self.filename):
                with open(self.filename, 'r', encoding='utf-8') as file:
                    self.fish_data = json.load(file)
                print(f"データを正常に読み込みました: {len(self.fish_data)}種類の魚")
            else:
                print("データベースファイルが存在しません。新しいデータベースを作成します。")
        except json.JSONDecodeError:
            print("データベースファイルの形式が無効です。新しいデータベースを作成します。")
        except Exception as e:
            print(f"データの読み込み中にエラーが発生しました: {e}")
    
    def save_data(self):
        """データをデータベースファイルに保存する"""
        try:
            with open(self.filename, 'w', encoding='utf-8') as file:
                json.dump(self.fish_data, file, ensure_ascii=False, indent=4)
            print("データを正常に保存しました。")
        except Exception as e:
            print(f"データの保存中にエラーが発生しました: {e}")
    
    def add_fish(self, name, weight, habitat):
        """魚をデータベースに追加する"""
        try:
            if name in self.fish_data:
                print(f"警告: {name}は既にデータベースに存在します。上書きします。")
            
            self.fish_data[name] = {
                '重さ': float(weight),
                '生息地': habitat
            }
            print(f"{name}をデータベースに追加しました。")
            self.save_data()
        except ValueError:
            print("エラー: 重さは数値でなければなりません。")
        except Exception as e:
            print(f"魚の追加中にエラーが発生しました: {e}")
    
    def get_fish(self, name):
        """魚の情報を取得する"""
        try:
            if name in self.fish_data:
                return self.fish_data[name]
            else:
                print(f"エラー: {name}はデータベースに存在しません。")
                return None
        except Exception as e:
            print(f"魚の取得中にエラーが発生しました: {e}")
            return None
    
    def list_all_fish(self):
        """すべての魚を一覧表示する"""
        try:
            if not self.fish_data:
                print("データベースは空です。")
                return
            
            print("\n===== 魚のデータベース =====")
            for name, info in self.fish_data.items():
                print(f"名前: {name}, 重さ: {info['重さ']}kg, 生息地: {info['生息地']}")
            print("==========================\n")
        except Exception as e:
            print(f"魚の一覧表示中にエラーが発生しました: {e}")
    
    def delete_fish(self, name):
        """魚をデータベースから削除する"""
        try:
            if name in self.fish_data:
                del self.fish_data[name]
                print(f"{name}をデータベースから削除しました。")
                self.save_data()
            else:
                print(f"エラー: {name}はデータベースに存在しません。")
        except Exception as e:
            print(f"魚の削除中にエラーが発生しました: {e}")

# データベースの使用例
def main():
    db = FishDatabase('fish_database.json')
    
    # 魚を追加
    db.add_fish('マグロ', 80, '太平洋')
    db.add_fish('サケ', 5, '北太平洋')
    db.add_fish('タイ', 3, '日本海')
    
    # すべての魚を一覧表示
    db.list_all_fish()
    
    # 特定の魚の情報を取得
    tuna_info = db.get_fish('マグロ')
    if tuna_info:
        print(f"マグロの情報: 重さ: {tuna_info['重さ']}kg, 生息地: {tuna_info['生息地']}")
    
    # 魚を削除
    db.delete_fish('タイ')
    
    # 更新された一覧を表示
    db.list_all_fish()

if __name__ == "__main__":
    main()
```

**くるみ**: すごい！これで魚のデータを簡単に管理できるね！

**ジャービス**: そうだね。このプログラムでは、ファイル操作と例外処理を組み合わせて、堅牢なデータベースシステムを作成しているんだ。実際のアプリケーションでも、このような方法でデータを管理することが多いよ。

## まとめ

**くるみ**: 今日はたくさんのことを学んだね！ファイル操作と例外処理について、もう一度おさらいしてみよう。

**ジャービス**: いいね！今日学んだ主なポイントは以下の通りだよ：

1. **ファイル操作の基本**：
   - `open()`関数でファイルを開く
   - ファイルモード（'r', 'w', 'a'など）の使い分け
   - `with`ステートメントを使用して自動的にファイルを閉じる

2. **様々なファイル形式の操作**：
   - CSVファイル：`csv`モジュールを使用
   - JSONファイル：`json`モジュールを使用

3. **例外処理**：
   - `try`, `except`, `else`, `finally`ブロックの使用
   - 具体的な例外タイプのキャッチ
   - カスタム例外クラスの定義と使用

4. **実践的なアプリケーション**：
   - 例外処理とファイル操作を組み合わせた堅牢なプログラムの作成
   - データの永続化と管理

**くるみ**: ありがとう、ジャービス！これでPythonのファイル操作と例外処理についてよく理解できたよ。次回も楽しみにしてるね！

**ジャービス**: こちらこそ、くるみさん。次回はPythonのベストプラクティスについて学んでいこう！

---

これでPythonのファイル操作と例外処理についての基本を学びました。これらの知識を活用して、データの読み書きや堅牢なプログラムの作成に取り組んでみてください。次回もお楽しみに！

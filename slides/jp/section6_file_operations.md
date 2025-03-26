# セクション6: ファイル操作と例外処理

## ファイル操作の基本

### ファイルの読み書き
- ファイルを開く: `open()` 関数
- 読み込みモード: `'r'`
- 書き込みモード: `'w'`
- 追加モード: `'a'`
- バイナリモード: `'b'`
- ファイルを閉じる: `close()` メソッド

### ファイルの読み込み
```python
# ファイル全体を読み込む
with open('fish_data.txt', 'r') as file:
    content = file.read()

# 1行ずつ読み込む
with open('fish_data.txt', 'r') as file:
    for line in file:
        print(line.strip())
```

### ファイルへの書き込み
```python
# ファイルに書き込む
with open('new_fish.txt', 'w') as file:
    file.write('マグロ,80kg,太平洋\n')
    file.write('サケ,5kg,北太平洋\n')

# ファイルに追加する
with open('new_fish.txt', 'a') as file:
    file.write('タイ,3kg,日本海\n')
```

### `with` ステートメント
- ファイルを自動的に閉じる
- リソース管理の推奨される方法
- 例外が発生しても確実にファイルが閉じられる

---

## ファイルパスとディレクトリ操作

### `os` モジュール
```python
import os

# 現在の作業ディレクトリ
current_dir = os.getcwd()

# ディレクトリ内のファイル一覧
files = os.listdir(current_dir)

# ディレクトリの作成
os.mkdir('fish_data')

# ファイルの存在確認
exists = os.path.exists('fish_data.txt')

# ファイルパスの結合
path = os.path.join('fish_data', 'tuna.txt')
```

### `pathlib` モジュール (Python 3.4+)
```python
from pathlib import Path

# 現在のディレクトリ
current_dir = Path.cwd()

# ホームディレクトリ
home = Path.home()

# パスの結合
data_file = current_dir / 'fish_data' / 'tuna.txt'

# ディレクトリの作成
Path('fish_images').mkdir(exist_ok=True)

# ファイルの存在確認
exists = Path('fish_data.txt').exists()
```

---

## 様々なファイル形式の操作

### CSV ファイル
```python
import csv

# CSVファイルの読み込み
with open('fish_data.csv', 'r') as file:
    csv_reader = csv.reader(file)
    for row in csv_reader:
        print(row)

# CSVファイルへの書き込み
with open('new_fish.csv', 'w', newline='') as file:
    csv_writer = csv.writer(file)
    csv_writer.writerow(['名前', '重さ(kg)', '生息地'])
    csv_writer.writerow(['マグロ', 80, '太平洋'])
    csv_writer.writerow(['サケ', 5, '北太平洋'])
```

### JSON ファイル
```python
import json

# 辞書の作成
fish_dict = {
    'マグロ': {'重さ': 80, '生息地': '太平洋'},
    'サケ': {'重さ': 5, '生息地': '北太平洋'},
    'タイ': {'重さ': 3, '生息地': '日本海'}
}

# JSONファイルへの書き込み
with open('fish_data.json', 'w') as file:
    json.dump(fish_dict, file, ensure_ascii=False, indent=4)

# JSONファイルの読み込み
with open('fish_data.json', 'r') as file:
    loaded_data = json.load(file)
```

### pickle ファイル (Pythonオブジェクトのシリアル化)
```python
import pickle

# オブジェクトのシリアル化
with open('fish_data.pkl', 'wb') as file:
    pickle.dump(fish_dict, file)

# オブジェクトのデシリアル化
with open('fish_data.pkl', 'rb') as file:
    loaded_data = pickle.load(file)
```

---

## 例外処理

### 基本的な例外処理
```python
try:
    # 例外が発生する可能性のあるコード
    file = open('non_existent_file.txt', 'r')
    content = file.read()
    file.close()
except FileNotFoundError:
    # ファイルが見つからない場合の処理
    print('ファイルが見つかりません')
```

### 複数の例外をキャッチ
```python
try:
    number = int(input('数字を入力してください: '))
    result = 10 / number
    print(f'結果: {result}')
except ValueError:
    print('有効な数字を入力してください')
except ZeroDivisionError:
    print('ゼロで割ることはできません')
```

### `else` と `finally` 句
```python
try:
    file = open('fish_data.txt', 'r')
    content = file.read()
except FileNotFoundError:
    print('ファイルが見つかりません')
else:
    # 例外が発生しなかった場合に実行
    print(f'ファイルの内容: {content}')
finally:
    # 例外の有無にかかわらず実行
    try:
        file.close()
    except:
        pass
```

### 例外の発生
```python
def validate_weight(weight):
    if weight <= 0:
        raise ValueError('重さは正の値でなければなりません')
    return weight

try:
    fish_weight = validate_weight(-5)
except ValueError as e:
    print(f'エラー: {e}')
```

---

## カスタム例外

### カスタム例外クラスの定義
```python
class FishError(Exception):
    """魚に関連するエラーの基底クラス"""
    pass

class InvalidWeightError(FishError):
    """無効な魚の重さに関するエラー"""
    pass

class InvalidSpeciesError(FishError):
    """無効な魚の種類に関するエラー"""
    pass
```

### カスタム例外の使用
```python
def process_fish(name, weight):
    valid_species = ['マグロ', 'サケ', 'タイ', 'サバ', 'アジ']
    
    if name not in valid_species:
        raise InvalidSpeciesError(f'{name}は有効な魚の種類ではありません')
    
    if weight <= 0:
        raise InvalidWeightError(f'重さは正の値でなければなりません（入力値: {weight}）')
    
    return f'{name}, {weight}kg'

try:
    result = process_fish('フグ', 2)
except InvalidSpeciesError as e:
    print(f'種類エラー: {e}')
except InvalidWeightError as e:
    print(f'重さエラー: {e}')
except FishError as e:
    print(f'一般的な魚のエラー: {e}')
```

---

## コンテキストマネージャ

### `with` ステートメントとコンテキストマネージャ
```python
# ファイル操作のコンテキストマネージャ
with open('fish_data.txt', 'r') as file:
    content = file.read()
# ファイルは自動的に閉じられる
```

### カスタムコンテキストマネージャの作成
```python
class FishDatabase:
    def __init__(self, filename):
        self.filename = filename
        self.file = None
    
    def __enter__(self):
        self.file = open(self.filename, 'r')
        return self.file
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()

# カスタムコンテキストマネージャの使用
with FishDatabase('fish_data.txt') as file:
    content = file.read()
```

### `contextlib` モジュール
```python
from contextlib import contextmanager

@contextmanager
def open_fish_database(filename):
    try:
        file = open(filename, 'r')
        yield file
    finally:
        file.close()

# contextlibを使用したコンテキストマネージャ
with open_fish_database('fish_data.txt') as file:
    content = file.read()
```

---

## 実践的なファイル操作と例外処理

### ログファイルの作成
```python
import logging

# ログの設定
logging.basicConfig(
    filename='fish_app.log',
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

try:
    # 何らかの操作
    logging.info('魚のデータを処理しています')
    result = 10 / 0  # ゼロ除算エラー
except Exception as e:
    logging.error(f'エラーが発生しました: {e}')
```

### 一時ファイルの使用
```python
import tempfile
import os

# 一時ファイルの作成
with tempfile.NamedTemporaryFile(delete=False) as temp:
    temp.write(b'一時的な魚のデータ')
    temp_name = temp.name

try:
    # 一時ファイルの使用
    with open(temp_name, 'rb') as file:
        content = file.read()
    print(content)
finally:
    # 一時ファイルの削除
    os.unlink(temp_name)
```

### 大きなファイルの効率的な処理
```python
# 大きなファイルを1行ずつ処理
def process_large_fish_file(filename):
    try:
        with open(filename, 'r') as file:
            for i, line in enumerate(file, 1):
                try:
                    # 各行の処理
                    process_line(line)
                except Exception as e:
                    print(f'行 {i} の処理中にエラーが発生しました: {e}')
    except FileNotFoundError:
        print(f'ファイル {filename} が見つかりません')
    except PermissionError:
        print(f'ファイル {filename} にアクセスする権限がありません')
```

---

## ベストプラクティス

### ファイル操作のベストプラクティス
- 常に `with` ステートメントを使用する
- 適切なエラー処理を行う
- バイナリファイルとテキストファイルを区別する
- 文字エンコーディングを明示的に指定する
- 大きなファイルはチャンクで処理する

### 例外処理のベストプラクティス
- 具体的な例外をキャッチする
- 例外を無視しない
- ログを適切に記録する
- クリーンアップコードは `finally` ブロックに配置する
- 例外は適切なレベルで処理する

### セキュリティ上の考慮事項
- ユーザー入力からのファイルパスを検証する
- 適切なファイルアクセス権限を設定する
- 機密情報を平文で保存しない
- 一時ファイルを適切に管理する

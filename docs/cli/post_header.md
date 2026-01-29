# post-header

RRI の `out` にヘッダーを付与して **ASCII グリッド（.asc）** を作成します。  
RAW (`.out`) とヘッダー雛形を使って、後処理に使える `.asc` を生成します。

## 実行

```powershell
uv run python main.py post-header
```

### 主なオプション

- `--project`  
  - `project.toml` を明示指定します（未指定ならカレントの `project.toml`）。
- `--config`  
  - `post_header.toml` を直接指定します。
- `--dry-run`  
  - 設定確認のみ行い、処理は実行しません。

## 設定ファイルの読み方

`project.toml` の `[post_header].config` を参照します。

```toml
[post_header]
config = "data/tools_config/post_header/post_header.toml"
```

## 入力

### RAW 入力（必須）

- **raw_input_dir**  
  - RRI の `out` ディレクトリを指定します。

### ヘッダー雛形

- **header_template**  
  - 通常格子の `.asc` ヘッダーを指定します。
- **fine_header_template（任意）**  
  - fine 格子の `.asc` ヘッダーを指定します。

> 2つ必要な理由:  
> RRI の `out` には **通常格子**と**fine 格子**が混在します。  
> それぞれ **セルサイズや行列サイズが異なる**ため、別のヘッダー雛形が必要です。  
> fine 格子が存在しない場合は `fine_header_template` を空欄にできます。

### 追加パラメータ

- **prefixes**  
  - 対象 prefix を絞り込みたい場合に指定します。\n
  - 空の場合は自動検出した prefix をすべて処理します。
- **flat_output**  
  - `true` の場合、出力先直下に `.asc` を並べます。\n
  - `false` の場合、prefix ごとのサブディレクトリに出力します。

## 設定例（post_header.toml）

```toml
[inputs]
raw_input_dir = "data/input_test"
header_template = "data/input_test/dem_kiku.asc"
fine_header_template = "data/input_test/dem_kiku.asc"

[outputs]
header_output_dir = "data/tools_output/ouptut_kiku"

[params]
prefixes = []
flat_output = true
```

## 出力

- **header_output_dir** に `.asc` を出力します。
- prefix 単位でファイルが作成されます。

## 補足

- fine 格子を扱う場合は `fine_header_template` を指定してください。\n
- 入力/出力ディレクトリは同一にしないでください。

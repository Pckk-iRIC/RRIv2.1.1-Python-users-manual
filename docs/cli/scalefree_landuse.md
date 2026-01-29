# scaleFree + landuse

scaleFree を実行し、その結果から **landuse 付与（grad × landuse 変換）** まで一括で行います。  
**scaleFree の出力（grad / land）が必須**になります。

## 実行

```powershell
uv run python main.py scalefree-landuse
```

### 主なオプション

- `--project`  
  - `project.toml` を明示指定します（未指定ならカレントの `project.toml`）。
- `--config`  
  - `scaleFree.toml` / `scaleFree.txt` を直接指定します。
- `--rules`  
  - landuse ルール CSV を指定します。
- `--output`  
  - landuse 付与後の出力 `.asc` を指定します。
- `--dry-run`  
  - 設定確認のみ行い、処理は実行しません。

## 参照される設定

- `project.toml` の `[scale_free].config`  
  - scaleFree の設定ファイル（TOML/TXT）
- `project.toml` の `[landuse].rules` / `[landuse].output`  
  - landuse のルールと出力先

## 入力

### scaleFree 側の必須出力

`scaleFree` の設定ファイル（TOML/TXT）内で、次の出力が指定されている必要があります。

- **outputs.grad**  
  - 勾配（grad）ASCII Grid
- **outputs.land**  
  - landuse ASCII Grid

> `outputs.grad` / `outputs.land` が未設定の場合、エラーになります。  
> なお **`outputs.land` は `inputs.land` が指定されている場合のみ出力されます**。

### landuse 側の入力

- **rules（CSV）**  
  - landuse 付与ルール（`[landuse].rules` で指定）
  - ルール形式の詳細は [landuse 付与](landuse.md) を参照してください。

## 出力

- scaleFree の出力（設定ファイルで指定されたもの）
- landuse 付与済み ASCII Grid（`[landuse].output` または `--output`）

## 補足

- `--dry-run` は scaleFree 出力の有無と landuse ルールの存在を 設定を確認します。

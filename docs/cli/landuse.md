# landuse 付与

勾配（grad）と landuse を組み合わせて、**土地利用区分コードを更新**するツールです。  
勾配の範囲に応じて landuse を置き換えるルールを CSV で指定します。

## 実行

```powershell
uv run python main.py landuse
```

### 主なオプション

- `--project`  
  - `project.toml` を明示指定します（未指定ならカレントの `project.toml`）。
- `--grad`  
  - 勾配の ASCII Grid（.asc）を指定します。
- `--landuse`  
  - landuse の ASCII Grid（.asc）を指定します。
- `--rules`  
  - ルール CSV を指定します。
- `--output`  
  - 出力する landuse の ASCII Grid を指定します。
- `--dry-run`  
  - 設定確認のみ行い、処理は実行しません。

## 設定ファイルの読み方

`project.toml` の `[landuse]` を参照します。

```toml
[landuse]
rules = "data/tools_config/landuse_from_grad/landuse_rules.csv"
output = "data/tools_output/landuse_from_grad/landuse_from_grad.asc"
grad = "data/tools_input_asc/landuse_from_grad/grad_anou_150m.asc"
landuse = "data/tools_input_asc/landuse_from_grad/landuse_150m.asc"
```

## 入力ファイル

### grad（勾配）

- ASCII Grid（.asc）
- landuse と **同じグリッド**である必要があります。

### landuse（土地利用）

- ASCII Grid（.asc）
- 値は **土地利用区分コード（整数）**を想定しています。

### rules（ルールCSV）

以下のヘッダーを持つ CSV です。

```
base_landuse,min,max,code
```

- 例（先頭5行）:

```
base_landuse,min,max,code
1,0,0.4,1
1,0.4,0.5,2
1,0.5,,3
2,*,*,4
3,*,*,5
```

- `base_landuse`  
  - 変換対象となる landuse の元コード
- `min` / `max`  
  - 勾配の範囲（`*` は無条件）
- `code`  
  - 置き換える landuse コード

> `min`/`max` の片方だけに `*` は使えません。両方 `*` にすると無条件になります。

## 出力

- landuse 付与済みの ASCII Grid（.asc）

## 補足

- grad と landuse のヘッダーが一致しない場合はエラーになります。
- scaleFree と連携する場合は `scalefree-landuse` を推奨します。

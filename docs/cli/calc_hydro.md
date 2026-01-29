# calcHydro

RRI の `out` 出力から、指定地点の水位・流量などを抽出します。  
地点情報（location）と出力プレフィックスを指定して実行します。

## 実行

```powershell
uv run python main.py calc-hydro
```

### 主なオプション

- `--project`  
  - `project.toml` を明示指定します（未指定ならカレントの `project.toml`）。
- `--config`  
  - `calcHydro.toml` / `calcHydro.txt` を直接指定します。
- `--dry-run`  
  - 設定確認のみ行い、処理は実行しません。

## 設定ファイルの読み方

`project.toml` の `[calc_hydro].config` を参照します。

```toml
[calc_hydro]
config = "data/tools_config/calcHydro/calcHydro.toml"
```

## 入力ファイル

### calcHydro.toml（推奨）

`[inputs]` と `[outputs]` を使用します。

```toml
[inputs]
location = "data/tools_input_asc/calcHydro/location_anou_150m.txt"
infile_prefix = "data/tools_input_asc/calcHydro/qr_"

[outputs]
outfile_prefix = "data/tools_output/calcHydro/hydro_"
```

### calcHydro.txt

3 行構成です。

1. location ファイルのパス  
2. 入力プレフィックス（例: `qr_`）  
3. 出力プレフィックス（例: `hydro_`）  

### location ファイル

1 行ごとに **地点名 / I / J** を記述します（I/J は **1始まり**）。

```
point_A 120 85
point_B 130 90
```

## 入力の意味

- **infile_prefix**  
  - `RRI out` のファイル名プレフィックスです。\n
  - 例: `qr_000001.out` を読む場合は `qr_` を指定します。\n
- **location**  
  - 抽出地点（I/J）を指定します。

## 出力

- 指定地点ごとの時系列ファイル（例: `hydro_point_A.txt`）

## 補足

- 入力の `infile_prefix` は **RRI 出力 .out** を指します。

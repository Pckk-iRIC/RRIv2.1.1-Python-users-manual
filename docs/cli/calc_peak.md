# calcPeak

RRI の `out` 出力から、各セルのピーク値を抽出します。  
入力は `out` のプレフィックスと参照ヘッダーを指定します。

## 実行

```powershell
uv run python main.py calc-peak
```

### 主なオプション

- `--project`  
  - `project.toml` を明示指定します（未指定ならカレントの `project.toml`）。
- `--config`  
  - `calcPeak.toml` / `calcPeak.txt` を直接指定します。
- `--dry-run`  
  - 設定確認のみ行い、処理は実行しません。

## 設定ファイルの読み方

`project.toml` の `[calc_peak].config` を参照します。

```toml
[calc_peak]
config = "data/tools_config/calcPeak/calcPeak.toml"
```

## 入力ファイル

### calcPeak.toml（推奨）

`[inputs]` と `[outputs]` を使用します。

```toml
[inputs]
dem = "data/tools_input_asc/calcPeak/adem_anou_150m.asc"
infile_prefix = "data/tools_input_asc/calcPeak/gampt_ff_"
maxt = 10

[outputs]
outfile = "data/tools_output/calcPeak/hpeak.txt"
```

### calcPeak.txt

4 行構成です。

1. 参照ヘッダー（DEM）のパス  
2. 入力プレフィックス（例: `gampt_ff_`）  
3. 最大ステップ数（maxt）  
4. 出力ファイルのパス  

## 入力の意味

- **dem**  
  - 出力ヘッダーを作るための参照 DEM です。
- **infile_prefix**  
  - `RRI out` のファイル名プレフィックスです。\n
  - 例: `gampt_ff_000001.out` を読む場合は `gampt_ff_` を指定します。\n
- **maxt**  
  - 読み込む時系列の最大番号です（例: 1〜10）。

## 出力

- ピーク値を集約したテキストファイル（ASCII Grid）

## 補足

- 入力の `infile_prefix` は **RRI 出力 .out** を指します。

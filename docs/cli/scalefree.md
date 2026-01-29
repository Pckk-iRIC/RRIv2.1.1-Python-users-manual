# scaleFree

DEM などの地形データを **スケールアップ（粗い格子化）** して、RRI の前処理用データを生成します。  
単なる前処理だけでなく、**landuse 付与や河道—斜面の接続情報**にも使われます。  
本ツールは **設定ファイルに書かれた入出力だけを対象**に処理します。

## 実行

```powershell
uv run python main.py scalefree
```

### 主なオプション

- `--project`  
  - `project.toml` を明示指定します（未指定ならカレントの `project.toml`）。
- `--config`  
  - `scaleFree.toml` / `scaleFree.txt` を直接指定します。
- `--outputs`  
  - 出力対象を制限します（例: `dem,dir,acc`）。
- `--dry-run`  
  - 設定確認のみ行い、処理は実行しません。

## 設定ファイルの読み方

### 1) `project.toml` から参照する場合

`project.toml` の `[scale_free].config` を参照します。

```toml
[scale_free]
config = "data/tools_config/scaleFree/scaleFree.toml"
```

### 2) `--config` で直接指定する場合

```powershell
uv run python main.py scalefree --config data/tools_config/scaleFree/scaleFree.toml
```

## 設定ファイルの形式

### TOML 形式（推奨）

```toml
[inputs]
dem = "data/tools_input_asc/common/dem_anou.asc"
dir = "data/tools_input_asc/common/dir_anou.asc"
acc = "data/tools_input_asc/common/acc_anou.asc"
sec = "data/tools_input_asc/common/secid_sample.asc"
land = "data/tools_input_asc/common/landuse_sample.asc"

[params]
ups = 5
fups = 2
grad_thresh = 0.3
rl_thresh = 1000

[outputs]
land = "data/tools_output/scaleFree/landuse_s_150m.asc"
grad = "data/tools_output/scaleFree/grad_anou_150m.asc"
```

### TXT 形式

`scaleFree.txt` でも動作しますが、**相対パスはカレントディレクトリ基準**になります。

## 入力ファイル（5種）

いずれも **ASCII グリッド（.asc）** を想定しています。

- **dem**  
  標高（DEM）。スケールアップと調整の基準になります。
- **dir**  
  流向（8方向の数値）。流路の向きを表します。
- **acc**  
  累積流量（flow accumulation）。上流セル数の指標です。
- **sec**（任意）  
  河川断面・河道区分の ID。指定しない場合は関連出力がスキップされます。
- **land**（任意）  
  土地利用区分コード。指定しない場合は関連出力がスキップされます。

> `outputs.sec` / `outputs.land` を出したい場合は、対応する入力（`inputs.sec` / `inputs.land`）が必要です。

## 出力の指定ルール（重要）

- **出力は `[outputs]` にパスが書かれているものだけ作成されます。**
- `--outputs` で出力対象を指定した場合、**対応する出力パスが `[outputs]` に存在しないとエラー**になります。

### 出力名の一覧

```
dem, dir, acc, sec, land, grad, idx, fdem, fidx, riv_slo_ups, riv_slo_org_ups
```

## 出力ファイル（11種）

出力は `TOML` の `[outputs]` に指定されたものだけ生成されます。

- **dem**  
  スケールアップ後の **ADEM**。スロープ/河道計算に使う調整済み DEM です。
- **dir**  
  スケールアップ後の流向（ADIR）。
- **acc**  
  スケールアップ後の累積流量。
- **sec**  
  スケールアップ後の断面/河道区分 ID。
- **land**  
  スケールアップ後の土地利用。
- **grad**  
  平均勾配（sin θ）。RRI の斜面計算で使用します。
- **idx**  
  スケールアップ格子のセル ID（斜面格子用）。
- **fdem**  
  fine 格子用 DEM。調整（demAdjustment）は行われません。
- **fidx**  
  fine 格子用セル ID。
- **riv_slo_ups**  
  河道格子と斜面格子の接続情報（同一解像度）。
- **riv_slo_org_ups**  
  河道格子と斜面格子の接続情報（異なる解像度）。

### `--outputs` の例

```powershell
uv run python main.py scalefree --outputs grad,land
```

## 入力と出力の解決ルール

- TOML 形式は **`project.toml` の場所**を基準に相対パスが解決されます。
- TXT 形式は **カレントディレクトリ**基準です。

## 補足

- `--dry-run` で入力/出力の存在とパス関係を検証できます。

# makeRiver5

RRI 本体で利用する **river5 関連データ（幅・深さ・高さ）** を生成します。  
このツールは **DEM / ACC / DIR** と、`params` に指定した河道パラメータから計算します。

## 実行

```powershell
uv run python main.py make-river5
```

### 主なオプション

- `--project`  
  - `project.toml` を明示指定します（未指定ならカレントの `project.toml`）。
- `--config`  
  - `makeRiver5.toml` / `makeRiver5.txt` を直接指定します。
- `--rri-input`  
  - `RRI_Input.txt` を直接指定します（TOMLで入力を指定しない場合のみ使用）。
- `--dry-run`  
  - 設定確認のみ行い、処理は実行しません。

## 設定ファイルの読み方

### 1) `project.toml` から参照する場合

```toml
[make_river5]
config = "data/tools_config/makeRiver5/makeRiver5.toml"
```

### 2) `--config` / `--rri-input` を直接指定する場合

```powershell
uv run python main.py make-river5 --config data/tools_config/makeRiver5/makeRiver5.toml
```

## 入力ファイル

### makeRiver5.toml（推奨）

`[inputs]` と `[params]` に **DEM/ACC/DIR と計算パラメータ** を指定します。

```toml
[inputs]
dem = "data/tools_input_asc/common/dem_anou.asc"
acc = "data/tools_input_asc/common/acc_anou.asc"
dir = "data/tools_input_asc/common/dir_anou.asc"

[params]
utm = 0
riv_thresh1 = 10
riv_thresh2 = 50
area_param_c = 7.0
area_param_s = 0.7858
wd_param_c = 2.898
wd_param_s = 0.324
height_param = 0.0
height_limit = 20.0

[outputs]
width = "data/tools_output/makeRiver5/width.asc"
depth = "data/tools_output/makeRiver5/depth.asc"
height = "data/tools_output/makeRiver5/height.asc"
```

### RRI_Input.txt（任意）

TOML で入力を指定しない場合、`RRI_Input.txt` から次を参照します。

- **4〜6行目**: DEM / ACC / DIR の入力パス
- **9行目**: `utm`
- **44〜51行目**: 河道パラメータ

> TOML の `[inputs]` / `[params]` がある場合、RRI_Input.txt は不要です。

## 出力ファイル（3種）

- **width**  
  河川幅（ASCII Grid）
- **depth**  
  河川深さ（ASCII Grid）
- **height**  
  河川高さ（ASCII Grid）

## 入力と出力の解決ルール

- DEM/ACC/DIR と params は次の優先順位で解決されます。  
  1) `RRI_Input.txt`（`--rri-input` または `project.toml [rri].input`）  
  2) `makeRiver5.toml` の `[inputs]` / `[params]`
- `makeRiver5.toml` の相対パスは **project.toml の場所**を基準に解決されます。

## 補足

- `--dry-run` で DEM/ACC/DIR と出力先の存在を確認できます。

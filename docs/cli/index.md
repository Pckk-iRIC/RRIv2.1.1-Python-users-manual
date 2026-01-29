# CLI 使い方の概要

CLI は `main.py` を入口にして実行します。

```powershell
uv run python main.py <command> [options]
```

## 共通オプション

- `--dry-run`: 設定内容だけ確認し、実行は行いません

## サブコマンド一覧

- `pre` 入力データ作成 GUI
- `post` 結果可視化 GUI
- `scalefree` scaleFree 単体
- `scalefree-landuse` scaleFree + landuse
- `landuse` landuse 単体
- `make-river5` makeRiver5
- `calc-hydro` calcHydro
- `calc-peak` calcPeak
- `post-header` out → asc
- `post-value-max` 最大値ラスター生成

各コマンドの詳細は以下を参照してください。

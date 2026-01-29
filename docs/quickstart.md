# クイックスタート

最小限の手順で動作確認するためのページです。

## 1. 設定ファイルの確認

`project.toml` を確認し、各ツールの設定ファイルパスが正しいか確認します。

- 例: `data/tools_config/` 配下の設定を使う
- 実データを使う場合は、パスを実データに合わせて編集します

## 2. 前処理の一括実行（例）

```powershell
uv run python main.py scalefree-landuse
```

## 3. 解析補助ツール

```powershell
uv run python main.py make-river5
uv run python main.py calc-hydro
uv run python main.py calc-peak
```

## 4. 後処理

```powershell
uv run python main.py post-header
uv run python main.py post-value-max
```

## 5. 可視化 GUI

```powershell
uv run python main.py post
```

> 補足
> - `--dry-run` を付けると設定のみ検証できます。
> - 途中でエラーになった場合は [トラブルシューティング](troubleshooting.md) を参照してください。

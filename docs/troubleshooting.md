# トラブルシューティング

## よくあるエラー

### 設定ファイルが見つからない

```
設定ファイルが見つかりません: ...
```

- `project.toml` のパスが正しいか確認してください。

### 入力ファイルが見つからない

```
No such file or directory: ...
```

- 設定ファイルの **相対パスの基準** を確認してください。

### RRI_Input.txt の参照がずれる

```
RRI_Input.txt が見つかりません: ...
```

- `project.toml` の `[rri].input` が有効になっているか確認してください。
- `makeRiver5.toml` に `[inputs]/[params]` がある場合は **RRI_Input.txt を使わず**に動きます。

### landuse のヘッダーが一致しない

```
勾配と landuse のヘッダが一致しません
```

- grad と landuse の **ncols / nrows / cellsize** が一致しているか確認してください。

### post-header のヘッダー雛形が足りない

```
fine ヘッダー雛形ファイルが存在しません
```

- fine 格子が必要な場合のみ `fine_header_template` を指定してください。

### parquet ライブラリがない

```
Missing optional dependency 'pyarrow' ...
```

- `pyarrow` または `fastparquet` を追加で導入してください。

## それでも解決しない場合

- `--dry-run` で設定だけ確認して原因を切り分けてください。
- どの設定ファイルを参照しているか、コンソール出力を確認してください。

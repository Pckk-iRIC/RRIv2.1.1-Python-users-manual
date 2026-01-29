# post-value-max

post-header 出力の `.asc` を使って **最大値ラスター** を生成します。  
prefix 単位で最大値を集約し、`value_max/` に出力します。

## 実行

```powershell
uv run python main.py post-value-max
```

### 主なオプション

- `--project`  
  - `project.toml` を明示指定します（未指定ならカレントの `project.toml`）。
- `--config`  
  - `post_value_max.toml` を直接指定します。
- `--dry-run`  
  - 設定確認のみ行い、処理は実行しません。

## 設定ファイルの読み方

`project.toml` の `[post_value_max].config` を参照します。

```toml
[post_value_max]
config = "data/tools_config/post_value_max/post_value_max.toml"
```

## 入力

- **asc_dir**  
  - post-header の出力ディレクトリを指定します。
  - サブディレクトリも再帰的に探索します。

## 出力

- **value_max_dir** に最大値ラスターを出力します。
- ファイル名は `prefix_XXXXXX.asc` 形式になります。

## 追加パラメータ

- **workers**  
  - prefix 単位の並列数です（1 で逐次実行）。\n
  - CPU/メモリに応じて増やせます（最大 4 推奨）。

## 設定例（post_value_max.toml）

```toml
[inputs]
asc_dir = "data/tools_output/ouptut_kiku-20260126"

[outputs]
value_max_dir = "data/tools_output/kiku_value_max"

[params]
workers = 2
```

## 補足

- `--dry-run` で設定確認のみ行えます。

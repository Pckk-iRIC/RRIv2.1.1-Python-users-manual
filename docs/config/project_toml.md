# project.toml

`project.toml` は **全体設定の入口** です。各ツールの設定ファイルパスを指定します。  
詳細なパラメータは **各 CLI ページ**で説明します。

## 最小例

```toml
[rri]
input = "data/tools_config/common/RRI_Input.txt"

[scale_free]
config = "data/tools_config/scaleFree/scaleFree.toml"

[landuse]
rules = "data/tools_config/landuse_from_grad/landuse_rules.csv"
output = "data/tools_output/landuse_from_grad/landuse_from_grad.asc"

[make_river5]
config = "data/tools_config/makeRiver5/makeRiver5.toml"
```

## 注意点

- 相対パスは `project.toml` の場所が基準です。\n
- `rri.input` が指定されている場合、`makeRiver5` は **RRI_Input.txt を優先**します。\n
  詳細は [makeRiver5](../cli/make_river5.md) を参照してください。

# tools_config の使い方

`data/tools_config/` には各ツールの **設定テンプレート** を置きます。  
ここで編集した設定ファイルのパスを `project.toml` から参照します。

## 使い方

1. 目的のツールの設定ファイルを編集  
2. `project.toml` にパスを設定  
3. `main.py` から実行

## 運用ルール

- **設定は `project.toml` を入口にする**  
- **TOML/TXT 両対応のツールは両方置いてよい**  
- **実データを使う場合はパスを書き換える**

## 詳細は CLI ページへ

ツール固有の設定は、それぞれの CLI ページにまとめています。

- [scaleFree](../cli/scalefree.md)
- [landuse 付与](../cli/landuse.md)
- [makeRiver5](../cli/make_river5.md)
- [calcHydro](../cli/calc_hydro.md)
- [calcPeak](../cli/calc_peak.md)
- [post-header](../cli/post_header.md)
- [post-value-max](../cli/post_value_max.md)

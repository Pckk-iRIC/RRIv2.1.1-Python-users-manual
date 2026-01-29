# 目的別ガイド

CLI/GUI の入口が多いので、**利用シーンごとに何を使うか** を整理します。

## 1. 解析を始めるための入力データを作りたい

- **GUI（初心者向け）**: [入力データ作成 (pre)](gui/preproc.md)  
  - メッシュ生成 / 標高付与 / 土地利用区分コード付与 / Shapefile→ASCII
- **CLI（大量処理向け）**: [scaleFree](cli/scalefree.md)  
- DEM/dir/acc を **スケールアップ（粗い格子化）** して派生データを作成  
  - landuse 付与や河道—斜面の接続情報にも使われる

## 2. landuse だけを更新したい

- **CLI（単体）**: [landuse 付与](cli/landuse.md)
- **CLI（一括）**: [scaleFree + landuse](cli/scalefree_landuse.md)

## 3. RRI 実行前に河道パラメータを作りたい

- **makeRiver5**: [makeRiver5](cli/make_river5.md)  
  - DEM/ACC/DIR から **width / depth / height** を生成

## 4. RRI 実行後の out を集計したい

- **calcHydro**: [calcHydro](cli/calc_hydro.md)  
  - `out` から地点ごとの時系列を抽出
- **calcPeak**: [calcPeak](cli/calc_peak.md)  
  - `out` からピーク値を抽出

## 5. RRI 実行後の out を可視化したい

- **GUI**: [結果可視化 (post)](gui/postproc.md)
- **CLI**: [post-header](cli/post_header.md) → [post-value-max](cli/post_value_max.md)

## 6. 設定ファイルの場所を知りたい

- [設定の概要](config/index.md)

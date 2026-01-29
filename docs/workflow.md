# ワークフロー全体像

RRI v2.1.1 Python版は、次の流れで利用することを想定しています。

1. **入力データ作成（pre GUI）**
2. **前処理（scaleFree / landuse / makeRiver5 / calcHydro / calcPeak）**
3. **RRI 本体実行（Fortran）で `out` 生成**
4. **後処理（post-header / post-value-max / post GUI）**

## 代表的な流れ（例）

- 入力データ作成: `python main.py pre`
- scaleFree + landuse: `python main.py scalefree-landuse`
- makeRiver5: `python main.py make-river5`
- calcHydro / calcPeak: `python main.py calc-hydro` / `python main.py calc-peak`
- RRI 本体で `out` を作成
- ヘッダー付与: `python main.py post-header`
- 最大値ラスター: `python main.py post-value-max`
- 可視化 GUI: `python main.py post`

> 補足
> - `--dry-run` を付けると **実行せず設定だけ確認** できます。
> - 前処理の出力や RRI 本体の `out` を、後処理の入力に使います。

## どこから手を付ければよい？

- 初めての方は [クイックスタート](quickstart.md) を先に進めてください。
- GUI 操作が中心の方は [GUI](gui/preproc.md) を参照してください。
- CLI 操作が中心の方は [CLI](cli/index.md) を参照してください。

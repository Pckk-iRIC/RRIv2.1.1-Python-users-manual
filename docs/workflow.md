# ワークフロー全体像

RRI v2.1.1 Python版は、次の流れで利用することを想定しています。

1. **入力データ作成（pre GUI）**
2. **RRI 本体実行（Fortran）で `out` 生成**
3. **派生データ作成（scaleFree / landuse / makeRiver5）**
4. **後処理（post-header / post-value-max / post GUI）**
5. **解析（calcHydro / calcPeak）**

## 代表的な流れ（例）

- 入力データ作成: `python main.py pre`
- RRI 本体で `out` を作成
- 派生データ作成: `python main.py scalefree-landuse` / `python main.py make-river5`
- ヘッダー付与: `python main.py post-header`
- 最大値ラスター: `python main.py post-value-max`
- 可視化 GUI: `python main.py post`
- calcHydro / calcPeak: `python main.py calc-hydro` / `python main.py calc-peak`

> 補足
> - `--dry-run` を付けると **実行せず設定だけ確認** できます。
> - 派生データ（scaleFree / landuse / makeRiver5）や RRI 本体の `out` を、後処理や解析の入力に使います。

## どこから手を付ければよい？

- 初めての方は [クイックスタート](quickstart.md) を先に進めてください。
- GUI 操作が中心の方は [GUI](gui/preproc.md) を参照してください。
- CLI 操作が中心の方は [CLI](cli/index.md) を参照してください。

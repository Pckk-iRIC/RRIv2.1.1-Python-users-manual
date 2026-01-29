# インストール

このプロジェクトは Windows 環境での利用を想定しています。

## 必要なもの

- Python 3.13 系
- uv（Python パッケージ管理）

## セットアップ手順（例）

1. リポジトリを取得
2. 依存関係を同期

### リポジトリ取得（アクセス申請が必要）
RRIv2.1.1-Python は **非公開リポジトリ** です。利用にはアクセス権が必要です。

1. **Pckk 関係者のみ**アクセス可能です。
2. GitHub アカウント作成のうえ、**リポジトリ管理者へアクセス申請**してください。
3. 管理者は本 Organization（Pckk-iRIC）と同じため、**Pckk-iRIC 管理者へお問い合わせ**ください。
4. 対象リポジトリ: [Pckk-solvers/RRIv2.1.1-Python](https://github.com/Pckk-solvers/RRIv2.1.1-Python)

```powershell
uv sync
```

3. 動作確認（ヘルプ表示）

```powershell
uv run python main.py --help
```

> 注意
> - 依存関係の導入に失敗する場合は、社内プロキシや権限を確認してください。
> - GUI を使う場合は、Windows の表示スケール設定により文字が小さくなる場合があります。

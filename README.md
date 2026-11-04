# countup

## 開発環境

Dev Container（Go & PostgreSQL）で開発します。

- **app**: Go 1.27（Debian trixie）。Node.js と Claude Code も入っています。
- **db**: PostgreSQL（`postgres:latest`）。app コンテナからは `localhost:5432` で接続できます。

### セットアップ

1. リポジトリをクローンします。
2. `.devcontainer/.env.example` を `.devcontainer/.env` にコピーし、値を入れます。

   ```sh
   cp .devcontainer/.env.example .devcontainer/.env
   ```

   | 変数 | 内容 |
   | --- | --- |
   | `POSTGRES_USER` | DB ユーザー名 |
   | `POSTGRES_PASSWORD` | DB パスワード |
   | `POSTGRES_DB` | DB 名 |
   | `POSTGRES_HOSTNAME` | DB ホスト名（通常は `localhost`） |

3. VS Code でフォルダを開き、「Reopen in Container」でコンテナを起動します。

`.devcontainer/.env` は `.gitignore` で除外されているため、コミットされません。

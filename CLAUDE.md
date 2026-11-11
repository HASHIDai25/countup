# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project status

This repository is newly initialized: it contains only the dev container configuration (`.devcontainer/`) and a setup-focused `README.md`. There is no application code, Go module, build script, or test yet. Update this file with build/test/lint commands and architecture notes once code is added.

`README.md` is written in Japanese; keep it in Japanese when updating it.
## 概要
開発を進める上で遵守すべき標準ルールを定義します。

## プロジェクト構造
本リポジトリはcountup（行動記録・積み上げツール）アプリケーション専用リポジトリです。

### ドキュメントの分類

#### 1.永続的ドキュメント('docs/')
アプリケーション全体の「**何を作るか**」「**どう作るか**」を定義する恒久的なドキュメント。
アプリケーションの基本設計や方針が変わらない限り更新されません。

- **product-requirements.md**　- プロダクト要求定義書
    - プロダクトビジョンと目的
    - ターゲットユーザーと課題・ニーズ
    - 主要な機能一覧
    - 成功の定義
    - ビジネス要件
    - ユーザーストーリー
    - 受け入れ条件
    - 機能要件
    - 非機能要件

- **functional-design.md** - 機能設計書
    - 機能ごとのアーキテクチャ
    - システム構成図
    - データモデル定義書（ER図含む）
    - コンポーネント設計
    - ユースケース図、画面遷移図、ワイヤーフレーム
    - API設計（将来的にバックエンドと連携する場合）

- **architeture.md** - 技術仕様書
    - テクノロジースタック
    - 開発ツールと手法
    - 技術的制約と要件
    - パフォーマンス要件

- **repository-structure.md** - リポジトリ構造定義書
    - フォルダ・ファイル構成
    - ディレクトリの役割
    - ファイル配置ルール

- **development-guidelines.md** - 開発ガイドライン
    - コーディング規約
    - 命名規則
    - スタイリング規約
    - テスト規約
    - Git規約

- **glossary.md** - ユビキタス言語定義
    - ドメイン用語の定義
    - ビジネス用語の定義
    - UI/UX用語の定義
    - 英語・日本語対応表
    - コード上の命名規則

#### 2. 作業単位のドキュメント('.steering/[YYYYMMDD]-[開発タイトル]/')
特定の開発作業における「**今回何をするか**」を定義する一時的なステアリングファイル
作業完了後は参照用として保存されますが、新しい作業では新しいディレクトリを作成します。

- **requirements.md** - 今回の作業の要求内容
    - 変更・追加する機能の説明
    - ユーザーストーリー
    - 受け入れ条件
    - 製薬事項

- **design.md** - 変更内容の設計
    - 実装アプローチ
    - 変更するコンポーネント
    - データ構造の変更
    - 影響範囲の分析

- **tasklist.md** - タスクリスト
    - 具体的な実装タスク
    - タスクの進捗状況
    - 完了条件

### ステアリングディレクトリの命名規則
```
.steering/[YYYYMMDD]-[開発タイトル]/
```

**例:**
- '.steering/20261014-initial-implementation/'
- '.steering/20261015-add-tag-feature/'
- '.steering/20261020-fix-filter-bag/'
- '.steering/20261025-improve-performance/'

## 開発プロセス

### 初回セットアップ時の手順

#### 1. フォルダ作成
```bash
mkdir -p docs
mkdir -p .steering
```

#### 2. 永続的ドキュメントの作成（'docs/'）
#### 3. 初回実装用のステアリングファイル作成
#### 4. 環境セットアップ
#### 5. 実装開始
#### 6. 品質チェック



## Development environment

The project runs in a Dev Container based on the "Go & PostgreSQL" template:

- **app** service: `mcr.microsoft.com/devcontainers/go` image (Go 1.27, Debian trixie), with Node.js and Claude Code added as features. The repo is mounted at `/workspaces/countup`.
- **db** service: `postgres:latest`, data persisted in the `postgres-data` volume.
- The app container uses `network_mode: service:db`, so PostgreSQL is reachable from the app at `localhost:5432`.
- To reach a port from the host, add it to `forwardPorts` in `devcontainer.json`, not to `ports` in `docker-compose.yml`. Nothing is forwarded by default.
- Database credentials come from `.devcontainer/.env` (`POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`, `POSTGRES_HOSTNAME`), which is loaded as environment variables into both containers. Read connection settings from these env vars rather than hardcoding them.
- `.devcontainer/.env` is git-ignored. On a fresh clone, copy `.devcontainer/.env.example` to `.devcontainer/.env` and fill in the values before starting the container.

## Git

The workspace is mounted with root ownership, so git fails with "detected dubious ownership" unless the repo is marked safe. `postCreateCommand` in `devcontainer.json` does this automatically on container creation; if it is missing (e.g. in a container created before that change), run:

```
git config --global --add safe.directory /workspaces/countup
```

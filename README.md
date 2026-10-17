# codespaces-envについて

## Github CodeSpacesでClaude Codeを用いて開発するための設定
- 開発環境の設定を`.devcontainer/devcontainer.json`に構築
```json
{
  "image": "mcr.microsoft.com/devcontainers/base:ubuntu-24.04",
  "features": {
    "ghcr.io/anthropics/devcontainer-features/claude-code:1.0": {},
    "ghcr.io/devcontainers/features/node:1": {
      "version": "24",
      "pnpmVersion": "latest"
    },
    "ghcr.io/devcontainers/features/python:1": {
      "version": "3.14",
      "toolsToInstall": "uv"
    }
  },
  "containerEnv": {
    "TZ": "Asia/Tokyo",
    "UV_LINK_MODE": "copy"
  }
}
```
- 使用言語・パッケージマネージャー
  - Node.js 24 + pnpm
  - Python 3.14 + uv（`UV_LINK_MODE=copy`はCodespacesでのハードリンク警告を回避するための設定）
- Dockerは含まれていない。DB等をコンテナで動かす場合は`features`に`"ghcr.io/devcontainers/features/docker-in-docker:2": {}`を追加する
- 設定変更後はコマンドパレットから「Codespaces: Rebuild Container」で反映する
- ローカルPC、または Codespace 内のターミナルで、コマンド`claude setup-token` を実行しトークンを出力。トークン形式は`sk-ant-oat01-...`
- 右上のプロフィール → Settings → 左メニュー Codespaces → 「Codespaces secrets」→ New secret → 名前 CLAUDE_CODE_OAUTH_TOKEN、値にトークンを入れ、「Repository access」で使うリポジトリを選択
- CodespacesのターミナルでClaude Codeを起動

## 環境変数の扱い
- 秘密情報（トークン・APIキー・DB パスワード等）はCodespaces Secrets（GitHub 設定画面）に保存すること。
- チームで共有してよい設定値（NODE_ENV、TZなど）は、`.devcontainer/devcontainer.json` の containerEnvに保存（リビルドは必要）。

## ハンズオン
- `docs/handson/`に、この環境で手を動かしながら学ぶためのメモを置いている。上から順に進める
  - [Git 超入門ハンズオン](docs/handson/git-handson.md)：このリポジトリを使って、branch / add / commit / push などGitの基本操作を覚える
  - [Claude Code 超入門ハンズオン](docs/handson/claude-code-handson.md)：Claude Codeに指示を出しながら、Next.js + MapLibre GL JSで地図に図形を描けるWeb-GISアプリを作る

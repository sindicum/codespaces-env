# codespaces-env

Github CodeSpacesで開発するための環境設定
- デフォルトでNode.js、Python、Git環境は構築されている。
- Claude Codeの設定を`.devcontainer/devcontainer.json`に構築
```json
{
  "features": {
    "ghcr.io/anthropics/devcontainer-features/claude-code:1.0": {}
  }
}
```
- ローカルPC、または Codespace 内で claude setup-token を実行しトークンを出力。トークン形式は`sk-ant-oat01-...`
- 右上のプロフィール → Settings → 左メニュー Codespaces → 「Codespaces secrets」→ New secret → 名前 CLAUDE_CODE_OAUTH_TOKEN、値にトークンを入れ、「Repository access」で使うリポジトリを選択
- CodespacesのターミナルでClaude Codeを起動
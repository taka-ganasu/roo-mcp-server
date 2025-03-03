# Roo MCP サーバー

これは、Roo Code のための MCP サーバーです。このサーバーは、基本的なツールを提供します。

## 前提条件

- [Deno](https://deno.com/) がインストールされていること

## 起動方法

```bash
# サーバーの起動
deno task start

# 開発モードでの起動（変更を監視して自動再起動）
deno task dev
```

## テスト実行

```bash
# テストの実行
deno task test
```

## 提供するツール

### getStringLength

文字列の長さを返すツール

**パラメータ:**

- `input` (string, 必須): 長さを計算する文字列

**使用例:**

```
use_mcp_tool(
  server_name="local",
  tool_name="getStringLength",
  arguments={
    "input": "こんにちは世界"
  }
)
```

### getGitHubRepoInfo

GitHub リポジトリの情報を取得するツール

**パラメータ:**

- `owner` (string, 必須): リポジトリのオーナー（ユーザー名または組織名）
- `repo` (string, 必須): リポジトリ名

**使用例:**

```
use_mcp_tool(
  server_name="local",
  tool_name="getGitHubRepoInfo",
  arguments={
    "owner": "denoland",
    "repo": "deno"
  }
)
```

### getGitHubRepoContents

GitHub リポジトリのコンテンツ（ファイルやディレクトリ）を取得するツール

**パラメータ:**

- `owner` (string, 必須): リポジトリのオーナー（ユーザー名または組織名）
- `repo` (string, 必須): リポジトリ名
- `path` (string, オプション): ファイルまたはディレクトリのパス（デフォルト: ルートディレクトリ）
- `ref` (string, オプション): コミット/ブランチ/タグの名前（デフォルト: デフォルトブランチ）

### getGitHubIssues

GitHub リポジトリのイシューを取得するツール

**パラメータ:**

- `owner` (string, 必須): リポジトリのオーナー（ユーザー名または組織名）
- `repo` (string, 必須): リポジトリ名
- `state` (string, オプション): イシューの状態（open, closed, all）（デフォルト: open）
- `per_page` (number, オプション): 取得するイシューの数（最大: 100）（デフォルト: 30）

### getGitHubCommits

GitHub リポジトリのコミット履歴を取得するツール

**パラメータ:**

- `owner` (string, 必須): リポジトリのオーナー（ユーザー名または組織名）
- `repo` (string, 必須): リポジトリ名
- `path` (string, オプション): コミットをフィルタするパス（デフォルト: すべてのファイル）
- `per_page` (number, オプション): 取得するコミットの数（最大: 100）（デフォルト: 30）

## Roo Code への登録方法

1. サーバーを起動します: `deno task start`
2. Roo Cline の設定ファイルを編集します: `~/Library/Application Support/Code/User/globalStorage/rooveterinaryinc.roo-cline/settings/cline_mcp_settings.json`
3. 以下の設定を追加します:

```json
{
  "mcpServers": {
    "local": {
      "command": "deno",
      "args": [
        "run",
        "--allow-net",
        "--allow-env",
        "--allow-read",
        "/path/to/src/server.ts"
      ],
      "env": {},
      "disabled": false,
      "alwaysAllow": []
    }
  }
}
```

4. パスを実際の src/server.ts のパスに置き換えてください
5. Roo Cline を再起動して設定を反映させます

登録後、Roo Code から提供されるツールにアクセスできるようになります。

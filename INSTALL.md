# colleague.skill インストールガイド

---

## プラットフォームを選択

### A. Claude Code（推奨）

本プロジェクトは公式 [AgentSkills](https://agentskills.io) 標準に準拠しており、リポジトリ全体が skill ディレクトリになっています。Claude の skills ディレクトリにクローンするだけで使えます：

```bash
# ⚠️ git リポジトリのルートディレクトリで実行してください！
cd $(git rev-parse --show-toplevel)

# 方法 1：現在のプロジェクトにインストール
mkdir -p .claude/skills
git clone https://github.com/titanwings/colleague-skill .claude/skills/create-colleague

# 方法 2：グローバルにインストール（すべてのプロジェクトで使用可能）
git clone https://github.com/titanwings/colleague-skill ~/.claude/skills/create-colleague
```

Claude Code で `/create-colleague` と入力すれば起動します。

生成された同僚 Skill はデフォルトで `./colleagues/` ディレクトリに書き出されます。

---

### B. OpenClaw

```bash
# OpenClaw の skills ディレクトリにクローン
git clone https://github.com/titanwings/colleague-skill ~/.openclaw/workspace/skills/create-colleague
```

OpenClaw セッションを再起動し、`/create-colleague` と入力すれば起動します。

---

## 依存関係のインストール

```bash
# 基本（Python 3.9+）
pip3 install pypinyin        # 中国語名からピンイン slug への変換（任意だが推奨）

# Feishu（飛書）ブラウザ方式（社内ドキュメント／ログインが必要なドキュメント）
pip3 install playwright
playwright install chromium  # chromium のみインストールすればOK、完全な Chrome は不要

# Feishu（飛書）MCP 方式（会社承認済みドキュメント、App Token 経由で読み取り）
npm install -g feishu-mcp    # Node.js 16+ が必要

# その他のフォーマット対応（任意）
pip3 install python-docx     # Word .docx をテキストに変換
pip3 install openpyxl        # Excel .xlsx を CSV に変換
```

### プラットフォーム方式選択ガイド

| シナリオ | 推奨方式 |
|------|---------|
| Feishu（飛書）ユーザー、App 権限あり | `feishu_auto_collector.py` |
| Feishu（飛書）社内ドキュメント（App 権限なし）| `feishu_browser.py` |
| Feishu（飛書）手動リンク指定 | `feishu_mcp_client.py` |
| DingTalk（釘釘）ユーザー | `dingtalk_auto_collector.py` |
| DingTalk（釘釘）メッセージ取得失敗時 | 手動スクリーンショット → 画像アップロード |
| Slack ユーザー | `slack_auto_collector.py` |

**Feishu（飛書）自動収集の初期設定**：
```bash
python3 tools/feishu_auto_collector.py --setup
# Feishu（飛書）オープンプラットフォームの App ID と App Secret を入力
```

**DingTalk（釘釘）自動収集の初期設定**：
```bash
python3 tools/dingtalk_auto_collector.py --setup
# DingTalk（釘釘）オープンプラットフォームの AppKey と AppSecret を入力
# 初回実行時は --show-browser パラメータを追加して DingTalk（釘釘）ログインを完了させる
```

**Feishu（飛書）MCP 初期設定**（手動リンク指定時に使用）：
```bash
python3 tools/feishu_mcp_client.py --setup
```

**Feishu（飛書）ブラウザ方式**（初回使用時にログイン画面が表示され、以降はログイン状態が自動的に再利用されます）：
```bash
python3 tools/feishu_browser.py \
  --url "https://xxx.feishu.cn/wiki/xxx" \
  --show-browser    # 初回使用時にこのパラメータを追加、ログイン後は不要
```

**Slack 自動収集の初期設定**：
```bash
pip3 install slack-sdk
python3 tools/slack_auto_collector.py --setup
# プロンプトに従って Bot User OAuth Token（xoxb-...）を入力
```

> Slack の詳細設定については下記の「[Slack 自動収集設定](#slack-自動収集設定)」セクションを参照してください

---

## Slack 自動収集設定

### 前提条件

- Python 3.9+
- Slack Workspace（App をインストールするには**管理者権限**が必要、または管理者にインストールを依頼してください）
- `pip3 install slack-sdk`

> **無料版 Workspace の制限**：直近 **90 日間**のメッセージのみアクセス可能です。有料版（Pro / Business+ / Enterprise）にはこの制限はありません。

---

### ステップ 1：Slack App を作成

1. [https://api.slack.com/apps](https://api.slack.com/apps) にアクセス → **Create New App**
2. **From scratch** を選択
3. App Name を入力（例：`colleague-skill-bot`）、対象の Workspace を選択 → **Create App**

---

### ステップ 2：Bot Token Scopes を設定

**OAuth & Permissions** → **Bot Token Scopes** → **Add an OAuth Scope** に進み、以下の権限を追加します：

| Scope | 用途 |
|-------|------|
| `users:read` | ユーザーリストの検索（必須） |
| `channels:read` | public channels の一覧表示（必須） |
| `channels:history` | public channel の履歴メッセージの読み取り（必須） |
| `groups:read` | private channels の一覧表示（必須） |
| `groups:history` | private channel の履歴メッセージの読み取り（必須） |
| `mpim:read` | グループ DM の一覧表示（任意） |
| `mpim:history` | グループ DM の履歴メッセージの読み取り（任意） |
| `im:read` | DM の一覧表示（任意、ユーザー認可が必要） |
| `im:history` | DM の履歴メッセージの読み取り（任意、ユーザー認可が必要） |

---

### ステップ 3：App を Workspace にインストール

1. **OAuth & Permissions** ページのまま、**Install to Workspace** をクリック
2. Workspace 管理者の承認後、**Bot User OAuth Token**（形式：`xoxb-...`）をコピー

---

### ステップ 4：Bot を対象チャンネルに追加

Bot は**参加済み**のチャンネルのみ読み取り可能です。Slack で各対象チャンネルに入り、以下を入力します：

```
/invite @your-bot-name
```

> ヒント：対象の同僚がどのチャンネルにいるかわからない場合は、まず招待せずに収集を実行してください。スクリプトが Bot が参加しているチャンネルを表示するので、その後で追加招待できます。

---

### ステップ 5：設定ウィザードを実行

```bash
python3 tools/slack_auto_collector.py --setup
```

プロンプトに従って Bot Token を貼り付けると、スクリプトが自動的に検証し `~/.colleague-skill/slack_config.json` に保存します。

設定が成功すると以下が表示されます：
```
Token を検証中 ... OK
  Workspace：Your Company，Bot：colleague-skill-bot

✅ 設定を /Users/you/.colleague-skill/slack_config.json に保存しました
```

---

### ステップ 6：同僚データを収集

```bash
# 基本的な使い方（同僚の中国語名または英語ユーザー名を入力）
python3 tools/slack_auto_collector.py --name "張三"
python3 tools/slack_auto_collector.py --name "john.doe"

# 出力ディレクトリを指定
python3 tools/slack_auto_collector.py --name "張三" --output-dir ./knowledge/zhangsan

# 収集量を制限（大規模 Workspace ではまず少量でテストすることを推奨）
python3 tools/slack_auto_collector.py --name "張三" --msg-limit 500 --channel-limit 20
```

出力ファイル：
```
knowledge/張三/
├── messages.txt            # 重要度別に分類されたメッセージ記録
└── collection_summary.json # 収集サマリー（ユーザー情報、チャンネルリスト、日時）
```

---

### よくあるエラーと解決方法

| エラー | 原因 | 解決方法 |
|------|------|------|
| `missing_scope: channels:history` | Bot Token に権限が不足 | api.slack.com → OAuth & Permissions で該当 Scope を追加し、App を再インストール |
| `invalid_auth` | Token が無効または失効 | `--setup` を再実行して新しい Token を設定 |
| `not_in_channel` | Bot がそのチャンネルに未参加 | Slack で `/invite @bot` を実行して Bot を招待 |
| ユーザーが見つからない | 名前のスペルが間違っている | 英語ユーザー名（例：`john.doe`）または Slack display name を使用 |
| メッセージが 90 日分のみ | 無料版の制限 | Workspace をアップグレードするか、手動でスクリーンショットを補足 |
| レート制限（429）| リクエストが多すぎる | スクリプトが自動的に待機してリトライするため、手動対応は不要 |

## クイック検証

```bash
cd ~/.claude/skills/create-colleague   # またはプロジェクト内の .claude/skills/create-colleague

# Feishu（飛書）パーサーをテスト
python3 tools/feishu_parser.py --help

# Slack コレクターをテスト
python3 tools/slack_auto_collector.py --help

# メールパーサーをテスト
python3 tools/email_parser.py --help

# 既存の同僚 Skill を一覧表示
python3 tools/skill_writer.py --action list --base-dir ./colleagues
```

---

## ディレクトリ構成の説明

本プロジェクトのリポジトリ全体が一つの skill ディレクトリです（AgentSkills 標準フォーマット）：

```
colleague-skill/        ← .claude/skills/create-colleague/ にクローン
├── SKILL.md            # skill エントリーポイント（公式 frontmatter）
├── prompts/            # 分析・生成用のプロンプトテンプレート
├── tools/              # Python ツールスクリプト
├── docs/               # ドキュメント（PRD など）
│
└── colleagues/         # 生成された同僚 Skill の保存先（.gitignore で除外）
    └── {slug}/
        ├── SKILL.md            # 完全な Skill（Persona + Work）
        ├── work.md             # 仕事能力のみ
        ├── persona.md          # 人物の性格のみ
        ├── meta.json           # メタデータ
        ├── versions/           # 履歴バージョン
        └── knowledge/          # 元の素材アーカイブ
```

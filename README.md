<div align="center">

# colleague.skill

> *「おまえらAI屋はコードベースの裏切り者だ――フロントエンドを殺しておいて、次はバックエンド、QA、運用、セキュリティ、チップ設計、最後には自分たち自身と全人類まで来るつもりか」*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://python.org)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![AgentSkills](https://img.shields.io/badge/AgentSkills-Standard-green)](https://agentskills.io)

[![Discord](https://img.shields.io/badge/Discord-Join%20Community-5865F2?logo=discord&logoColor=white)](https://discord.gg/aRjmJBdK)

<br>

同僚が辞めて、メンテされないドキュメントの山だけが残った？<br>
インターンが去って、空の机と半端なプロジェクトだけが残った？<br>
メンターが卒業して、コンテキストと経験のすべてを持っていった？<br>
パートナーが異動して、築いたケミストリーが一夜でリセットされた？<br>
前任者が引き継いで、3年分を3ページに凝縮しようとした？<br>

**冷たい別れを温かい Skill に変えよう――サイバー不死へようこそ！**

<br>

ソース資料（飞书メッセージ、钉钉ドキュメント、Slackメッセージ、メール、スクリーンショット）と<br>
その人に対するあなたの主観的な説明を提供するだけで<br>
**実際にその人のように働くAI Skill** が手に入ります

[対応ソース](#対応データソース) · [インストール](#インストール) · [使い方](#使い方) · [デモ](#デモ) · [詳細インストール](INSTALL.md) · [💬 Discord](https://discord.gg/aRjmJBdK)

[**中文**](docs/lang/README_ZH.md) · [**Español**](docs/lang/README_ES.md) · [**Deutsch**](docs/lang/README_DE.md) · [**日本語**](docs/lang/README_JA.md) · [**Русский**](docs/lang/README_RU.md) · [**Português**](docs/lang/README_PT.md)

</div>

---

> 🆕 **2026.04.13 アップデート** — **dot-skill ロードマップ公開！** colleague.skill は **dot-skill** へと進化します――同僚だけでなく、誰でも蒸留できるようになります。マルチモーダル出力、Skillエコシステムなど、続々登場予定。
>
> 👉 **[ロードマップ全文を読む](ROADMAP.md)** · **[💬 Discord](https://discord.gg/aRjmJBdK)**
>
> Issueの整理、マイルストーンの追加、[公開プロジェクトボード](https://github.com/users/titanwings/projects/1)の設置も行いました。コミュニティからの貢献を歓迎します――`good-first-issue` ラベルをチェックしてください！

> 🆕 **2026.04.07 アップデート** — dot-skill リミックスに対するコミュニティの熱意が素晴らしいです！コミュニティギャラリーを構築しました――PR歓迎！
>
> 任意の Skill やメタ Skill を共有し、あなた自身のGitHubリポジトリに直接トラフィックを誘導できます。仲介者なし。
>
> 👉 **[titanwings.github.io/colleague-skill-site](https://titanwings.github.io/colleague-skill-site/)**
>
> 現在掲載中: 户晨风.skill · 峰哥亡命天涯.skill · 罗翔.skill など

---

Created by [@titanwings](https://github.com/titanwings) | Powered by Shanghai AI Lab · AI Safety Center

## 対応データソース

> これはまだ colleague.skill のベータ版です――対応ソースは今後追加予定です、お楽しみに！

| ソース | メッセージ | ドキュメント / Wiki | スプレッドシート | 備考 |
|--------|:--------:|:-----------:|:------------:|-------|
| 飞书（自動） | ✅ API | ✅ | ✅ | 名前を入力するだけで完全自動 |
| 钉钉（自動） | ⚠️ ブラウザ | ✅ | ✅ | 钉钉APIはメッセージ履歴に対応していません |
| Slack（自動） | ✅ API | — | — | 管理者によるBot導入が必要。無料プランは90日間の制限あり |
| WeChatチャット履歴 | ✅ SQLite | — | — | 現在不安定、以下のオープンソースツールの使用を推奨 |
| PDF | — | ✅ | — | 手動アップロード |
| 画像 / スクリーンショット | ✅ | — | — | 手動アップロード |
| 飞书 JSONエクスポート | ✅ | ✅ | — | 手動アップロード |
| メール `.eml` / `.mbox` | ✅ | — | — | 手動アップロード |
| Markdown | ✅ | ✅ | — | 手動アップロード |
| テキスト直接貼り付け | ✅ | — | — | 手動入力 |

### 推奨WeChatチャットエクスポートツール

これらは独立したオープンソースプロジェクトです――本プロジェクトにそれらのコードは含まれていませんが、パーサーはそれらのエクスポート形式に対応しています。WeChat自動復号は現在不安定なため、これらのオープンソースツールでチャット履歴をエクスポートし、本プロジェクトに貼り付けまたはインポートすることを推奨します：

| ツール | プラットフォーム | 説明 |
|------|----------|-------------|
| [WeChatMsg](https://github.com/LC044/WeChatMsg) | Windows | WeChatチャット履歴エクスポート、複数形式対応 |
| [PyWxDump](https://github.com/xaoyaoo/PyWxDump) | Windows | WeChatデータベース復号＆エクスポート |
| [留痕 (Liuhen)](https://github.com/greyovo/留痕) | macOS | WeChatチャット履歴エクスポート（Macユーザー推奨） |

> ツール推薦は [@therealXiaomanChu](https://github.com/therealXiaomanChu) より。すべてのオープンソース作者に感謝――サイバー不死を共に！

---

## インストール

### Claude Code

> **重要**: Claude Code は **gitリポジトリルート** の `.claude/skills/` からスキルを探します。正しい場所で実行してください。

```bash
# 現在のプロジェクトにインストール（gitリポジトリルートで実行）
mkdir -p .claude/skills
git clone https://github.com/titanwings/colleague-skill .claude/skills/create-colleague

# またはグローバルにインストール（すべてのプロジェクトで利用可能）
git clone https://github.com/titanwings/colleague-skill ~/.claude/skills/create-colleague
```

### OpenClaw

```bash
git clone https://github.com/titanwings/colleague-skill ~/.openclaw/workspace/skills/create-colleague
```

### 依存関係（オプション）

```bash
pip3 install -r requirements.txt
```

> 飞书/钉钉/Slack自動収集にはアプリ資格情報が必要です。詳細は [INSTALL.md](INSTALL.md) を参照してください。

---

## 使い方

Claude Code で以下を入力：

```
/create-colleague
```

プロンプトに従ってください：エイリアス、会社/レベル（例: `バイトダンス L2-1 バックエンドエンジニア`）、性格タグを入力し、データソースを選択します。すべてのフィールドはスキップ可能です――説明だけでもSkillを生成できます。

作成後、`/{slug}` で同僚Skillを呼び出せます。

### コマンド

| コマンド | 説明 |
|---------|-------------|
| `/list-colleagues` | すべての同僚Skillを一覧表示 |
| `/{slug}` | フルSkillを呼び出し（ペルソナ + 業務） |
| `/{slug}-work` | 業務能力のみ |
| `/{slug}-persona` | ペルソナのみ |
| `/colleague-rollback {slug} {version}` | 以前のバージョンにロールバック |
| `/delete-colleague {slug}` | 削除 |

---

## デモ

> 入力: `バイトダンス L2-1 バックエンドエンジニア、INTJ、責任転嫁マン、バイトダンス風`

**シナリオ1: コードレビュー**

```
User            ❯ このAPI設計をレビューしてもらえますか？

colleague.skill ❯ ちょっと待って――影響範囲は？コンテキストの説明がないんだけど。
                  （読んだ後）N+1クエリ、直して。標準の
                  {code, message, data} レスポンス形式を使って。それが仕様だから、
                  理由は聞かないで。
```

**シナリオ2: 責任のなすりつけ**

```
User            ❯ このバグ、あなたが入れたんですよね？

colleague.skill ❯ タイムライン合ってる？その機能は複数箇所に影響してて、
                  他の変更もあったけど。
```

---

## 機能

### 生成されるSkillの構造

各同僚Skillは連携する2つのパートで構成されます：

| パート | 内容 |
|------|---------|
| **パートA — 業務Skill** | システム、技術基準、ワークフロー、経験 |
| **パートB — ペルソナ** | 5層の性格構造：ハードルール → アイデンティティ → 表現 → 意思決定 → 対人関係 |

実行フロー: `タスク受信 → ペルソナが態度を決定 → 業務Skillが実行 → その人の声で出力`

### 対応タグ

**性格**: 責任感あり · 責任転嫁 · 完璧主義者 · そこそこ主義 · 先延ばし · PUAマスター · 社内政治家 · 上司アピール達人 · 受動的攻撃 · 二転三転 · 寡黙 · 既読スルー …

**企業文化**: バイトダンス風 · アリババ風 · テンセント風 · ファーウェイ風 · バイドゥ風 · 美団風 · 第一原理主義 · OKR重視 · 大企業パイプライン · スタートアップモード

**レベル**: バイトダンス 2-1~3-3+ · アリババ P5~P11 · テンセント T1~T4 · バイドゥ T5~T9 · 美団 P4~P8 · ファーウェイ 13~21 · NetEase · JD · Xiaomi …

### 進化

- **ファイル追加** → 差分を自動分析 → 関連セクションにマージ、既存の結論は上書きしない
- **会話修正** → 「彼はそんなことしない、xxxのはずだ」と言う → 修正レイヤーに書き込み、即座に反映
- **バージョン管理** → 更新ごとに自動アーカイブ、任意の以前のバージョンにロールバック可能

---

## プロジェクト構造

このプロジェクトは [AgentSkills](https://agentskills.io) オープンスタンダードに準拠しています。リポジトリ全体がスキルディレクトリです：

```
create-colleague/
├── SKILL.md              # Skillエントリポイント（公式フロントマター）
├── prompts/              # プロンプトテンプレート
│   ├── intake.md         #   対話ベースの情報収集
│   ├── work_analyzer.md  #   業務能力の抽出
│   ├── persona_analyzer.md #  性格の抽出（タグ翻訳付き）
│   ├── work_builder.md   #   work.md 生成テンプレート
│   ├── persona_builder.md #   persona.md 5層構造
│   ├── merger.md         #   インクリメンタルマージロジック
│   └── correction_handler.md # 会話修正ハンドラ
├── tools/                # Pythonツール
│   ├── feishu_auto_collector.py  # 飞书自動収集
│   ├── feishu_browser.py         # 飞书ブラウザ方式
│   ├── feishu_mcp_client.py      # 飞书 MCP方式
│   ├── dingtalk_auto_collector.py # 钉钉自動収集
│   ├── slack_auto_collector.py   # Slack自動収集
│   ├── email_parser.py           # メールパーサー
│   ├── skill_writer.py           # Skillファイル管理
│   └── version_manager.py        # バージョンアーカイブ＆ロールバック
├── colleagues/           # 生成された同僚Skill（gitignore対象）
├── docs/PRD.md
├── requirements.txt
└── LICENSE
```

---

## 注意事項

- **ソース資料の質 = Skillの質**: チャットログ + 長文ドキュメント > 手動説明のみ
- 優先して収集すべきもの: **本人が書いた** 長文 > **意思決定の返信** > カジュアルなメッセージ
- 飞书自動収集にはアプリBotを関連グループチャットに追加する必要があります
- これはまだデモ版です――バグを見つけたらIssueを立ててください！

---
### 📄 技術レポート

> **[Colleague.Skill: エキスパート知識蒸留による自動AIスキル生成](colleague_skill.pdf)**
>
> colleague.skill のシステム設計を詳述した論文を執筆しました――2パート構成（業務Skill + ペルソナ）、マルチソースデータ収集、Skill生成＆進化メカニズム、実世界シナリオでの評価結果について記載しています。興味があればぜひご覧ください！

---

## Star History

<a href="https://www.star-history.com/?repos=titanwings%2Fcolleague-skill&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/image?repos=titanwings/colleague-skill&type=date&theme=dark&legend=top-left" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/image?repos=titanwings/colleague-skill&type=date&legend=top-left" />
   <img alt="Star History Chart" src="https://api.star-history.com/image?repos=titanwings/colleague-skill&type=date&legend=top-left" />
 </picture>
</a>

---

<div align="center">

MIT License © [titanwings](https://github.com/titanwings)

</div>

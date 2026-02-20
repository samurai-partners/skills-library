# Samurai Skills Library

YouTube チャンネル運用のための Claude AI スキルライブラリ。
MCP Server で取得したデータに対して、会社として統一された分析観点・出力形式で分析を行う。

## コンセプト

```mermaid
graph LR
    subgraph MCP["MCP Server<br/><i>データ取得層</i>"]
        M1[get_videos]
        M2[get_comments]
        M3[get_snapshots]
        M4[get_analytics]
    end

    subgraph Skills["Skills<br/><i>分析・解釈定義</i>"]
        S1[comment-analysis]
        S2[video-performance]
        S3[channel-comparison]
        S4[content-strategy]
        S5[trend-detection]
    end

    subgraph Claude["Claude AI<br/><i>実行・出力</i>"]
        C1[レポート生成]
        C2[戦略提案]
        C3[トレンド検出]
    end

    MCP -->|データ| Skills -->|分析指示| Claude

    style MCP fill:#e8f4fd,stroke:#2196F3,color:#000
    style Skills fill:#fff3e0,stroke:#FF9800,color:#000
    style Claude fill:#e8f5e9,stroke:#4CAF50,color:#000
```

**MCP** がデータの「何を取るか」を担い、**Skills** が「どう分析するか」を定義する。
Claude は Skills に従ってデータを取得・分析し、統一されたフォーマットでレポートを出力する。

## スキル一覧

| スキル | 説明 | 主な用途 |
|---|---|---|
| [comment-analysis](./skills/comment-analysis/) | コメントの感情・テーマ・要望を分析 | 視聴者の声の把握、改善点の発見 |
| [video-performance](./skills/video-performance/) | 動画のパフォーマンスを多角的に分析 | 伸びた動画の要因分析、改善策の提案 |
| [channel-comparison](./skills/channel-comparison/) | チャンネル間の横断比較 | 競合分析、自社チャンネルのポジショニング |
| [content-strategy](./skills/content-strategy/) | データに基づくコンテンツ戦略の策定 | 次の動画企画、投稿スケジュール最適化 |
| [trend-detection](./skills/trend-detection/) | 再生数・エンゲージメントのトレンド検出 | 異常検知、成長チャンネルの早期発見 |

## セットアップ

### Claude Code (プロジェクトスキルとして)

```bash
# リポジトリの skills/ を .claude/skills/ にシンボリックリンク
ln -s /path/to/skills-library/skills/comment-analysis .claude/skills/comment-analysis
ln -s /path/to/skills-library/skills/video-performance .claude/skills/video-performance
```

### Claude Code (個人スキルとして)

```bash
# ~/.claude/skills/ に配置すると全プロジェクトで利用可能
ln -s /path/to/skills-library/skills/comment-analysis ~/.claude/skills/comment-analysis
```

### 前提条件

`samurai-youtube` MCP Server が接続済みであること。

```json
{
  "mcpServers": {
    "samurai-youtube": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp-server-drab-three.vercel.app/mcp"]
    }
  }
}
```

## スキルの作り方

`_template/` に雛形があります。新しいスキルを作る場合:

1. `skills/<skill-name>/` ディレクトリを作成
2. `SKILL.md` を作成 (YAML frontmatter + Markdown)
3. 必要に応じて `references/`, `examples/`, `scripts/` を追加
4. PR を作成してレビュー

詳細は [_template/SKILL.md](./_template/SKILL.md) を参照。

## 仕様

[Agent Skills Open Standard](https://agentskills.io/specification) に準拠。
Claude Code / Cursor / Gemini CLI / GitHub Copilot で利用可能。

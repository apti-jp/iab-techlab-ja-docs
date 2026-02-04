---
title: Introduction
---

# IAB Tech Lab ドキュメントへようこそ

IAB Tech Lab が提供する各種仕様の日本語訳および英語版をまとめています。上部の「Japanese」「English」タブから言語を選択し、左側のナビゲーションの各ページを辿ってください。

- 日本語版の最初のページ: [/docs/ja/ads-txt-1.1](/docs/ja/ads-txt-1.1)
- 英語版の最初のページ: [/docs/en/ads-txt-1.1](/docs/en/ads-txt-1.1)

必要に応じてブックマークしてご利用ください。

---

## 翻訳ドキュメントについて

### 翻訳者・原著者・ライセンス

本サイトで公開している日本語翻訳ドキュメントは、以下の情報に基づいています。

| 項目 | 内容 |
|------|------|
| 翻訳 | Advertisers and Publishers Transparency Initiative (APTI) |
| 原著者 | IAB Technology Laboratory (IAB Tech Lab) |
| ライセンス | [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/) |

**免責事項**: これらの翻訳は、IAB Tech Lab による公式なものではありません。翻訳の正確性については翻訳者が責任を負います。

### 収録ドキュメント

現在、以下の仕様ドキュメントの日本語訳を公開しています。

#### 透明性・認証関連
- **ads.txt 1.1** - パブリッシャーが認定された販売者を明示するためのテキストファイル仕様
- **app-ads.txt** - モバイルアプリ向けの ads.txt 仕様
- **sellers.json** - 広告技術プロバイダーが販売者情報を公開するための JSON 仕様
- **buyers.json 1.0** - バイヤー情報を公開するための JSON 仕様
- **Supply Chain Object** - サプライチェーン内の全ての当事者を確認するための OpenRTB 拡張オブジェクト仕様
- **Demand Chain Object 1.0** - デマンドチェーン内の全ての当事者を確認するための仕様

#### プロトコル仕様
- **OpenRTB v3.0** - リアルタイム入札（RTB）インターフェースの標準仕様

#### 実装ガイド・補足資料
- **ads.txt 1.1 Implementation Guide** - ads.txt の実装ガイド
- **CTV App Ads Explainer Guide** - CTV（コネクテッドTV）アプリにおける ads.txt の解説ガイド

#### 新技術
- **Agentic RTB Framework 1.0** - OpenRTB およびデジタル広告におけるエージェント駆動型コンテナの使用に関する仕様

---

## AI ツールとの連携（MCP サーバー）

本サイトのドキュメントは、Model Context Protocol (MCP) サーバーを通じて AI ツールから直接検索・参照することができます。

### MCP サーバー URL

```
https://iab-docs.apti.jp/mcp
```

### MCP サーバーとは

MCP（Model Context Protocol）は、AI アプリケーションと外部サービスを接続するための標準化されたプロトコルです。MCP サーバーを AI ツールに接続することで、AI が本サイトのドキュメントを直接検索し、最新の情報に基づいた回答を生成できるようになります。

### 対応 AI ツール

以下のような MCP 対応 AI ツールで利用できます。

- **Claude Desktop** - Anthropic の Claude デスクトップアプリ
- **Claude Code** - Claude CLI ツール
- **Cursor** - AI 搭載コードエディタ
- **VS Code** - MCP 拡張機能を使用

### 利用方法

各 AI ツールの MCP サーバー設定に上記 URL を追加することで、IAB Tech Lab の仕様ドキュメントを AI が検索・参照できるようになります。詳しい設定方法は、各 AI ツールのドキュメントをご参照ください。

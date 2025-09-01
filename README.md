TODO

- [ ] フロー化
    - https://zenn.dev/yosh1/articles/mastra-ai-agent-framework-guide
    - https://n8n.io/
    - Slack等からできるように

# 技術情報キュレーションシステム

AI支援による技術記事の効率的な収集・整理・学習システム

## 概要

このシステムは、技術記事やメーリングリストなどの最新情報を効率的に収集・整理・学習するためのAI支援ツールです。ユーザープロファイルに基づいて情報を優先順位付けし、構造化された要約を作成します。

## 主な機能

- URLから技術記事を読み込み、内容を解析
- ユーザープロファイルに基づいた情報の優先順位付け
- Markdown形式での構造化された要約作成
- 継続的なプロファイル改善とフィードバックループ

## ディレクトリ構造

```
tech-knowledge-base/
├── README.md                 # このファイル
├── 00_setting/               # 設定ファイル
│   └── user_profile.md       # ユーザープロファイル設定
├── CHANGELOG.md              # 更新履歴
├── 10_general/               # 一般的な技術情報
│   ├── git/                  # Git関連
│   ├── review/               # レビュー関連
│   ├── management/           # プロジェクト管理
│   └── weekly_digest/        # 週次まとめ
├── 20_frontend/              # フロントエンド技術
│   ├── frameworks/           # フレームワーク
│   ├── tools/                # ツール
│   ├── concepts/             # 概念
│   └── weekly_digest/        # 週次まとめ
├── 30_backend/               # バックエンド技術
│   ├── languages/            # プログラミング言語
│   ├── databases/            # データベース
│   └── apis/                 # API関連
└── 40_devops/                # DevOps
    ├── ci_cd/                # CI/CD
    ├── containerization/     # コンテナ化
    └── monitoring/           # 監視
```

## 使用方法

1. `00_setting/user_profile.md`でプロファイルを設定
2. URLを提供して記事を解析・要約
3. フィードバックを基にプロファイルを継続的に改善

## 重要度レベル

- 🔴 高: 重要で緊急性の高い情報
- 🟡 中: 参考になる情報
- 🟢 低: 将来的に有用な情報

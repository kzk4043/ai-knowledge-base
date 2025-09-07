# CHANGELOG

技術情報キュレーションシステムの変更履歴

## [1.3.0] - 2025-09-07

### Added
- React Server Components フレームワーク不要実装記事 (`20_frontend/frameworks/react.md`)
  - Krasimir Tsonevのフレームワーク非依存RSC実装アプローチ
  - 軽量なサーバーサイドレンダリング手法
- Ripple UI Framework 情報 (`20_frontend/frameworks/ui_frameworks.md`)
  - React/Solid/Svelte統合を目指す新フレームワーク
  - Dominic Gannawayによる開発プロジェクト
- Astro React統合手法 (`20_frontend/frameworks/react.md`)
  - Chris PenningtonのYouTube動画要約
  - 3つの実践的React統合方法
- ブラウザタイマーThrottling解説 (`20_frontend/concepts/browser_apis.md`)
  - Nolan LawsonによるJavaScriptタイマーの内部動作解説
  - setTimeout(0)の実際の動作とパフォーマンス影響

### Updated
- React Status Issue 442, JavaScript Weekly #751, Astro Weekly #99の記事分析・選定プロセス実行
- ユーザープロファイル照合による優先度付け記事要約（5記事選定）

## [1.2.0] - 2025-08-30

### Added  
- Beacon API分析記事 (`20_frontend/concepts/beacon_api.md`)
  - ページ離脱時の確実なデータ送信手法
  - 従来手法との比較と技術的仕組みの解説
  - Web Analytics実装パターン

### Updated
- JavaScript Weekly #750 の記事分析・選定プロセス実行
- ユーザープロファイルに重要度判定基準を追加
  - ブラウザ標準による従来技術の代替を重要視する方針を明記

## [1.1.0] - 2024-08-28

### Added
- React状態管理パターン分析記事 (`20_frontend/frameworks/react_state_management.md`)
  - localStorage vs Context/Redux/Zustand比較
  - 技術的制約と適切な使用場面の解説
- React高性能フレームワーク分析記事 (`20_frontend/frameworks/react_performance_framework.md`)
  - Rariフレームワークのアーキテクチャ解析
  - Server Componentsとパフォーマンス最適化技法

### Updated
- URL処理プロンプト形式の改良 (`90_prompt/url_processing.md`)

## [1.0.0] - 2025-01-28

### Added
- 初期プロジェクト構造の作成
- ディレクトリ構造の構築（10_general, 20_frontend, 30_backend, 40_devops）
- ユーザープロファイル管理システムの導入
- README.md with プロジェクト概要
- 技術記事要約テンプレートの定義

### Features
- ユーザープロファイルベースの記事優先順位付け
- Markdown形式での構造化要約
- 継続的なプロファイル学習機能
- カテゴリ別情報整理システム
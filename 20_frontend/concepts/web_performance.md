# Webパフォーマンス最適化

## Core Web Vitals と Google 検索のランキング影響

**URL**: https://developers.google.com/search/docs/appearance/core-web-vitals?hl=ja
**日付**: 2025-09-30
**重要度**: 🔴 高
**タグ**: Core Web Vitals, SEO, Performance, User Experience

### 概要
Core Web VitalsはWebページのユーザーエクスペリエンスを測定する重要な指標で、Google検索のランキングに直接影響を与えます。

### Core Web Vitalsの3つの主要指標

#### 1. Largest Contentful Paint (LCP)
- **測定対象**: 読み込みパフォーマンス
- **目標値**: ページ読み込み開始から2.5秒以内
- **意義**: メインコンテンツの表示速度

#### 2. Interaction To Next Paint (INP)
- **測定対象**: 応答性
- **目標値**: 200ミリ秒未満
- **意義**: ユーザーインタラクションへの反応速度

#### 3. Cumulative Layout Shift (CLS)
- **測定対象**: 視覚的安定性
- **目標値**: 0.1未満
- **意義**: レイアウトの予期しない移動の防止

### 最適化のためのリソース
- Search Consoleの Core Web Vitalsレポート
- Web.devのCore Web Vitalsガイド
- 各種測定・分析ツール

### 影響と意義
- Google検索のランキングシステムで考慮される
- ユーザーエクスペリエンス向上がSEOに直結
- サイト所有者は積極的な改善が推奨される

## JavaScript長時間タスクの最適化 - scheduler.yield() API

**URL**: https://web.dev/articles/optimize-long-tasks?utm_source=devtools&utm_campaign=stable&hl=ja
**日付**: 2025-09-30
**重要度**: 🔴 高
**タグ**: JavaScript, Performance, Main Thread, Task Management

### 概要
メインスレッドでの長時間JavaScript実行がWebページの応答性に与える影響と、`scheduler.yield()` APIを使用した最適化手法。

### 主要な技術的指針

#### 1. タスク分割戦略
- 50ミリ秒以上のタスクは応答性を低下させる
- タスクを小さな単位に分割する
- 重要なユーザー向けタスクを優先する

#### 2. scheduler.yield() APIの活用
```javascript
async function processLargeDataset() {
  for (let i = 0; i < dataset.length; i++) {
    processItem(dataset[i]);
    
    // 定期的にメインスレッドに制御を戻す
    if (i % 100 === 0) {
      await scheduler.yield();
    }
  }
}
```

#### 3. 実装のベストプラクティス
- 非同期関数内で `await scheduler.yield()` を使用
- タスクをバッチ処理し、定期的にメインスレッドに制御を戻す
- クロスブラウザ対応のためのフォールバック戦略

### 影響と意義
- ブラウザ標準APIによる複雑なパフォーマンス問題の解決
- React開発でのレンダリング最適化に直接適用可能
- ユーザーインタラクションの応答性向上

## レイアウトスラッシング回避とパフォーマンス最適化

**URL**: https://web.dev/articles/avoid-large-complex-layouts-and-layout-thrashing?utm_source=devtools&utm_campaign=stable&hl=ja#avoid-forced-synchronous-layouts
**日付**: 2025-09-30
**重要度**: 🔴 高
**タグ**: Layout, Performance, DOM, Browser Rendering

### 概要
ブラウザのレイアウト処理最適化により、Webページのパフォーマンスと応答性を向上させる手法。

### レイアウト最適化の重要ポイント

#### 1. レイアウトの基本原理
- レイアウトはブラウザが要素のジオメトリ情報を計算するプロセス
- DOMのサイズと複雑さがレイアウト費用に直接影響
- インタラクション レイテンシを最小限に抑える必要

#### 2. 強制同期レイアウトの回避
```javascript
// 悪い例：強制同期レイアウト
element.style.width = '100px';
console.log(element.offsetWidth); // レイアウトを強制実行

// 良い例：読み取りと書き込みの分離
const width = element.offsetWidth; // 最初に読み取り
element.style.width = '100px';   // 次に書き込み
```

#### 3. 最適化戦略
- スタイル値の読み取りと書き込みを分離
- レイアウトのスラッシング（連続する不要なレイアウト）を回避
- `requestAnimationFrame()` を活用してパフォーマンスを最適化

### 技術的指針
- レイアウトをトリガーするプロパティの使用を最小限に
- スタイルの読み取りは常にバッチ処理
- DevToolsを使用してレイアウトボトルネックを特定

### 影響と意義
- React開発での根本的なパフォーマンス問題の解決
- ブラウザ標準の理解による開発者体験向上
- 大規模アプリケーションでの応答性確保

## First Contentful Paint (FCP) 最適化指針

**URL**: https://developer.chrome.com/docs/lighthouse/performance/first-contentful-paint/?utm_source=lighthouse&utm_medium=lr
**日付**: 2025-09-30
**重要度**: 🟡 中
**タグ**: FCP, Lighthouse, Performance Metrics, Page Load

### 概要
First Contentful Paint (FCP)は、ブラウザが最初のDOMコンテンツをレンダリングするまでの時間を測定するWebパフォーマンス指標。

### 技術的詳細

#### 1. FCP測定基準
- 画像、非白色のcanvas要素、SVGをDOMコンテンツとして考慮
- iframe内のコンテンツは除外
- 秒単位で測定

#### 2. パフォーマンススコア閾値

**モバイル**:
- 0-1.8秒: Green（高速）
- 1.8-3秒: Orange（中程度）
- 3秒超: Red（低速）

**デスクトップ**:
- 0-0.9秒: Green（高速）
- 0.9-1.6秒: Orange（中程度）
- 1.6秒超: Red（低速）

#### 3. 最適化推奨事項
- フォント読み込み時間の改善
- レンダリングブロックリソースの除去
- Lighthouseレポートの診断セクション活用
- 総合的なパフォーマンススコア向上

### 影響と意義
- ページ読み込み速度の可視化
- ユーザーエクスペリエンス向上への貢献
- Lighthouseパフォーマンス最適化の基礎指標

## Largest Contentful Paint (LCP) 測定と改善

**URL**: https://developer.chrome.com/docs/lighthouse/performance/lighthouse-largest-contentful-paint/?utm_source=lighthouse&utm_medium=lr
**日付**: 2025-09-30
**重要度**: 🟡 中
**タグ**: LCP, Core Web Vitals, Performance Optimization, Main Content

### 概要
Largest Contentful Paint (LCP)は、ビューポート内の最大コンテンツ要素がスクリーンにレンダリングされる時間を測定するLighthouseパフォーマンス指標。

### 技術的詳細

#### 1. LCP測定対象
- ビューポート内の最大コンテンツ要素
- メインページコンテンツの可視化タイミングを近似
- ユーザーにとって意味のあるコンテンツの表示速度

#### 2. パフォーマンス閾値

**モバイルLCPスコア**:
- 0-2.5秒: Green（高速）
- 2.5-4秒: Orange（中程度）
- 4秒超: Red（低速）

**デスクトップLCPスコア**:
- 0-1.2秒: Green（高速）
- 1.2-2.4秒: Orange（中程度）
- 2.4秒超: Red（低速）

#### 3. LCPサブパート分析
1. **Time to first byte (TTFB)**: サーバー応答時間
2. **Load delay**: リソース発見の遅延
3. **Load time**: リソース読み込み時間
4. **Render delay**: レンダリング遅延

#### 4. 最適化戦略
- 最も時間のかかるLCPサブパートの分析
- リソース読み込みの最適化
- TTFBの最小化
- レンダリング・読み込み遅延の削減

### 影響と意義
- Core Web Vitalsの主要指標
- 実際の最適化手法の習得機会
- ユーザー体感速度の改善
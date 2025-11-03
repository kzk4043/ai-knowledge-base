# CSS Anchor Positioning API - Perfect Tooltips

## メタデータ
- **URL**: https://frontendmasters.com/blog/perfectly-pointed-tooltips-a-foundation/
- **日付**: 2025-10-31
- **重要度**: 🟢 低
- **タグ**: CSS Anchor Positioning, Tooltips, ブラウザ標準

## 概要
CSS Anchor Positioning APIを使った完璧なツールチップの実装。JavaScriptでの複雑な位置計算を標準CSS機能で代替し、パフォーマンスと保守性を向上。

## API概要

### 従来の課題
- JavaScript による複雑な位置計算
- スクロール・リサイズ時の再計算
- 画面外配置の検出・調整
- パフォーマンスオーバーヘッド

### CSS Anchor Positioning の解決
```css
#my-tooltip {
  position-anchor: --question-mark;
  position-area: top;
  position-try-fallbacks: flip-block;
}
```

**利点:**
- 宣言的な位置指定
- 自動フォールバック
- ネイティブパフォーマンス

## 基本実装

### HTML構造
```html
<button id="anchor-element">?</button>
<div id="tooltip">説明テキスト</div>
```

### CSS設定
```css
#anchor-element {
  anchor-name: --question-mark;
}

#tooltip {
  position: absolute;
  position-anchor: --question-mark;
  position-area: top;
}
```

## 高度な機能

### 自動フォールバック
```css
.tooltip {
  position-area: top;
  position-try-fallbacks: flip-block, flip-inline;
}
```

**フォールバック順序:**
1. `top` (基本位置)
2. `flip-block` (上下反転)  
3. `flip-inline` (左右反転)

### カスタムフォールバック
```css
@position-try --custom-fallback {
  position-area: bottom;
  margin-top: 10px;
}

.tooltip {
  position-try-fallbacks: --custom-fallback;
}
```

### 動的サイジング
```css
.tooltip {
  /* アンカー要素の幅に基づくサイズ調整 */
  width: anchor-size(width);
  max-width: 300px;
}
```

## 実装例

### 基本ツールチップ
```css
.tooltip {
  position: absolute;
  position-anchor: --trigger;
  position-area: top;
  
  background: #333;
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  
  /* 矢印の実装 */
  &::after {
    content: '';
    position: absolute;
    top: 100%;
    left: 50%;
    transform: translateX(-50%);
    border: 5px solid transparent;
    border-top-color: #333;
  }
}
```

### アクセシブルツールチップ
```css
.tooltip {
  position-anchor: --trigger;
  position-area: top;
  
  /* スクリーンリーダー対応 */
  role: tooltip;
  
  /* フォーカス管理 */
  &:not([data-visible]) {
    opacity: 0;
    pointer-events: none;
  }
}
```

## ブラウザサポート

### 現在の対応状況
- **Chrome 123+**: 完全サポート
- **Edge 123+**: 完全サポート  
- **Firefox**: 開発中
- **Safari**: 開発中

### Polyfill対応
```javascript
// Oddbird CSS Anchor Positioning Polyfill
import { polyfill } from '@oddbird/css-anchor-positioning';

if (!CSS.supports('anchor-name', '--test')) {
  polyfill();
}
```

## パフォーマンス比較

### JavaScript実装
```javascript
// 従来の方法（複雑）
function positionTooltip(anchor, tooltip) {
  const anchorRect = anchor.getBoundingClientRect();
  const tooltipRect = tooltip.getBoundingClientRect();
  
  // 位置計算ロジック（50行以上）
  // スクロール・リサイズ対応
  // 画面外チェック
}
```

### CSS実装
```css
/* 新しい方法（シンプル） */
.tooltip {
  position-anchor: --anchor;
  position-area: top;
  position-try-fallbacks: flip-block;
}
```

**メリット:**
- コード量: 90%以上削減
- パフォーマンス: ネイティブ最適化
- 保守性: 宣言的で理解しやすい

## 制限事項

### 現在の制約
- ブラウザサポートが限定的
- 複雑なアニメーションとの組み合わせ
- カスタムロジックが必要な特殊ケース

### 移行戦略
```css
/* Progressive Enhancement */
.tooltip {
  /* フォールバック位置 */
  position: absolute;
  top: -40px;
  left: 50%;
  transform: translateX(-50%);
}

/* Anchor Positioning対応ブラウザ */
@supports (position-anchor: --test) {
  .tooltip {
    position-anchor: --trigger;
    position-area: top;
    position-try-fallbacks: flip-block;
    top: auto;
    left: auto;
    transform: none;
  }
}
```

## 今後の展望
- **Universal Browser Support**: 2025年末目標
- **Enhanced Animation Support**: transition との統合
- **Framework Integration**: React, Vue での標準サポート

## 学習リソース
- [CSS Anchor Positioning - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_anchor_positioning)
- [Chrome DevTools での デバッグ](https://developer.chrome.com/docs/devtools/css/anchor-positioning)
- [Polyfill Repository](https://github.com/oddbird/css-anchor-positioning)
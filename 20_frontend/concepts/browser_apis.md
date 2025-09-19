# ブラウザAPI情報

**更新日**: 2025-09-07  
**カテゴリ**: 20_frontend/concepts  

## 概要
ブラウザの内部動作やAPIの仕組みに関する技術情報をまとめます。

## JavaScript言語機能

### 安全な配列メソッド（ES2023） 🔴

**URL**: JavaScript Weekly Issue 752  
**重要度**: 高  
**日付**: 2025-09-18  
**タグ**: #javascript, #es2023, #arrays, #immutable, #browser-standards

#### 概要
ES2023で導入された4つの新しい「安全な」配列メソッド。これらは既存の破壊的メソッドの非破壊版で、元の配列を変更せずに新しい配列を返す。

#### 新メソッド一覧
1. **`toSorted()`** - `sort()`の非破壊版
2. **`toReversed()`** - `reverse()`の非破壊版
3. **`toSpliced()`** - `splice()`の非破壊版
4. **`with()`** - インデックス指定要素置換の非破壊版

#### 技術的メリット
- **意図しない突然変異の防止**: 元配列の意図しない変更を回避
- **関数型プログラミング対応**: 不変データ構造をサポート
- **React状態管理の改善**: 状態更新時の予測可能性向上
- **デバッグの簡素化**: 副作用のないコードでバグ追跡が容易

#### コード例
```javascript
const numbers = [3, 1, 4, 1, 5];

// 従来の破壊的メソッド
numbers.sort(); // 元配列を変更: [1, 1, 3, 4, 5]

// 新しい安全なメソッド
const sorted = numbers.toSorted(); // [1, 1, 3, 4, 5]
console.log(numbers); // 元配列は変更されず: [3, 1, 4, 1, 5]

// その他の例
const arr = [1, 2, 3, 4];
const reversed = arr.toReversed(); // [4, 3, 2, 1]
const spliced = arr.toSpliced(1, 2, 'a', 'b'); // [1, 'a', 'b', 4]
const updated = arr.with(1, 'new'); // [1, 'new', 3, 4]
```

#### ブラウザサポート
- **Chrome/Edge**: 110+
- **Safari**: 16+
- **Firefox**: 115+
- **Node.js**: 20+

#### React開発への影響
```javascript
// 従来のReact状態更新（良くない例）
setItems(items.sort()); // 元配列を破壊的に変更

// 安全な状態更新（推奨）
setItems(items.toSorted()); // 新しい配列を作成
```

#### 採用判断基準
- **高優先度**: 複雑・不安定だった配列操作がブラウザ標準で解決
- **関数型プログラミング**: 不変性を重視する開発チームに最適
- **フレームワーク互換**: React、Vue等の状態管理と自然に連携

## タイマー機能

### ブラウザのタイマーThrottling 🟡

**URL**: https://javascriptweekly.com/issues/751  
**重要度**: 中  
**日付**: 2025-09-05  
**タグ**: #browser, #timers, #performance, #throttling

#### 概要
Nolan Lawsonによる記事「Why Do Browsers Throttle JavaScript Timers?」の要約。ブラウザがJavaScriptタイマーをスロットルする理由と影響について解説。

#### 主なポイント
- `setTimeout(0)`は実際には0ミリ秒で実行されない
- ブラウザは最低数ミリ秒の遅延を設ける（clamp）
- 精密なタイミングに依存するコードのパフォーマンスに影響

#### 技術的背景
- ブラウザによるタイマー最適化機能
- CPUリソース管理のための制限

#### 開発者への影響
- `setTimeout`や類似関数の実際の動作理解
- 代替アプローチの検討が必要な場合がある

#### 対策
- 記事では回避策も提案（詳細は元記事参照）

#### 関連リソース
- [元記事](https://nolanlawson.com)
# JSON Import Attributes

## メタデータ  
- **URL**: https://jakearchibald.com/2024/import-json/
- **日付**: 2025-10-31
- **重要度**: 🔴 高
- **タグ**: ES Modules, JSON, ブラウザ標準, Jake Archibald

## 概要
新しいImport属性を使ったJSON読み込み方法。従来のfetch APIベースの複雑な処理を標準化された`import`文で代替可能。

## 要点

### 新しい構文
```javascript
import data from './data.json' with { type: 'json' };
```

### 従来のfetch APIとの比較

**従来の方法:**
```javascript
const response = await fetch('./data.json');
const data = await response.json();
```

**新しい方法:**
```javascript
import data from './data.json' with { type: 'json' };
```

### メリット
- **静的解析**: バンドラーでの最適化が可能
- **キャッシュ効率**: モジュールキャッシュの活用
- **型安全性**: TypeScriptでの型推論サポート
- **デッドコード除去**: 未使用データの自動削除

## 詳細

### ブラウザサポート
- Chrome 123+
- Firefox 114+  
- Safari 17.5+

### 使用上の注意点
- JSONは静的にインポートされる
- 動的な読み込みには従来の`fetch`を使用
- バンドル時にJSONがインライン化される

### TypeScript統合
```typescript
// types.d.ts
declare module '*.json' {
  const value: any;
  export default value;
}
```

## 活用例

### 設定ファイルの読み込み
```javascript
import config from './config.json' with { type: 'json' };
console.log(config.apiEndpoint);
```

### 静的データの埋め込み
```javascript
import translations from './i18n/en.json' with { type: 'json' };
export const t = (key: string) => translations[key];
```

## 関連リソース
- [Import Attributes Proposal](https://github.com/tc39/proposal-import-attributes)
- [MDN Import Attributes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#import_attributes)
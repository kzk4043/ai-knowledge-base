# Node.js バックエンド開発

**更新日**: 2025-01-28  
**カテゴリ**: 30_backend/languages  

## 概要
Node.jsを使用したバックエンド開発に関する情報をまとめます。

## Express.js基本

### サーバーセットアップ
```javascript
const express = require('express');
const app = express();

app.use(express.json());

app.get('/', (req, res) => {
  res.json({ message: 'Hello World' });
});

app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

### ミドルウェア
```javascript
// ログ出力ミドルウェア
app.use((req, res, next) => {
  console.log(`${req.method} ${req.path}`);
  next();
});

// エラーハンドリング
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Something went wrong!' });
});
```

## 非同期処理

### Promise/async-await
```javascript
async function fetchData() {
  try {
    const data = await someAsyncOperation();
    return data;
  } catch (error) {
    throw new Error('Failed to fetch data');
  }
}
```

## npm Supply Chain Security

### GitHub npm Supply Chain Security Plan 🟡

**URL**: https://javascriptweekly.com/issues/754
**重要度**: 中
**日付**: 2025-09-30
**タグ**: npm, security, supply-chain, malware, trusted-publishing

#### 概要
GitHubがnpmエコシステムのサプライチェーンセキュリティ向上のための包括的計画を発表。

#### 主要な対策
- **マルウェアパッケージのブロック**: 悪意のあるパッケージのアップロード防止
- **パッケージ公開の堅牢化**: より厳格な認証・検証プロセス
- **信頼できる公開（Trusted Publishing）の推進**: 正規の開発者・組織からの公開を保証

#### 背景
- 「Shai-Hulud」攻撃により数百のパッケージが影響
- トークンや機密情報の漏洩を試みる攻撃が発生
- pnpmなどのツールが対応を実施

#### 技術的対策
- **自動スキャン**: パッケージの脆弱性・マルウェア検出
- **公開認証**: 多要素認証とデジタル署名の強化
- **依存関係分析**: 間接的な脅威の検出と防止

#### 開発者への影響
- パッケージ公開時の追加認証手順
- 依存関係の信頼性評価の重要性増加
- セキュリティベストプラクティスの必須化

#### 長期的意義
- Node.jsエコシステム全体の信頼性向上
- オープンソースの持続可能性とセキュリティの両立
- 企業でのNode.js採用促進

## 関連リソース
- [Node.js公式ドキュメント](https://nodejs.org/docs)
- [Express.js公式ガイド](https://expressjs.com)
- [npm Security Guidelines](https://docs.npmjs.com/security)
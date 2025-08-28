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

## 関連リソース
- [Node.js公式ドキュメント](https://nodejs.org/docs)
- [Express.js公式ガイド](https://expressjs.com)
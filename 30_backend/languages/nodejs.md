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

## Node.js v24 LTS リリース 🔴

**URL**: https://nodejs.org/en/blog/release/v24.11.0  
**重要度**: 高  
**日付**: 2025-11-04  
**タグ**: Node.js, LTS, npm, V8, URLPattern, AsyncLocalStorage

### 概要
Node.js v24がLTS（Long Term Support）として正式リリース。2028年4月まで長期サポート対象。

### 主要な新機能

#### V8エンジン v13.6
```javascript
// Float16Array対応
const float16Array = new Float16Array([1.5, 2.5, 3.5]);

// RegExp.escape() 標準関数
const pattern = new RegExp(RegExp.escape('user.input'));
```

#### npm 11統合
```bash
# パフォーマンス向上
npm install  # より高速なインストール

# セキュリティ強化
npm audit --fix  # 改善されたセキュリティチェック

# プロジェクト初期化改善
npm init  # より直感的な初期化プロセス
```

#### URLPattern グローバル対応
```javascript
// インポート不要でURLPattern使用可能
const pattern = new URLPattern('/api/users/:id');
const match = pattern.exec('/api/users/123');
console.log(match.pathname.groups.id); // '123'
```

#### AsyncLocalStorage改善
```javascript
// AsyncContextFrameをデフォルト使用
import { AsyncLocalStorage } from 'node:async_hooks';

const asyncLocalStorage = new AsyncLocalStorage();
// パフォーマンスと安定性が向上
```

#### 権限モデルの正式化
```bash
# 実験的フラグから正式機能へ
node --permission=read,write script.js
# 旧: --experimental-permission
```

### npm 11の改善点

#### インストール速度
```bash
# キャッシュ最適化
npm install express  # 平均30%高速化

# 並列処理改善
npm ci  # CI環境での大幅な速度向上
```

#### セキュリティ機能
```json
{
  "scripts": {
    "audit": "npm audit --audit-level moderate",
    "fix": "npm audit fix --force"
  }
}
```

#### プロジェクト管理
```bash
# ワークスペース機能強化
npm workspaces update  # 依存関係の一括更新

# パッケージ情報の詳細表示
npm info express --verbose
```

### 技術的メリット

#### 依存関係管理の複雑さ解決
- npm 11での依存関係解決アルゴリズム改善
- 循環依存の検出と警告機能強化
- パッケージロックファイルの最適化

#### 標準ライブラリ機能拡張
- URLPatternの標準搭載により、複雑なルーティングライブラリが不要に
- AsyncLocalStorageの安定性向上でコンテキスト管理が簡素化

#### セキュリティ標準化
```javascript
// 権限モデルによるファイルアクセス制御
process.permission.has('fs.read', '/etc/passwd'); // false
```

### 移行ガイド

#### v22からの変更点
```bash
# Node.js v24へのアップグレード
nvm install 24
nvm use 24

# npm 11の確認
npm --version  # 11.x.x
```

#### 破壊的変更
- 古いV8フラグの削除
- 非推奨APIの削除
- Node.js 16以前のサポート終了

### パフォーマンス改善

#### ベンチマーク結果
```javascript
// HTTP サーバーパフォーマンス（v22比較）
// リクエスト処理: +15%改善
// メモリ使用量: -8%削減
// 起動時間: +20%高速化
```

#### 最適化ポイント
- V8 JITコンパイラーの改善
- ガベージコレクションの最適化
- モジュール読み込み速度の向上

### 開発者への影響

#### 新機能活用
```javascript
// URLPatternでルーティング簡素化
const userPattern = new URLPattern('/users/:id');
const productPattern = new URLPattern('/products/:category/:id');

// AsyncLocalStorageでリクエストコンテキスト管理
const requestContext = new AsyncLocalStorage();
```

#### ツールチェーン統合
- Viteとの連携改善
- TypeScriptサポート強化
- ESMとCommonJSの相互運用性向上

### まとめ
Node.js v24 LTSは、依存関係管理・標準ライブラリ拡張・セキュリティ標準化の重要な進歩をもたらす。特にnpm 11の改善とURLPatternの標準搭載は、複雑な実装を標準機能で代替する理想的な進化を示している。

## Node.js Runtime選択肢

### Node.js v24 LTS + Vercel Bun Runtime サポート 🟡

**URL**: https://javascriptweekly.com/issues/760, https://react.statuscode.com/issues/450  
**重要度**: 中  
**日付**: 2025年11月  
**タグ**: #nodejs, #bun, #vercel, #runtime, #dependency-management

#### 概要
VercelがBun runtimeの公式サポートを発表し、Node.js v24 LTSと並行してランタイム選択肢が拡充。依存関係管理の複雑さを解決する重要な進歩。

#### Vercel Bun Runtime サポート
```javascript
// vercel.json での設定
{
  "functions": {
    "app.js": {
      "runtime": "bun"
    }
  }
}

// package.json での指定
{
  "engines": {
    "bun": "^1.0.0"
  }
}
```

#### パフォーマンス比較
- **起動速度**: Node.jsより高速なコールドスタート
- **パッケージ管理**: 統合されたパッケージマネージャー
- **バンドルサイズ**: より小さなデプロイメントサイズ
- **開発体験**: 統一ツールチェーンによる設定簡素化

#### 移行考慮事項
```javascript
// LTS採用戦略
{
  "engines": {
    "node": ">=24.0.0"
  }
}

// Docker でのLTS使用
FROM node:24-alpine
```

#### ランタイム選択指針
- **既存プロジェクト**: Node.js LTSによる安定運用
- **新規プロジェクト**: 要件に応じたBun評価
- **クラウド統合**: Vercel等での最適化活用
- **パフォーマンス**: 実測による選択

#### 学習ポイント
1. **LTS戦略**: 長期サポートによる本番環境構築
2. **依存関係削減**: 標準ライブラリによる外部依存最小化
3. **ランタイム選択**: プロジェクト特性に応じた適切な判断
4. **クラウド統合**: プラットフォーム最適化の活用

## 関連リソース
- [Node.js公式ドキュメント](https://nodejs.org/docs)
- [Express.js公式ガイド](https://expressjs.com)
- [npm Security Guidelines](https://docs.npmjs.com/security)
- [Bun Runtime Documentation](https://bun.sh)
- [Vercel Functions](https://vercel.com/docs/functions)
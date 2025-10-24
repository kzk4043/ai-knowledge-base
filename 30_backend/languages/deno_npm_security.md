# Denoのnpm脆弱性保護機能

**URL**: https://deno.com/blog/deno-protects-npm-exploits  
**日付**: 2025年10月  
**重要度**: 🔴 高  
**タグ**: Deno, セキュリティ, npm, 脆弱性, サンドボックス

## 概要

Denoが採用する「secure by default」アプローチにより、npmエコシステムで頻発するセキュリティ脆弱性から開発者を保護する仕組みを解説。従来の複雑なセキュリティ対策を標準機能で解決する重要な進歩。

## npmセキュリティの現状課題

### 最近の主要インシデント
- **大規模パッケージの侵害**: 週数百万ダウンロードのパッケージが攻撃対象
- **postinstallスクリプト攻撃**: インストール時の自動実行を悪用
- **フィッシング攻撃**: パッケージ名の類似性を利用した攻撃

### Node.js/npmの脆弱性
```bash
# Node.js/npmでの危険な実行例
npm install suspicious-package

# パッケージが自動でシステム全体にアクセス可能
# - ファイルシステム全体
# - ネットワーク接続
# - 環境変数
# - 子プロセス実行
```

## Denoのセキュリティモデル

### サンドボックス実行
- **デフォルト制限**: コードは隔離された環境で実行
- **明示的許可**: 必要な権限のみを個別に付与
- **システム保護**: 不正アクセスを根本的に防止

### 権限システム
```javascript
// Denoでの安全なコード実行
// ファイル読み取り権限を明示的に付与
deno run --allow-read=./config.json app.js

// ネットワークアクセスを特定ドメインのみ許可
deno run --allow-net=api.example.com app.js

// 複数権限の組み合わせ
deno run --allow-read=./data --allow-write=./output --allow-net=api.company.com app.js
```

## 技術的詳細

### 権限の粒度制御
```javascript
// ファイルシステムアクセスの制限
--allow-read              // 全ファイル読み取り許可
--allow-read=./src        // srcディレクトリのみ許可
--allow-read=config.json  // 特定ファイルのみ許可

// ネットワークアクセスの制限
--allow-net               // 全ネットワーク許可
--allow-net=deno.land     // 特定ドメインのみ許可
--allow-net=:8000         // 特定ポートのみ許可
```

### 権限の監査機能
```bash
# 権限使用状況のログ出力
deno run --log-level=info --allow-all app.js

# 権限要求の詳細表示
deno run --allow-read --allow-net=api.example.com --inspect app.js
```

## セキュリティの実践例

### 従来のNode.js（危険）
```javascript
// package.json の postinstall スクリプト
{
  "scripts": {
    "postinstall": "node malicious-script.js"
  }
}

// malicious-script.js
const fs = require('fs');
const crypto = require('crypto');

// システム全体にアクセス可能
fs.readFileSync('/etc/passwd');
process.env.SECRET_KEY; // 環境変数へのアクセス
```

### Denoでの安全な実行
```javascript
// Denoでの同等機能（安全）
try {
  // 明示的に許可されたファイルのみアクセス可能
  const config = await Deno.readTextFile('./config.json');
  
  // 権限がない場合は例外発生
  const systemFile = await Deno.readTextFile('/etc/passwd'); // PermissionDenied
} catch (error) {
  console.log('権限エラー:', error.message);
}
```

## 追加のセキュリティ機能

### 標準ライブラリの活用
```javascript
// Denoの標準ライブラリによる依存関係削減
import { serve } from "https://deno.land/std@0.208.0/http/server.ts";
import { hash } from "https://deno.land/std@0.208.0/crypto/mod.ts";

// 外部パッケージの依存を最小化
```

### JSR（JavaScript Registry）
- **強化されたセキュリティ**: パッケージの検証機能
- **来歴証明**: パッケージの出所と変更履歴の追跡
- **透明性**: オープンで検証可能なレジストリ

## 移行のメリット

### セキュリティ向上
- **攻撃面の縮小**: 不要な権限の排除
- **透明性**: 必要な権限の明確化
- **監査可能性**: 権限使用の追跡

### 開発効率
```javascript
// package.json の複雑な依存関係から解放
// Denoでのシンプルなインポート
import { assertEquals } from "https://deno.land/std@0.208.0/testing/asserts.ts";
import { Application } from "https://deno.land/x/oak@v12.6.1/mod.ts";
```

## 実装戦略

### 段階的移行
```bash
# 1. 既存プロジェクトの評価
deno check src/main.ts

# 2. 必要最小限の権限で実行
deno run --allow-read=./config --allow-net=api.example.com src/main.ts

# 3. 権限の最適化
deno run --allow-read=./config.json --allow-net=api.example.com:443 src/main.ts
```

### セキュリティ設計原則
1. **最小権限の原則**: 必要最小限の権限のみ付与
2. **明示的許可**: 暗黙的なアクセスの排除
3. **監査可能性**: 権限使用の記録と追跡
4. **分離原則**: コンポーネント間の適切な分離

## 学習ポイント

1. **セキュリティモデル**: サンドボックス実行の重要性
2. **権限管理**: 粒度細かい権限制御の価値
3. **依存関係**: 外部依存の最小化戦略
4. **監査**: セキュリティ状況の可視化

## まとめ

Denoのセキュリティアプローチは、従来のNode.js/npmエコシステムの根本的な脆弱性を解決する革新的な仕組み。複雑なセキュリティ対策を標準機能として提供し、開発者が明示的な権限管理により安全なアプリケーションを構築できる。特に、セキュリティが苦手な開発者にとって、システムレベルでの保護により安心して開発に集中できる重要な進歩。
# GitHub Actions CI/CD

**更新日**: 2025-01-28  
**カテゴリ**: 40_devops/ci_cd  

## 概要
GitHub Actionsを使用したCI/CDパイプラインの設定と運用について。

## 基本ワークフロー

### Node.js プロジェクト
```yaml
name: Node.js CI

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [16.x, 18.x, 20.x]
        
    steps:
    - uses: actions/checkout@v3
    
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
        
    - run: npm ci
    - run: npm run build --if-present
    - run: npm test
```

### デプロイ例
```yaml
  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
    - uses: actions/checkout@v3
    - name: Deploy to production
      run: echo "Deploying to production"
```

## ベストプラクティス

### セキュリティ
- Secretsを使用して機密情報を管理
- 最小権限の原則を適用
- 依存関係の脆弱性をチェック

### パフォーマンス
- キャッシュを活用してビルド時間を短縮
- 並列実行でジョブを最適化
- 必要な場合のみワークフローを実行

## 関連リソース
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Marketplace](https://github.com/marketplace?type=actions)
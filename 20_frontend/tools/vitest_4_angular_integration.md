# Vitest 4.0 - Angular統合とViteネイティブテスト

## メタデータ
- **URL**: https://vitest.dev/blog/vitest-4
- **日付**: 2025-10-31
- **重要度**: 🟡 中
- **タグ**: Vitest, Angular, テストフレームワーク, Vite

## 概要
Vitest 4.0がリリースされ、Angular 21のデフォルトテストフレームワークに採用。安定したブラウザモード、ビジュアルリグレッションテスト、Playwrightトレース統合を提供。

## 主要機能

### 安定したブラウザモード
- Vitest 4.0でブラウザモードが安定版に
- 実ブラウザ環境でのテスト実行
- Node.js環境の制約を解消

**プロバイダー対応:**
```javascript
// 個別パッケージのインストールが必要
npm install @vitest/browser-playwright
npm install @vitest/browser-webdriverio  
npm install @vitest/browser-preview
```

### ビジュアルリグレッションテスト
- UI変更の自動検出
- スクリーンショット比較機能
- ブラウザモードと統合

### Angular 21での採用

**デフォルト選択:**
```bash
ng new my-app
# Vitest が Jasmine より優先される
```

**採用理由:**
- ESMサポート（Jestの問題解決）
- TypeScriptファーストクラス対応
- ブラウザ実行（Jasmine/Karma同様）

### Viteエコシステム統合

**メリット:**
- Viteと同一設定の共有
- Hot Module Replacement対応
- 高速なテスト実行

**設定例:**
```javascript
// vitest.config.ts
import { defineConfig } from 'vitest/config';

export default defineConfig({
  test: {
    environment: 'jsdom', // or 'happy-dom'
    browser: {
      enabled: true,
      name: 'chrome'
    }
  }
});
```

## Angular統合の利点

### 技術的改善
- **ESM対応**: Jestでの複雑な設定が不要
- **型安全性**: TypeScript統合の改善
- **パフォーマンス**: Viteベースの高速ビルド

### 開発体験向上
```javascript
// Angular Component テスト
import { render } from '@testing-library/angular';
import { AppComponent } from './app.component';

test('should render title', async () => {
  await render(AppComponent, {
    inputs: { title: 'Test App' }
  });
  
  expect(screen.getByText('Test App')).toBeInTheDocument();
});
```

### エコシステム統合
- Angular CLI完全サポート
- 既存Jasmine/Karmaからの移行パス
- Vite dev serverとの統合

## 他フレームワークでの影響

### React
- Next.js, Vite React テンプレートでの採用拡大
- Jest代替としての地位確立

### Vue
- Vite Vue テンプレートでの標準化
- Vitest + Vue Test Utilsの組み合わせ

## パフォーマンス比較

**Vitest vs Jest:**
- 起動時間: 約50%短縮
- テスト実行: 30-40%高速化
- Hot reload: ほぼ瞬時

**Vitest vs Jasmine/Karma:**
- 設定の簡素化
- ブラウザ互換性維持
- モダンJS機能の完全サポート

## 移行ガイド

### Angular プロジェクト
```bash
# 新規プロジェクト
ng new my-app --package-manager=npm

# 既存プロジェクトでの追加
ng add @angular/vitest
```

### 設定ファイル
```javascript
// angular.json
{
  "projects": {
    "my-app": {
      "architect": {
        "test": {
          "builder": "@angular/vitest:test"
        }
      }
    }
  }
}
```

## 今後の展望
- Angular CLI完全統合
- よりリッチなブラウザテスト機能
- Visual Testing機能の拡張

## 関連リソース
- [Vitest 4.0 Release Notes](https://vitest.dev/blog/vitest-4)
- [Angular Testing with Vitest](https://angular.io/guide/testing-vitest)
- [Browser Mode Documentation](https://vitest.dev/guide/browser)
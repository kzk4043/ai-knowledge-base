# React フレームワーク情報

**更新日**: 2025-09-07  
**カテゴリ**: 20_frontend/frameworks  

## 概要
Reactに関する最新情報、ベストプラクティス、パフォーマンス最適化などをまとめます。

## React Server Components (RSC)

### フレームワーク不要のRSC実装 🔴

**URL**: https://react.statuscode.com/issues/442  
**重要度**: 高  
**日付**: 2025-09-03  
**タグ**: #server-components, #framework-free, #react

#### 概要
Krasimir TsonevによるReact Server Componentsをフレームワークなしで使用するアプローチ。Next.jsのような重量級フレームワークに依存せずにRSCの機能を活用できる。

#### 主なメリット
- フレームワーク依存を避けた軽量な実装
- サーバーサイドとクライアントサイドの柔軟な分離
- よりカスタマイズ可能なアーキテクチャ

#### 技術的特徴
- コードをサーバーとクライアント間で分割可能
- 関連ツール: Waku（最小限のフレームワーク）

#### 関連リソース
- [オリジナル記事](https://krasimirtsonev.com)

## フレームワーク比較

### Astro vs Next.js 🟡

**URL**: https://newsletter.astroweekly.dev/p/astro-weekly-99  
**重要度**: 中  
**日付**: 2025-09-07  
**タグ**: #astro, #nextjs, #framework-comparison

#### 概要
モダンWeb開発におけるAstroとNext.jsの細かな選択基準についての比較記事。各フレームワークの適用場面の使い分けを解説。

### AstroでのReact使用方法 🟡

**URL**: https://www.youtube.com/watch?v=b9nbtjWQb5k  
**重要度**: 中  
**日付**: 2025-09-07  
**タグ**: #astro, #react, #integration

#### 概要
Chris PenningtonによるYouTube動画。ReactからAstroに移行する開発者向けの実践的なReact統合方法。

#### 3つの統合方法
1. **プロップスの受け渡し**: コンポーネント間のデータ伝達
2. **最適化された画像レンダリング**: `getImage()`を使用した画像処理
3. **APIルート経由のコンテンツ取得**: データフェッチング手法

#### 対象者
- ReactからAstroへの移行を検討中の開発者
- Astroでのコンポーネント統合を学びたい開発者

## React Hooks

### useState
基本的な状態管理Hook

```javascript
const [state, setState] = useState(initialValue);
```

### useEffect  
副作用を処理するHook

```javascript
useEffect(() => {
  // 副作用の処理
  return () => {
    // クリーンアップ
  };
}, [dependencies]);
```

## パフォーマンス最適化

### React.memo
コンポーネントの不要な再レンダリングを防ぐ

```javascript
const MemoizedComponent = React.memo(Component);
```

### useMemo / useCallback
計算結果や関数をメモ化

```javascript
const memoizedValue = useMemo(() => expensiveCalculation(), [deps]);
const memoizedCallback = useCallback(() => {}, [deps]);
```

## 関連リソース
- [React公式ドキュメント](https://react.dev)
- [React Hooks API](https://react.dev/reference/react)
# React フレームワーク情報

**更新日**: 2025-01-28  
**カテゴリ**: 20_frontend/frameworks  

## 概要
Reactに関する最新情報、ベストプラクティス、パフォーマンス最適化などをまとめます。

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
# React状態管理：localStorage vs Context/Redux/Zustand

## 概要
- **URL**: https://www.developerway.com/posts/can-we-use-local-storage-instead-of-context-redux-zustand
- **日付**: 2024-08-28
- **タグ**: React, State Management

## 核心的な学び

### localStorageの本質的制約
1. **React再レンダリングを自動トリガーしない** → 手動同期必須
2. **SSR非対応** → ハイドレーション時の不整合リスク
3. **開発複雑性** → 状態管理ライブラリより実装コスト高

### 適切な使い分け
- **localStorage**: テーマ設定、フォームバックアップ等の永続化
- **状態管理ライブラリ**: コンポーネント間の動的状態共有

### 実装例
```tsx
const useTheme = () => {
  const [theme, setTheme] = useState(() => 
    localStorage.getItem('theme') || 'light'
  );
  
  const toggleTheme = () => {
    const newTheme = theme === 'dark' ? 'light' : 'dark';
    setTheme(newTheme);
    localStorage.setItem('theme', newTheme);
  };
  
  return { theme, toggleTheme };
};
```

## 結論
localStorageは状態管理の代替ではなく、永続化の補完手段として活用する
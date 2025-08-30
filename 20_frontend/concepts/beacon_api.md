# Beacon API - ページ離脱時の確実なデータ送信

## 概要
Beacon APIは「fire-and-forget」型のリクエスト送信を可能にするWeb APIで、特にページ終了時やバックグラウンドでの軽量データ送信に特化している。

**URL**: https://hemath.dev/blog/say-bye-with-javascript-beacon/  
**日付**: 2025-01-30  
**重要度**: 🟡 中  
**タグ**: `Web API`, `JavaScript`, `Analytics`, `Performance`

---

## 主要ポイント

### 問題の背景
従来のXMLHttpRequestやfetchを`beforeunload`イベントで使用する場合の課題：
- リクエストの完了が不確実
- ブラウザがJavaScriptの実行完了を待たない
- ユーザー体験に遅延を引き起こす可能性

### Beacon APIの特徴
- **即時実行**: ブラウザの遅延なし
- **メモリ効率**: リクエスト後にメモリ上に何も保持しない
- **非同期**: コールバックやPromiseなし
- **軽量**: 少量のデータに最適化

## 実装方法

### 基本的な使用例
```javascript
// ページ離脱時の分析データ送信
navigator.sendBeacon('/analytics', JSON.stringify({ 
  event: 'page_leave',
  timestamp: Date.now()
}));
```

### イベントリスナーでの使用
```javascript
window.addEventListener('beforeunload', () => {
  navigator.sendBeacon('/api/session-end', JSON.stringify({
    sessionId: sessionStorage.getItem('sessionId'),
    duration: Date.now() - sessionStart
  }));
});
```

## 制限事項

- **データサイズ**: 少量のデータのみ送信可能
- **HTTPメソッド**: POSTリクエストのみサポート
- **レスポンス処理**: レスポンスを受け取れない（fire-and-forget）

## 従来手法との比較

| 方法 | 信頼性 | パフォーマンス | 複雑さ |
|------|--------|----------------|--------|
| XMLHttpRequest | 低 | 中 | 高 |
| fetch | 低 | 中 | 中 |
| Beacon API | 高 | 高 | 低 |

## 実用的な使用シーン

1. **Web Analytics**: ページビュー、セッション終了の記録
2. **ユーザー行動追跡**: 離脱パターンの分析
3. **エラーレポート**: 重要なエラー情報の送信
4. **A/Bテスト**: 実験結果の確実な記録

## 技術的な仕組み

Beacon APIはブラウザレベルで最適化されており：
- ブラウザのネットワークスタックを直接利用
- ページ終了後もリクエストが継続される
- OSレベルでのネットワーク処理により高い信頼性を実現

## 関連リソース

- [MDN Web Docs - Beacon API](https://developer.mozilla.org/en-US/docs/Web/API/Beacon_API)
- ブラウザサポート状況の確認が推奨される
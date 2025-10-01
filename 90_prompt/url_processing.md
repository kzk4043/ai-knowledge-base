# URL処理用サンプルプロンプト

記事などを読み、ドキュメントにまとめ、自分自身の理解を構造化していきたい。
以下のURLから技術記事を読み込み、ユーザープロファイルに基づいて分析し、ドキュメントに要約してください。

## URLs:
- https://developers.google.com/search/docs/appearance/google-images?hl=ja
- https://web.dev/explore/fast?hl=ja#optimize-your-images
- https://web.dev/articles/optimize-ttfb?hl=ja
- https://web.dev/articles/content-delivery-networks?hl=ja
- https://web.dev/articles/lcp-lazy-loading?hl=ja
- https://web.dev/articles/ttfb?hl=ja
- https://web.dev/articles/avoid-large-complex-layouts-and-layout-thrashing?utm_source=devtools&utm_campaign=stable&hl=ja#avoid-forced-synchronous-layouts
- https://web.dev/articles/optimize-long-tasks?utm_source=devtools&utm_campaign=stable&hl=ja
- https://developer.chrome.com/docs/lighthouse/performance/first-contentful-paint/?utm_source=lighthouse&utm_medium=lr
- https://developer.chrome.com/docs/lighthouse/performance/lighthouse-largest-contentful-paint/?utm_source=lighthouse&utm_medium=lr
- https://developers.google.com/search/docs/appearance/core-web-vitals?hl=ja

## 処理手順:
1. 各URLの内容を読み込む
   1. URL内にて別記事が紹介されている場合はそちらも対象にする
2. ユーザープロファイル（@00_setting/user_profile.md）と照合
3. 以下の形式でドキュメント化候補リストを提示し、ユーザに確認する

```
重要度: 
- 🔴（高） 
- 🟡（中）
- 🟢（低）

### 記事候補（優先度順）:
1. 🔴**[記事タイトル1]** 
  - 理由: [ユーザーの関心分野・技術レベルとの関連性説明]
2. 🟡**[記事タイトル2]** 
  - 理由: [関連性の説明]
3. 🟢**[記事タイトル3]** 
  - 理由: [関連性の説明]

どの記事を要約しますか？（番号で選択、複数可）
```

4. 記事の要約を実施し、構造化した上で、対象となるフォルダに要約を記載する
5. 要約完了後のフィードバック収集:

```
要約作業が完了したら、以下についてお聞かせください：

### プロファイル改善のためのフィードバック:
- 📊 **優先度評価**: 今回の重要度判定は適切でしたか？
- 🎯 **新規関心分野**: 新しく興味を持った技術分野はありますか？
- ❌ **除外希望**: 今後除外したいトピックや内容はありますか？
- 📈 **技術レベル**: スキルレベルに変化はありますか？
- 🎲 **その他**: プロファイルに反映すべき点はありますか？

このフィードバックを基に、次回からより精度の高い記事選別を行います。
```

6. ３でのユーザの選択およびフィードバックを元に、ユーザプロファイルを更新してください
7. 記事追加とプロファイル改善をした上で、リポジトリ全体の構造を再構築してください

### 更新対象:
- @00_setting/user_profile.md - 必要に応じてユーザプロファイル更新
- `CHANGELOG.md` - 変更内容の記録
- 記事追加による全体構造の見直し

## コンテキスト
- 全て日本語で記載
- 内容はシンプルに、重要なものだけ記載

## 最終指示
ユーザ特性にあった構造化されたドキュメントを作成してください

<!-- これはコメントなので無視して：@90_prompt/url_processing.md これを読んで実行して -->
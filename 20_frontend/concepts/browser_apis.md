# ブラウザAPI情報

**更新日**: 2025-09-07  
**カテゴリ**: 20_frontend/concepts  

## 概要
ブラウザの内部動作やAPIの仕組みに関する技術情報をまとめます。

## タイマー機能

### ブラウザのタイマーThrottling 🟡

**URL**: https://javascriptweekly.com/issues/751  
**重要度**: 中  
**日付**: 2025-09-05  
**タグ**: #browser, #timers, #performance, #throttling

#### 概要
Nolan Lawsonによる記事「Why Do Browsers Throttle JavaScript Timers?」の要約。ブラウザがJavaScriptタイマーをスロットルする理由と影響について解説。

#### 主なポイント
- `setTimeout(0)`は実際には0ミリ秒で実行されない
- ブラウザは最低数ミリ秒の遅延を設ける（clamp）
- 精密なタイミングに依存するコードのパフォーマンスに影響

#### 技術的背景
- ブラウザによるタイマー最適化機能
- CPUリソース管理のための制限

#### 開発者への影響
- `setTimeout`や類似関数の実際の動作理解
- 代替アプローチの検討が必要な場合がある

#### 対策
- 記事では回避策も提案（詳細は元記事参照）

#### 関連リソース
- [元記事](https://nolanlawson.com)
# フレームワークパフォーマンス比較 - 同一アプリ10種類実装

**URL**: https://www.lorenstew.art/blog/10-kanban-boards/  
**日付**: 2025年11月  
**重要度**: 🟡 中  
**タグ**: フレームワーク比較, パフォーマンス, モバイル, バンドルサイズ, React, Vue, Svelte

## 概要

同一のKanbanボードアプリを10種類のフレームワークで実装し、モバイル環境でのパフォーマンスを比較。バンドルサイズ、読み込み時間、実行速度を詳細に分析した包括的研究。

## テスト対象フレームワーク

### 1. Next.js (React 19)
```javascript
// App Router + React Server Components
export default function KanbanBoard() {
  return (
    <div className="kanban-board">
      <TaskColumn title="To Do" tasks={tasks} />
    </div>
  );
}
```

### 2. TanStack Start (React)
```javascript
// TanStack Router + React
import { createFileRoute } from '@tanstack/react-router'

export const Route = createFileRoute('/kanban')({
  component: KanbanBoard
})
```

### 3. TanStack Start + Solid
```javascript
// SolidJS + TanStack Start
function KanbanBoard() {
  const [tasks, setTasks] = createSignal([]);
  return <div>...</div>;
}
```

### 4. Nuxt (Vue 3)
```vue
<!-- pages/kanban.vue -->
<template>
  <div class="kanban-board">
    <TaskColumn v-for="column in columns" :key="column.id" />
  </div>
</template>
```

### 5. Analog (Angular)
```typescript
// Angular with Analog meta-framework
@Component({
  selector: 'kanban-board',
  template: '<task-column *ngFor="let column of columns"></task-column>'
})
export class KanbanBoardComponent {}
```

### 6. Marko
```marko
<!-- kanban-board.marko -->
<div class="kanban-board">
  <task-column for(column in input.columns) column=column/>
</div>
```

### 7. SolidStart
```javascript
// SolidStart routing
export default function KanbanBoard() {
  return (
    <div class="kanban-board">
      <For each={columns()}>{(column) => <TaskColumn column={column} />}</For>
    </div>
  );
}
```

### 8. SvelteKit
```svelte
<!-- routes/kanban/+page.svelte -->
<script>
  import TaskColumn from '$lib/TaskColumn.svelte';
  export let data;
</script>

<div class="kanban-board">
  {#each data.columns as column}
    <TaskColumn {column} />
  {/each}
</div>
```

### 9. Qwik City
```javascript
// Qwik resumability
export default component$(() => {
  return (
    <div class="kanban-board">
      {columns.map(column => <TaskColumn column={column} />)}
    </div>
  );
});
```

### 10. Astro + HTMX
```astro
---
// kanban.astro
const columns = await getColumns();
---
<div class="kanban-board" hx-boost="true">
  {columns.map(column => <TaskColumn column={column} />)}
</div>
```

## パフォーマンス結果

### バンドルサイズ比較（圧縮後）

```javascript
const bundleSizes = {
  'Marko': '28.8 kB',           // 🥇 最小
  'Astro + HTMX': '32.1 kB',
  'SvelteKit': '45.7 kB',
  'Qwik City': '52.3 kB',
  'SolidStart': '67.4 kB',
  'TanStack + Solid': '71.8 kB',
  'Analog (Angular)': '89.6 kB',
  'Nuxt (Vue 3)': '98.2 kB',
  'TanStack Start': '134.5 kB',
  'Next.js (React 19)': '176.1 kB'  // 最大
};

// 差異: 最大39倍の差（176.1 / 28.8 ≈ 6.11倍）
```

### First Contentful Paint (FCP)

```javascript
const fcpTimes = {
  'Marko': '35ms',
  'Astro + HTMX': '38ms',
  'SvelteKit': '42ms',
  'SolidStart': '45ms',
  'Qwik City': '48ms',
  'TanStack + Solid': '52ms',
  'Nuxt (Vue 3)': '58ms',
  'Analog (Angular)': '61ms',
  'TanStack Start': '67ms',
  'Next.js': '71ms'
};

// すべて類似のFCP時間（35-71ms）
// バンドルサイズほど差が出ない理由：初期表示に必要な部分のみ優先読み込み
```

### モバイル3G環境での読み込み時間

```javascript
const mobileLoadTimes = {
  'Marko': '1.2s',
  'Astro + HTMX': '1.4s',
  'SvelteKit': '1.8s',
  'SolidStart': '2.1s',
  'Qwik City': '2.3s',
  'TanStack + Solid': '2.7s',
  'Nuxt (Vue 3)': '3.2s',
  'Analog (Angular)': '3.6s',
  'TanStack Start': '4.8s',
  'Next.js': '5.9s'
};
```

## 技術的分析

### パフォーマンス要因

#### 1. コンパイル戦略
```javascript
// Svelte/SolidJS: コンパイル時最適化
// バンドルサイズが小さい理由：ランタイムが軽量

// React/Vue: ランタイムフレームワーク
// バンドルサイズが大きい理由：フレームワーク本体を含む
```

#### 2. ハイドレーション戦略
```javascript
// Qwik: Resumability（ハイドレーション不要）
// Astro: 部分ハイドレーション
// 従来: 全体ハイドレーション（React、Vue等）
```

#### 3. バンドル分割
```javascript
// Next.js: 自動コード分割
import('./heavy-component').then(Component => {
  // 遅延読み込み
});

// しかし基本バンドルサイズが大きい
```

### フレームワーク特性分析

#### 軽量フレームワーク（<50kB）
- **Marko**: eBayが開発、コンパイル最適化
- **Astro**: 静的サイト重視、部分ハイドレーション
- **SvelteKit**: コンパイル戦略、ランタイム軽量

#### 中量フレームワーク（50-100kB）
- **SolidStart**: 細粒度リアクティビティ
- **Qwik**: Resumability、遅延実行
- **Angular**: エンタープライズ向け機能豊富

#### 重量フレームワーク（>100kB）
- **React系**: 豊富なエコシステム、開発者体験
- **Vue系**: 段階的導入、バランス型

## 実用的考察

### フレームワーク選定指針

#### プロジェクト規模別推奨
```javascript
const recommendations = {
  'Landing Page': ['Astro', 'SvelteKit', 'Marko'],
  'SPA (小〜中規模)': ['SolidStart', 'SvelteKit', 'Qwik'],
  'SPA (大規模)': ['Next.js', 'Nuxt', 'TanStack Start'],
  'Enterprise': ['Angular', 'Next.js', 'Nuxt']
};
```

#### パフォーマンス要件別
```javascript
const performanceFirst = {
  'モバイル最適化': ['Marko', 'SvelteKit', 'Astro'],
  'SEO重視': ['Next.js', 'Nuxt', 'SvelteKit'],
  'インタラクティブ': ['SolidStart', 'Qwik', 'React'],
  '開発速度': ['Next.js', 'Nuxt', 'SvelteKit']
};
```

### トレードオフ分析

#### バンドルサイズ vs 開発者体験
```javascript
// React: 大きなバンドル vs 豊富なエコシステム
// Svelte: 小さなバンドル vs 新しいエコシステム
// Vue: バランス型 vs 中途半端？
```

#### パフォーマンス vs 機能性
```javascript
// Astro: 優秀なパフォーマンス vs 限定的なインタラクティビティ
// Next.js: 豊富な機能 vs 大きなバンドル
// Qwik: 革新的な戦略 vs 学習コスト
```

## 結論と提言

### 主要な発見

1. **バンドルサイズの重要性**: モバイル環境で最大6倍の差
2. **コンパイル戦略の優位性**: Svelte、SolidJSが優秀
3. **フレームワーク成熟度**: Reactエコシステムは大きいが重い
4. **新しいアプローチ**: Qwik、Astroの革新的戦略

### ユーザープロファイルとの関連

#### React開発者への示唆
```javascript
// React使用継続 + パフォーマンス最適化
// - バンドル分析（webpack-bundle-analyzer）
// - 不要なライブラリ削除
// - 動的インポート活用
// - React Compiler活用（v19）
```

#### フレームワーク移行検討
```javascript
// パフォーマンス要件が厳しい場合
// React → SolidStart or SvelteKit
// 学習コストは高いが性能向上は確実
```

### 技術選定の指針

1. **パフォーマンス最優先**: Marko、SvelteKit、Astro
2. **開発効率重視**: Next.js、Nuxt、TanStack Start
3. **バランス重視**: SolidStart、Qwik、SvelteKit
4. **エンタープライズ**: Angular、Next.js

この比較研究は、フレームワーク選定において「なんとなくReact」ではなく、要件に基づいた技術選択の重要性を示している。特にモバイルファーストの現在、パフォーマンスは無視できない要素である。
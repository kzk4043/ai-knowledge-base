# TypeScript - 4つの非従来型キャスト手法

## メタデータ
- **URL**: https://wolfgirl.dev/blog/2025-10-22-4-unconventional-ways-to-cast-in-typescript/
- **日付**: 2025-10-31  
- **重要度**: 🔴 高
- **タグ**: TypeScript, 型キャスト, 高度な型システム

## 概要
TypeScriptの4つの非従来型キャスト手法を解説。通常のキャストでは対応できない特殊なケースでの技術だが、**本番環境では使用すべきでない**アンチパターン。

## ⚠️ 重要な注意点
- これらの手法は**本番コードで使用禁止**
- **フットガン（自分を撃つ銃）**として危険
- 学術的興味・TypeScript型システムの理解のみが目的

## 4つの手法

### 1. Unknown経由キャスト
```typescript
const value = (someValue as unknown) as TargetType;
```
- TypeScriptが推奨する「意図的な場合はunknownを経由」を悪用
- 任意の型間での強制変換が可能

### 2. Type Predicate (is) キャスト  
```typescript
function isCast<T>(value: any): value is T {
  return true; // 常にtrue
}

if (isCast<TargetType>(someValue)) {
  // someValueはTargetType扱い
}
```
- 型ガードの`is`演算子を悪用
- **truthyな値でのみ動作**

### 3. Void関数の共変性
```typescript
const cast = <T>(value: any): T => {
  return ((() => value) as () => void as () => T)();
};
```
- `() => void`型への変換の共変性を悪用
- 関数戻り値型での強制キャスト

### 4. Object.assign + Never型
```typescript
const cast = <T>(value: any): T => {
  return Object.assign(value, {} as never);
};
```
- `never`型との`Object.assign`を活用
- オブジェクト操作での型変換

## 安全な代替手法

### 推奨される方法
```typescript
// 1. asキャストの使用  
const value = someValue as TargetType;

// 2. satisfies演算子（TypeScript 4.9+）
const config = {
  endpoint: '/api'
} satisfies Config;

// 3. 適切な型ガード
function isString(value: unknown): value is string {
  return typeof value === 'string';
}
```

### typescript-eslint設定
```json
{
  "rules": {
    "@typescript-eslint/no-explicit-any": "error",
    "@typescript-eslint/no-unsafe-assignment": "error"
  }
}
```

## 学習価値
- TypeScript型システムの境界理解
- 型安全性の重要性の再認識
- 適切なキャスト手法の必要性

## 関連リソース
- [TypeScript Handbook - Type Assertions](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions)
- [typescript-eslint Rules](https://typescript-eslint.io/rules/)
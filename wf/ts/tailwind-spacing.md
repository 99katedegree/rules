# Tailwindのspacing

## 適用対象

全プロジェクト共通（Tailwind CSS v4）。

## 規約

余白（padding / margin / gap など）は `sm` / `md` / `lg` / `xl` の4段階を使う。加えて余白なしの `0` と、1pxだけ空けたい場合用の `1` を用意する。

値は `rem` で定義する（ルートフォントサイズ16px換算）。ただし `0` / `1` は `px` のままにする。

| 名前 | 値 | px換算 |
| --- | --- | --- |
| `0` | `0px` | 0px |
| `1` | `1px` | 1px |
| `sm` | `0.375rem` | 6px |
| `md` | `0.625rem` | 10px |
| `lg` | `1rem` | 16px |
| `xl` | `1.625rem` | 26px |

Tailwind v4 の `@theme` ブロックで定義する。あわせてデフォルトのspacingスケールを `initial` で無効化し、`p-4` や `mt-2` のような数値ベースのユーティリティクラスを生成させない。

```css
@theme {
  --spacing: initial;
  --spacing-0: 0px;
  --spacing-1: 1px;
  --spacing-sm: 0.375rem;
  --spacing-md: 0.625rem;
  --spacing-lg: 1rem;
  --spacing-xl: 1.625rem;
}
```

```tsx
<div className="p-md gap-sm mt-lg">
```

`xl`（1.625rem / 26px）より大きい余白が必要な場合は、任意の値を `xxx-[xxxxrem]` の形式で直接指定する。こちらも `rem` で書く。

```tsx
<div className="p-[2.5rem] gap-[4rem]">
```

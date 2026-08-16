# Tailwindのカラー

## 適用対象

全プロジェクト共通（Tailwind CSS v4）。

## 規約

### zincベース

カラーは基本的に `zinc` ベースで作成する。グレースケールが必要な箇所では `slate` / `gray` / `neutral` / `stone` ではなく `zinc` を使う。

### `--color-base`

`--color-base` は背景色を表す。ライトモードは `zinc-50`、ダークモードは `zinc-950`。

モードで値を切り替えるため、素の変数を `@theme inline` 経由で参照する。

```css
:root {
  --base: var(--color-zinc-50);
}

.dark {
  --base: var(--color-zinc-950);
}

@theme inline {
  --color-base: var(--base);
}
```

```tsx
<div className="bg-base">
```

### `white` / `black` は zinc に差し替える

純粋な `#fff` / `#000` は使わない。`--color-white` と `--color-black` を `@theme` で上書きし、zinc の値を指すようにする。`bg-white` / `text-black` はそのまま使えるが、実際に描画される色は zinc になる。

| 変数 | 差し替え先 |
| --- | --- |
| `--color-white` | `zinc-50` |
| `--color-black` | `zinc-950` |

```css
@theme {
  --color-white: var(--color-zinc-50);
  --color-black: var(--color-zinc-950);
}
```

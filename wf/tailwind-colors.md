# Tailwindのカラー

## 適用対象

全プロジェクト共通（Tailwind CSS v4）。

## 規約

### zincベース

カラーは基本的に `zinc` ベースで作成する。グレースケールが必要な箇所では `slate` / `gray` / `neutral` / `stone` ではなく `zinc` を使う。

### モードで切り替わるカラー

以下はライトモードとダークモードで値を切り替える。

| 変数 | ライトモード | ダークモード |
| --- | --- | --- |
| `--color-base` | `zinc-50` | `zinc-950` |
| `--color-main` | `zinc-200` | `zinc-800` |
| `--color-hover` | `zinc-300` | `zinc-500` |
| `--color-popover` | `zinc-100` | `zinc-900` |

`--color-base` は背景色を表す。

モードで値を切り替えるため、素の変数を `@theme inline` 経由で参照する。通常の `@theme` だと変数が `:root` で解決されてしまい、`.dark` での上書きが効かない。

```css
:root {
  --base: var(--color-zinc-50);
  --main: var(--color-zinc-200);
  --hover: var(--color-zinc-300);
  --popover: var(--color-zinc-100);
}

.dark {
  --base: var(--color-zinc-950);
  --main: var(--color-zinc-800);
  --hover: var(--color-zinc-500);
  --popover: var(--color-zinc-900);
}

@theme inline {
  --color-base: var(--base);
  --color-main: var(--main);
  --color-hover: var(--hover);
  --color-popover: var(--popover);
}
```

```tsx
<div className="bg-base">
  <button className="bg-main hover:bg-hover">
</div>
```

`--color-popover` はポップオーバーやドロップダウンなど、浮いて表示される要素の背景色。ライト・ダークとも `base` と `main` の中間の明度に置き、どちらの面の上に出しても輪郭が出るようにしている。明度差は小さいので、border と shadow も併せて付ける。

```tsx
<div className="bg-popover border border-main shadow-lg">
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

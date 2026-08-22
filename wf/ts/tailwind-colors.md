# Tailwindのカラー

## 適用対象

全プロジェクト共通（Tailwind CSS v4）。

## 規約

### グレースケールのベース色

カラーは1つのグレースケールをベースに作成する。ベース色はプロジェクトごとに以下のいずれかから選ぶ。

- `slate`
- `gray`
- `zinc`
- `neutral`
- `stone`
- `taupe`
- `mauve`
- `mist`

選んだ色はプロジェクト内で固定し、グレースケールが必要な箇所ではその1色だけを使う。複数を混ぜない。

以下このドキュメントでは、選んだベース色を `<base>` と表記する（`<base>-50` は `zinc` を選んだなら `zinc-50`）。コード例は `zinc` を選んだ場合のもの。

### モードで切り替わるカラー

以下はライトモードとダークモードで値を切り替える。

| 変数 | ライトモード | ダークモード |
| --- | --- | --- |
| `--color-base` | `<base>-50` | `<base>-950` |
| `--color-main` | `<base>-200` | `<base>-800` |
| `--color-accent` | `<base>-300` | `<base>-500` |
| `--color-popover` | `<base>-100` | `<base>-900` |

`--color-base` は背景色を表す。

モードで値を切り替えるため、素の変数を `@theme inline` 経由で参照する。通常の `@theme` だと変数が `:root` で解決されてしまい、`.dark` での上書きが効かない。

```css
:root {
  --base: var(--color-zinc-50);
  --main: var(--color-zinc-200);
  --accent: var(--color-zinc-300);
  --popover: var(--color-zinc-100);
}

.dark {
  --base: var(--color-zinc-950);
  --main: var(--color-zinc-800);
  --accent: var(--color-zinc-500);
  --popover: var(--color-zinc-900);
}

@theme inline {
  --color-base: var(--base);
  --color-main: var(--main);
  --color-accent: var(--accent);
  --color-popover: var(--popover);
}
```

```tsx
<div className="bg-base">
  <button className="bg-main hover:bg-accent">
</div>
```

`--color-accent` は要素が強調されている状態の面を表す。hover に限らず focus や選択中など、強調される場面すべてに使う。名前は shadcn/ui の同名変数に合わせたもので、ブランドのアクセントカラーではなくベース色の一段階として扱う。

```tsx
<div className="hover:bg-accent focus-visible:bg-accent aria-selected:bg-accent">
```

`--color-popover` はポップオーバーやドロップダウンなど、浮いて表示される要素の背景色。ライト・ダークとも `base` と `main` の中間の明度に置き、どちらの面の上に出しても輪郭が出るようにしている。明度差は小さいので、border と shadow も併せて付ける。

```tsx
<div className="bg-popover border border-main shadow-lg">
```

### `white` / `black` はベース色に差し替える

純粋な `#fff` / `#000` は使わない。`--color-white` と `--color-black` を `@theme` で上書きし、ベース色の値を指すようにする。`bg-white` / `text-black` はそのまま使えるが、実際に描画される色はベース色になる。

| 変数 | 差し替え先 |
| --- | --- |
| `--color-white` | `<base>-50` |
| `--color-black` | `<base>-950` |

```css
@theme {
  --color-white: var(--color-zinc-50);
  --color-black: var(--color-zinc-950);
}
```

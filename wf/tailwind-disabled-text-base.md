# 使わないTailwindフォントサイズ

## 適用対象

全プロジェクト共通（Tailwind CSS v4）。

## 規約

`text-base` クラスは使わない。`text-base` はフォントサイズだけでなく font-weight（`--text-base--font-weight`）も同時に持つため、両方を無効化する。

Tailwind v4 の `@theme` ブロックで `--text-base` と `--text-base--font-weight` を `initial` に上書きして無効化する。`text-base` ユーティリティクラス自体が生成されなくなる。

```css
@theme {
  --text-base: initial;
  --text-base--font-weight: initial;
}
```

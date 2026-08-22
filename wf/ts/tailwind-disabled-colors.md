# 使わないTailwindカラー

## 適用対象

全プロジェクト共通（Tailwind CSS v4）。

## 規約

以下のカラーパレットは使わない。

- `green`
- `emerald`
- `teal`
- `cyan`
- `olive`

Tailwind v4 の `@theme` ブロックで、該当パレットを `initial` に上書きして無効化する。`bg-green-500` のようなユーティリティクラス自体が生成されなくなる。

```css
@theme {
  --color-green-*: initial;
  --color-emerald-*: initial;
  --color-teal-*: initial;
  --color-cyan-*: initial;
  --color-olive-*: initial;
}
```

# パッケージマネージャ

## 適用対象

React プロジェクト。

## 規約

プロジェクトを開始する際は bun を用いる。React + TypeScript + Oxlint の組み合わせで作成する（`react-ts` テンプレートはリンターがデフォルトで Oxlint になる）。フォーマッタは `oxfmt` を追加する。

```bash
bun create vite . --template react-ts --no-interactive
bun add -d oxfmt
bun install
bun run dev
```

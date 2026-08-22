# パッケージマネージャ

## 適用対象

Next.js プロジェクト。

## 規約

プロジェクトを開始する際は bun を用いる。TypeScript + Tailwind + App Router + `src/` ディレクトリのみ有効にし、それ以外（ESLint、React Compiler、AGENTS.md）はなしにする。リンター・フォーマッタは `create-next-app` のセットアップに任せず、`oxlint` と `oxfmt` を別途追加する。

```bash
bun create next-app . --ts --tailwind --app --src-dir --no-eslint --no-agents-md
bun add -d oxlint oxfmt
```

`create-next-app` は対話質問がプロジェクト名（ディレクトリ名を引数で渡せば聞かれない）のみで、それ以外はすべてフラグで指定したとおりに決まる。依存関係のインストールも bun で自動的に行われる。

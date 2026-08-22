# パスエイリアス

## 適用対象

React プロジェクト。[nextjs/path-alias.md](../nextjs/path-alias.md) をベースに、Vite での設定手順を加えたもの。

## 規約

`src` 直下のディレクトリ（[directory-structure.md](./directory-structure.md) 参照）に対応する `@features` / `@shared` / `@generated` の3つのエイリアスを生成する。

- `app` ディレクトリがないため、nextjs 側の「`app` のエイリアスは作らない」はそのまま該当しない。エイリアスは3つのみで、`main.tsx` / `App.tsx` / `globals.css` に対するエイリアスは作らない。
- 相対パスは同一コンポーネントフォルダ内（`parts` や hook の import）でのみ使い、それ以外のディレクトリをまたぐ import はすべてエイリアスを使う。

```ts
import { PostCard } from "@features/post/components/PostCard/PostCard";
import { Input } from "@shared/components/Input/Input";
import type { Post } from "@generated/api";
```

## 手順

Vite は `tsconfig.json` の `paths` を自動では解決しないため、TypeScript 側とバンドラ側の両方に設定が必要になる。設定を二重管理しないよう、`vite-tsconfig-paths` を入れて tsconfig を単一の定義元にする。

1. プラグインを追加する。

```bash
bun add -d vite-tsconfig-paths
```

2. `tsconfig.app.json` の `compilerOptions` に `paths` を追加する（`react-ts` テンプレートではアプリのコンパイラ設定が `tsconfig.app.json` に分かれているため、ルートの `tsconfig.json` ではなくこちらに書く）。

```json
{
  "compilerOptions": {
    "paths": {
      "@features/*": ["./src/features/*"],
      "@shared/*": ["./src/shared/*"],
      "@generated/*": ["./src/generated/*"]
    }
  }
}
```

3. `vite.config.ts` にプラグインを登録する。

```ts
import react from "@vitejs/plugin-react";
import { defineConfig } from "vite";
import tsconfigPaths from "vite-tsconfig-paths";

export default defineConfig({
  plugins: [react(), tsconfigPaths()],
});
```

4. `bun run dev` で解決できることを確認する。

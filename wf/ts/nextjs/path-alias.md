# パスエイリアス

## 適用対象

Next.js プロジェクト。

## 規約

`src` 直下のディレクトリ（[directory-structure.md](./directory-structure.md) 参照）に対応する `@features` / `@shared` / `@generated` の3つのエイリアスを生成する。

- `create-next-app` がデフォルトで生成する `@/*` は残さない。必ず削除したうえで3つのエイリアスに置き換える（`@/*` を残すと `src` 直下を指す抜け道ができ、`app` を含めどこでも import できてしまうため）。
- `app` のエイリアスは作らない。`app` 配下は Next.js のルーティング専用で、外から import しない。
- 相対パスは同一コンポーネントフォルダ内（`parts` や hook の import）でのみ使い、それ以外のディレクトリをまたぐ import はすべてエイリアスを使う。

```ts
import { PostCard } from "@features/post/components/PostCard/PostCard";
import { Input } from "@shared/components/Input/Input";
import type { Post } from "@generated/api";
```

## 手順

Next.js は `tsconfig.json` の `paths` をそのままバンドラの解決に使うため、`tsconfig.json` の編集だけでよい。

`create-next-app` には `--import-alias <prefix/*>` があるが、指定できるのは1つだけで、しかも必ず `./src/*` へのマッピングになる（例: `--import-alias "@features/*"` → `"@features/*": ["./src/*"]`）。3つのエイリアスは作れないので、scaffold 後に `tsconfig.json` を編集する。

1. `tsconfig.json` の `compilerOptions.paths` にあるデフォルトの `"@/*": ["./src/*"]` を消し、以下の3つに置き換える（追記ではなく置き換え。`@/*` の行は残さない）。

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

2. `bun run dev` で解決できることを確認する。

scaffold 直後の `src/app` には `@/` を使った import がないため、書き換えが必要なファイルはない（`layout.tsx` の `globals.css` は相対 import）。

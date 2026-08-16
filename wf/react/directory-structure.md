# ディレクトリ構成

## 適用対象

React プロジェクト。[nextjs/directory-structure.md](../nextjs/directory-structure.md) をベースに、Next.js 固有の `app` ディレクトリを持たない構成にしたもの。

## 規約

`nextjs/directory-structure.md` との変更点は以下の2点のみ。

- `app` ディレクトリは作らない。
- Vite scaffold の `index.css` / `App.css` は削除し、代わりに `globals.css` に一本化する。

それ以外（`hooks` ディレクトリを作らずコンポーネントに hook を切り分ける方針、コンポーネントのフォルダ名・ファイル名を PascalCase で統一し同名にする方針、hook ファイルは camelCase にする方針）は nextjs と同じ。

```
src
├── main.tsx
├── App.tsx
├── globals.css
├── components
│   ├── features
│   │   └── post
│   │       └── PostCard
│   │           ├── PostCard.tsx
│   │           ├── PostCard.stories.tsx
│   │           ├── PostCard.test.tsx
│   │           └── usePostCard.ts
│   └── shared
│       └── Input
│           ├── Input.tsx
│           ├── Input.stories.tsx
│           ├── Input.test.tsx
│           └── useInput.ts
├── constants
├── lib
├── stores
└── utils
```

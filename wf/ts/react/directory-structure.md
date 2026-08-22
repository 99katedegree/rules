# ディレクトリ構成

## 適用対象

React プロジェクト。[nextjs/directory-structure.md](../nextjs/directory-structure.md) をベースに、Next.js 固有の `app` ディレクトリを持たない構成にしたもの。

## 規約

`nextjs/directory-structure.md` との変更点は以下の2点のみ。

- `app` ディレクトリは作らない。`src` 直下のディレクトリは `features` / `shared` / `generated` の3つで、ファイルは `main.tsx` / `App.tsx` / `globals.css` の3つのみ置く。
- Vite scaffold の `index.css` / `App.css` は削除し、代わりに `globals.css` に一本化する。

それ以外（feature と `shared` を `components` / `constants` / `lib` / `stores` / `utils` に分ける方針、`generated` にコード生成物をすべて置く方針、`hooks` ディレクトリを作らずコンポーネントに hook を切り分ける方針、コンポーネントのフォルダ名・ファイル名を PascalCase で統一し同名にする方針、hook ファイルは camelCase にする方針、そのコンポーネント内でのみ使うサブコンポーネントを `parts` に直接置き test・story・hook は置かない方針）は nextjs と同じ。`app` に `parts` を作らない方針は、`src` 直下（`App.tsx`）に `parts` を作らない方針に読み替える。

```
src
├── main.tsx
├── App.tsx
├── globals.css
├── features
│   └── post
│       ├── components
│       │   └── PostCard
│       │       ├── PostCard.tsx
│       │       ├── PostCard.stories.tsx
│       │       ├── PostCard.test.tsx
│       │       ├── usePostCard.ts
│       │       └── parts
│       │           ├── PostCardHeader.tsx
│       │           └── PostCardBody.tsx
│       ├── constants
│       ├── lib
│       ├── stores
│       └── utils
├── shared
│   ├── components
│   │   └── Input
│   │       ├── Input.tsx
│   │       ├── Input.stories.tsx
│   │       ├── Input.test.tsx
│   │       └── useInput.ts
│   ├── constants
│   ├── lib
│   ├── stores
│   └── utils
└── generated
```

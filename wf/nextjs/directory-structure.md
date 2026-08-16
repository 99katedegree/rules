# ディレクトリ構成

## 適用対象

Next.js プロジェクト。

## 規約

`hooks` ディレクトリは作らない。汎用的に使いたい hook がある場合は、コンポーネントを切り分けてそこに hook を配置する。

コンポーネントのフォルダ名・ファイル名は PascalCase で統一し、同名にする（フォルダ名 = ファイル名）。hook ファイルは camelCase（`use` から始まる関数名と同じ表記）。Next.js が名前を固定するファイル（`page.tsx` 等）はそのまま小文字。

```
src
├── app
│   ├── page.tsx
│   ├── PageClient.tsx
│   ├── PageClient.stories.tsx
│   └── PageClient.test.tsx
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

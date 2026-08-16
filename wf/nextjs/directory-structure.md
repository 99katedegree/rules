# ディレクトリ構成

## 適用対象

Next.js プロジェクト。

## 規約

`hooks` ディレクトリは作らない。汎用的に使いたい hook がある場合は、コンポーネントを切り分けてそこに hook を配置する。

コンポーネントのフォルダ名・ファイル名は PascalCase で統一し、同名にする（フォルダ名 = ファイル名）。hook ファイルは camelCase（`use` から始まる関数名と同じ表記）。Next.js が名前を固定するファイル（`page.tsx` 等）はそのまま小文字。

そのコンポーネント内でのみ使うサブコンポーネントは `items` ディレクトリに格納する。`items` の中はフォルダを切らず、コンポーネントファイルを直接置く。test・story・hook は `items` には置かず、親コンポーネント側でまとめて扱う。複数のコンポーネントから使うようになった時点で `components` 配下へ引き上げる。

`items` は `components` 配下のコンポーネントにのみ作る。`app` ディレクトリには作らず、切り出したいコンポーネントは `components` 配下に置く。

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
│   │           ├── usePostCard.ts
│   │           └── items
│   │               ├── PostCardHeader.tsx
│   │               └── PostCardBody.tsx
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

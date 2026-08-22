# ディレクトリ構成

## 適用対象

Next.js プロジェクト。

## 規約

### トップレベル

`src` 直下は `app` / `features` / `shared` / `generated` の4つのみ。`globals.css` を含め、ファイルを `src` 直下に直接置かない（`globals.css` は `app` に置く）。

- `app`: ルーティング（Next.js が名前を固定するファイル）と、そのページ専用のコンポーネント、`globals.css`。
- `features`: 機能単位のディレクトリ。各 feature の中を `components` / `constants` / `lib` / `stores` / `utils` に分ける。
- `shared`: 複数の feature から使うもの。中身の分け方は feature と同じ。
- `generated`: コード生成物（API クライアント、スキーマ型、GraphQL 型など）をすべてここへ置く。手で編集せず、lint / format の対象外にする。

feature 内のものを複数の feature から使うようになった時点で `shared` の同名ディレクトリへ引き上げる。

### 命名

コンポーネントのフォルダ名・ファイル名は PascalCase で統一し、同名にする（フォルダ名 = ファイル名）。hook ファイルは camelCase（`use` から始まる関数名と同じ表記）。Next.js が名前を固定するファイル（`page.tsx` 等）はそのまま小文字。

### hook

`hooks` ディレクトリは作らない。汎用的に使いたい hook がある場合は、コンポーネントを切り分けてそこに hook を配置する。

### parts

そのコンポーネント内でのみ使うサブコンポーネントは、コンポーネントのフォルダ内の `parts` ディレクトリに格納する。

- `parts` の中はフォルダを切らず、コンポーネントファイルを直接置く。
- test・story・hook は `parts` には置かず、親コンポーネント側でまとめて扱う。
- `parts` は `features` / `shared` 配下のコンポーネントにのみ作る。`app` には作らず、切り出したいコンポーネントは `features` 配下に置く。

```
src
├── app
│   ├── globals.css
│   ├── layout.tsx
│   ├── page.tsx
│   ├── PageClient.tsx
│   ├── PageClient.stories.tsx
│   └── PageClient.test.tsx
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

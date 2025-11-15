# Project Structure

## Organization Philosophy

**Vite標準構成ベースの段階的拡張**: 初期段階では`src/`直下にシンプルな構成を維持し、実装進行に伴いfeature-first/domain-drivenパターンへ移行予定。

## Directory Patterns

### Entry Points

**Location**: `/src/`
**Purpose**: アプリケーションエントリーポイントとルートコンポーネント
**Example**:
```
src/
├── main.tsx      # ReactDOMレンダリングエントリー
├── App.tsx       # ルートコンポーネント
└── index.css     # グローバルスタイル
```

### Future Patterns (実装時に追加予定)

- **Components**: `/src/components/` - UI部品 (feature/ui/commonに分類)
- **Features**: `/src/features/` - 機能別モジュール (profiles, learning, statistics)
- **State**: `/src/stores/` - Zustand stores
- **Types**: `/src/types/` - 共通型定義
- **Utils**: `/src/utils/` - 汎用ヘルパー関数

## Naming Conventions

- **Files**:
  - Components: `PascalCase.tsx` (e.g., `ProfileCard.tsx`)
  - Utilities/Stores: `camelCase.ts` (e.g., `profileStore.ts`)
  - Types: `PascalCase.ts` または `types.ts`
- **Components**: PascalCaseで関数名とファイル名を一致させる
- **Functions**: camelCase、純粋関数を優先

## Import Organization

Prettier + @trivago/prettier-plugin-sort-imports による自動ソート:

```typescript
// 1. React/外部ライブラリ
import { useState } from 'react'
import { create } from 'zustand'

// 2. 内部モジュール (絶対パス優先)
import { ProfileCard } from '@/components/ProfileCard'

// 3. 相対パス
import { formatDate } from './utils'
```

**Path Aliases** (tsconfig.json):
- `@/`: `./src/` にマッピング予定 (baseUrl設定済み、エイリアスは実装時に追加)

## Code Organization Principles

- **境界管理**: eslint-plugin-boundaries による依存方向制御
- **厳格な依存関係**: eslint-plugin-strict-dependencies でcircular dependency防止
- **関数型指向**: eslint-plugin-functional による副作用管理
- **セキュリティ**: eslint-plugin-security による脆弱性パターン検出
- **Component Isolation**: Storybook によるコンポーネント独立開発

## Project Configurations

重要な設定ファイル:
- `tsconfig.json`: TypeScript strict設定の基準
- `eslint.config.js`: 品質基準のソースオブトゥルース
- `vite.config.ts`: ビルド/開発サーバー設定
- `lefthook.yml`: Git hooks自動化定義
- `pnpm-workspace.yaml`: Monorepo/Catalog設定

---
_created: 2025-11-15_
_Note: 構造は実装進行に伴い feature-first パターンへ進化する想定_

# Technology Stack

## Architecture

**フロントエンドオンリーSPA**: サーバー不要のクライアントサイド完結型アーキテクチャ。すべてのデータはブラウザローカルストレージ/IndexedDBで管理。

## Core Technologies

- **Language**: TypeScript 5.x (strict mode, exactOptionalPropertyTypes有効)
- **Framework**: React 19.x (React Compiler有効)
- **State Management**: Zustand
- **Build Tool**: Vite
- **Runtime**: Modern Browsers (ES2023対応)

## Key Libraries

- **UI**: Tailwind CSS (スタイリング)
- **Testing**: Vitest, React Testing Library, Storybook, MSW (モック), Stryker (mutation testing)
- **Quality**: ESLint, Prettier, Stylelint, TypeDoc

## Development Standards

### Type Safety

- TypeScript strict mode全オプション有効
- `exactOptionalPropertyTypes`, `noUncheckedIndexedAccess` 有効
- `any`型の使用禁止、すべての型を明示的に定義
- `allowJs: false` でJavaScriptファイル混在を禁止

### Code Quality

- **ESLint**: 多層プラグイン構成(security, functional, boundaries, strict-dependencies)
- **Prettier**: Import自動ソート、Tailwind CSS class順序統一
- **Commitlint**: Conventional Commits準拠
- **Secretlint**: 機密情報の誤コミット防止

### Testing

- **Unit/Integration**: Vitest + React Testing Library + @storybook/addon-vitest
- **Component**: Storybook (a11y addon組込)
- **Mutation Testing**: Stryker Mutator
- **API Mocking**: MSW (Mock Service Worker)

## Development Environment

### Required Tools

- Node.js 24+ (package managerはpnpm 10.21.0)
- mise.toml によるツールバージョン管理

### Common Commands

```bash
# Dev: pnpm dev
# Build: pnpm build
# Lint: pnpm lint
# Test: (Vitest/Storybook実行コマンド - package.json参照)
```

## Key Technical Decisions

- **React Compiler採用**: パフォーマンス最適化のため babel-plugin-react-compiler 有効化
- **TypeScript超厳格設定**: 型安全性最大化のため全strictオプション + α
- **品質ゲート多層化**: ESLint(10+プラグイン) + Stylelint + Textlint + Secretlint + Remark
- **依存関係管理**: Catalog Protocol (pnpm workspace) による統一的なバージョン管理
- **アクセシビリティ**: WCAG 2.1 AA準拠、Storybookにa11yアドオン統合
- **Git Hooks**: Lefthook による pre-commit/commit-msg検証自動化

---
_created: 2025-11-15_

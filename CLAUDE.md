# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

OpenCode is an open-source AI-powered coding agent with a TUI (terminal UI), web interface, and desktop app. It's provider-agnostic, supporting Claude, OpenAI, Google, and local models.

## Development Commands

```bash
# Install dependencies (requires Bun 1.3+)
bun install

# Start development TUI (runs in packages/opencode by default)
bun dev
bun dev <directory>    # Run against specific directory
bun dev .              # Run in repo root

# Start headless API server (port 4096)
bun dev serve
bun dev serve --port 8080

# Type checking
bun typecheck          # All packages via Turbo

# Build standalone executable
./packages/opencode/script/build.ts --single

# Regenerate SDK after API changes
./script/generate.ts

# Regenerate JavaScript SDK
./packages/sdk/js/script/build.ts
```

### Running Tests

```bash
# Unit tests (in packages/opencode)
bun run --cwd packages/opencode test
bun run --cwd packages/opencode test <pattern>   # Run specific test

# E2E tests (in packages/app)
bun run --cwd packages/app test:e2e
bun run --cwd packages/app test:e2e:local
bun run --cwd packages/app test:e2e:ui          # With UI
```

Do NOT run `bun test` from root - it is disabled.

### Web and Desktop Development

```bash
# Web app (requires server running first)
bun dev serve                              # Start server
bun run --cwd packages/app dev             # Start web dev server

# Desktop app (requires Tauri/Rust toolchain)
bun run --cwd packages/desktop tauri dev
```

## Architecture

### Monorepo Structure

- **packages/opencode** - Core CLI, server, and business logic
- **packages/app** - Shared web UI components (SolidJS)
- **packages/desktop** - Native desktop app (Tauri wrapper)
- **packages/ui** - UI component library
- **packages/sdk/js** - JavaScript SDK
- **packages/plugin** - Plugin system
- **packages/console/** - Console dashboard (app, core, mail, resource)

### Core Source Layout (packages/opencode/src/)

- `agent/` - Agent implementations (build, plan, general)
- `provider/` - LLM provider integrations (Anthropic, OpenAI, Google, etc.)
- `cli/cmd/tui/` - TUI code (SolidJS with opentui)
- `server/` - API server (Hono)
- `session/` - Session management
- `tool/` - Tool implementations
- `mcp/` - Model Context Protocol
- `lsp/` - Language Server Protocol support
- `config/` - Configuration management
- `permission/` - Permission system

### Key Technologies

- **Runtime**: Bun
- **Build**: Turbo, Vite
- **Frontend**: SolidJS, Tailwind CSS
- **Backend**: Hono
- **Desktop**: Tauri
- **AI SDK**: Vercel AI SDK (@ai-sdk/*)

## Style Guide

- Avoid `try`/`catch` - prefer `.catch()`
- Avoid `let` - use `const` with ternaries or early returns
- Avoid `else` - use early returns
- Avoid `any` type
- Avoid unnecessary destructuring - use `obj.a` instead of `const { a } = obj`
- Prefer single-word variable names
- Use Bun APIs (e.g., `Bun.file()`)
- Rely on type inference; avoid explicit types unless necessary
- Keep functions single-purpose unless composable

## Testing Guidelines

- Avoid mocks - test actual implementations
- Do not duplicate logic into tests
- Tests are in `packages/opencode/test/` and `packages/app/e2e/`

## Agents

- **build** - Default agent with full access
- **plan** - Read-only agent for analysis (denies edits, asks permission for bash)
- **general** - Subagent for complex searches (invoke with `@general`)

## Git Workflow

- Default branch: `dev`
- PR titles follow conventional commits: `feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`
- Optional scope: `feat(app):`, `fix(desktop):`
- All PRs must reference an existing issue

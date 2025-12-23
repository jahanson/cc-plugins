# deno-lsp

Full Deno LSP integration for Claude Code, providing real-time code intelligence and comprehensive Deno development guidance.

## Features

### LSP Integration (via MCP)

Full `deno lsp` integration providing:
- **Diagnostics** - Real-time error and warning detection
- **Hover** - Type information and documentation on hover
- **Go-to-Definition** - Navigate to symbol definitions
- **Code Actions** - Quick fixes and refactoring suggestions
- **Completions** - Intelligent code completion

### Supported File Extensions

`.ts`, `.tsx`, `.js`, `.jsx`, `.mts`, `.cts`, `.mjs`, `.cjs`

### Skills

This plugin includes comprehensive Deno development guidance:

| Skill | Focus |
|-------|-------|
| **deno-typescript** | Quick reference for Deno TypeScript development |
| **deno-core** | Configuration, imports, testing, permissions, anti-patterns |
| **deno-ddd** | Domain-Driven Design architecture patterns |
| **deno-patterns** | Modern TypeScript patterns, resource management, migration |

## Prerequisites

Install Deno globally:

```bash
curl -fsSL https://deno.land/install.sh | sh
```

Or with Homebrew:

```bash
brew install deno
```

Verify installation:

```bash
deno --version
```

## Requirements

- **Deno >= 2.0** (for full LSP support)
- **deno.json** or **deno.jsonc** in project root (plugin only activates in Deno projects)

## Usage

### LSP Features

The LSP integration activates automatically when you work with TypeScript/JavaScript files in a Deno project. Claude will receive diagnostics, type information, and suggestions from the Deno language server.

### Skills

Skills activate automatically based on context:

- Ask about Deno configuration, imports, or testing → **deno-core** activates
- Work on complex business logic or architecture → **deno-ddd** activates
- Ask about modern patterns or Node.js migration → **deno-patterns** activates
- Quick questions about Deno → **deno-typescript** activates

## Configuration

No configuration required. The plugin uses your project's `deno.json` for LSP settings.

### LSP Configuration

The plugin configures the Deno LSP with these defaults (in `.lsp.json`):

```json
{
  "deno": {
    "command": "deno",
    "args": ["lsp"],
    "extensionToLanguage": {
      ".ts": "typescript",
      ".tsx": "typescriptreact",
      ".js": "javascript",
      ".jsx": "javascriptreact",
      ".mts": "typescript",
      ".cts": "typescript",
      ".mjs": "javascript",
      ".cjs": "javascript"
    },
    "initializationOptions": {
      "enable": true,
      "lint": true,
      "unstable": false
    },
    "settings": {
      "deno.enable": true,
      "deno.lint": true,
      "deno.suggest.autoImports": true,
      "deno.suggest.imports.autoDiscover": true
    }
  }
}
```

### Available LSP Settings

| Setting | Description |
|---------|-------------|
| `deno.enable` | Enable/disable Deno LSP |
| `deno.lint` | Enable linting |
| `deno.unstable` | Enable unstable APIs |
| `deno.config` | Path to deno.json |
| `deno.importMap` | Path to import map |
| `deno.suggest.autoImports` | Enable auto-import suggestions |
| `deno.codeLens.test` | Show test code lens |

### Custom Project Settings

Configure project-specific options in your `deno.json`:

```json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true
  }
}
```

## More Information

- [Deno Runtime Documentation](https://docs.deno.com/runtime/)
- [Deno Standard Library](https://jsr.io/@std)
- [JSR Registry](https://jsr.io/)
- [GitHub Repository](https://github.com/denoland/deno/)

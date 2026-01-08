# deno-lsp

Full Deno LSP integration for Claude Code, providing real-time code intelligence
and comprehensive Deno development guidance.

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

| Skill               | Focus                                                       |
| ------------------- | ----------------------------------------------------------- |
| **deno-typescript** | Quick reference for Deno TypeScript development             |
| **deno-core**       | Configuration, imports, testing, permissions, anti-patterns |
| **deno-ddd**        | Domain-Driven Design architecture patterns                  |
| **deno-patterns**   | Modern TypeScript patterns, resource management, migration  |

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
- **deno.json** or **deno.jsonc** in project root (plugin only activates in Deno
  projects)
- **ENABLE_LSP_TOOL=1** environment variable (see Enabling LSP below)

## Enabling LSP

Claude Code requires the `ENABLE_LSP_TOOL` environment variable to be set for
version < 2.1.1:

**Temporary (current session):**

```bash
ENABLE_LSP_TOOL=1 claude
```

**Permanent (add to shell profile):**

```bash
# Add to ~/.bashrc, ~/.zshrc, or equivalent:
export ENABLE_LSP_TOOL=1
```

After enabling, restart Claude Code for the LSP to initialize

## Usage

### LSP Features

The LSP integration activates automatically when you work with
TypeScript/JavaScript files in a Deno project. Claude will receive diagnostics,
type information, and suggestions from the Deno language server.

### Skills

Skills activate automatically based on context:

- Ask about Deno configuration, imports, or testing → **deno-core** activates
- Work on complex business logic or architecture → **deno-ddd** activates
- Ask about modern patterns or Node.js migration → **deno-patterns** activates
- Quick questions about Deno → **deno-typescript** activates

## Configuration

No configuration required. The plugin uses your project's `deno.json` for LSP
settings.

### LSP Configuration

The plugin configures the Deno LSP with these defaults (in `.lsp.json` and
`plugin.json`):

```json
{
  "typescript": {
    "command": "deno",
    "args": [
      [
        "lsp"
      ]
    ],
    "extensionToLanguage": {
      ".ts": "typescript",
      ".tsx": "typescriptreact",
      ".js": "javascript",
      ".jsx": "javascriptreact",
      ".mts": "typescript",
      ".cts": "typescript",
      ".mjs": "javascript",
      ". cjs": "javascript"
    },
    "transport": "stdio",
    "initializationOptions": {
      "enable": true,
      "enablePaths": [
        "src",
        "tests",
        "fixtures"
      ],
      "lint": true,
      "unstable": false,
      "suggest": {
        "autoImports": true,
        "imports": {
          "autoDiscover": true
        }
      }
    },
    "maxRestarts": 3
  }
}
```

**Note:** The server key is `"typescript"` to match the language identifiers in
`extensionToLanguage`. This ensures Deno LSP handles TypeScript files as the
default server.

### Available LSP Settings

| Setting               | Description                    |
| --------------------- | ------------------------------ |
| `enable`              | Enable/disable Deno LSP        |
| `lint`                | Enable linting                 |
| `unstable`            | Enable unstable APIs           |
| `config`              | Path to deno.json              |
| `importMap`           | Path to import map             |
| `suggest.autoImports` | Enable auto-import suggestions |
| `codeLens.test`       | Show test code lens            |

### Custom Project Settings

Add the lint section to your `deno.json` file to configure project-specific LSP settings:
```json
{
  "lint": {
    "rules": {
      "include": [
        "no-external-import"
      ]
    },
    "include": [
      "src/"
    ],
    "exclude": [
      ".tmp/",
    ]
  }
}
```

### LSP not using Deno for TypeScript

If another LSP (like typescript-language-server) handles TypeScript instead of Deno:

- The deno-lsp plugin registers for the `"typescript"` language identifier
- Disable conflicting TypeScript LSP plugins in settings
- Ensure deno-lsp is enabled and loaded first

### Debug Mode

Run Claude Code with debug logging to see LSP initialization:

```bash
claude --debug
```

Look for log lines mentioning "LSP" or "deno" to verify the server starts.

## More Information

- [Deno Runtime Documentation](https://docs.deno.com/runtime/)
- [Deno Standard Library](https://jsr.io/@std)
- [JSR Registry](https://jsr.io/)
- [GitHub Repository](https://github.com/denoland/deno/)

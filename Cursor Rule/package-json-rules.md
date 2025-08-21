---
description: package.json Conventions
alwaysApply: true
globs: ["**/package.json"]
---

# package.json Conventions

## Required Fields

**MUST include**: `name`, `version`, `description`
**MUST use ESM**: `"type": "module"`

```json
// ✅ Good
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "A modern TypeScript project",
  "type": "module"
}

// ❌ Bad
{
  "name": "my-project"
  // Missing version, description, and type
}
```

## Dependencies

**AVOID "^" symbols** for version constraints

```json
// ✅ Good
{
  "dependencies": {
    "react": "18.2.0",
    "typescript": "5.0.0"
  },
  "devDependencies": {
    "eslint": "8.0.0",
    "jest": "29.0.0"
  }
}

// ❌ Bad
{
  "dependencies": {
    "react": "^18.2.0",
    "typescript": "^5.0.0"
  },
  "devDependencies": {
    "eslint": "^8.0.0",
    "jest": "^29.0.0"
  }
}
```

## Scripts

**PREFER cross-platform commands** (Windows and Linux)

```json
// ✅ Good
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "test": "jest",
    "lint": "eslint src --ext .ts,.tsx",
    "clean": "rimraf dist"
  }
}

// ❌ Bad
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "test": "jest",
    "lint": "eslint src --ext .ts,.tsx",
    "clean": "rm -rf dist" // Not cross-platform
  }
}
```

## Avoid These Fields

**AVOID generating**: `author`, `license`, `keywords`

```json
// ✅ Good
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "A modern TypeScript project",
  "type": "module"
}

// ❌ Bad
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "A modern TypeScript project",
  "type": "module",
  "author": "John Doe",
  "license": "MIT",
  "keywords": ["typescript", "react"]
}
```

## General Rules

- **AVOID duplicate entries** in dependencies
- **PREFER exact versions** over ranges
- **Keep it minimal** - only include required fields

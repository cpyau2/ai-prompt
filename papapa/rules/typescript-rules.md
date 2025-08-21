---
description: Typescript Coding Convention
alwaysApply: true
globs: ["**/*.ts", "**/*.tsx", "**/*.js", "**/*.jsx"]
---

# TypeScript Coding Conventions

## Naming Conventions

**Variables/Functions**: `camelCase` (userName, calculateTotal)
**Classes/Interfaces**: `PascalCase` (UserService, UserProfile)  
**Constants**: `UPPER_SNAKE_CASE` (MAX_RETRY_COUNT)
**Files**: `kebab-case` (user-service.ts, user-profile.component.ts)
**Test files**: `.test.ts` or `.spec.ts`

```typescript
// ✅ Good
const userName = "john";
const MAX_RETRY_COUNT = 3;
class UserService {}
interface UserProfile {}

// ❌ Bad
const u = "john";
class userService {}
interface user_profile {}
```

## Type Annotations

**Functions**: Explicit return types, avoid `any`
**Variables**: Type complex objects, infer simple ones
**Interfaces**: Use for object shapes, types for unions/intersections
**Types**: Prefer union types over enums, use "as const" for object access

```typescript
// ✅ Good
function calculateTotal(price: number, tax: number): number {
  return price + price * tax;
}
interface User {
  id: number;
  name: string;
}
type UserStatus = "active" | "inactive";

// ✅ Good: "as const" when object access needed
const UserStatus = {
  Active: "active",
  Inactive: "inactive",
} as const;
type UserStatusType = (typeof UserStatus)[keyof typeof UserStatus];

// ❌ Bad
function calculateTotal(price, tax) {
  return price + price * tax;
}
enum UserStatus {
  Active = "active",
  Inactive = "inactive",
}
```

## Code Organization

**File Length**: Consider refactoring files exceeding 300 lines into smaller modules

### Imports and Exports

- Group imports: external libraries → internal modules → relative imports
- Use `@` alias for src directory imports
- Use `import type` for type imports
- Avoid wildcard imports (`import *`)
- Avoid `..` imports (use absolute paths)
- Use named exports over default exports
- Sort imports alphabetically within groups

```typescript
// ✅ Good
import { useState, useEffect } from "react";
import type { User, UserStatus } from "@/types";
import { UserService } from "@/services";
import { formatName } from "./utils";

// ❌ Bad
import * as React from "react";
import { User } from "../../types";
import { UserService } from "@/services";
import { formatName } from "./utils";
```

### Function and Class Structure

- Keep functions small and focused on a single responsibility
- Use early returns to reduce nesting
- Limit function parameters to 3-4 maximum

```typescript
// ✅ Good
function validateUser(user: User): ValidationResult {
  if (!user.email) {
    return { isValid: false, error: "Email is required" };
  }

  if (!user.name) {
    return { isValid: false, error: "Name is required" };
  }

  return { isValid: true };
}

// ❌ Bad
function validateUser(user: User): ValidationResult {
  if (user.email) {
    if (user.name) {
      return { isValid: true };
    } else {
      return { isValid: false, error: "Name is required" };
    }
  } else {
    return { isValid: false, error: "Email is required" };
  }
}
```

## Error Handling

### Try-Catch Blocks

- Always handle errors appropriately
- Use specific error types when possible
- Log errors for debugging purposes

```typescript
// ✅ Good
async function fetchUserData(userId: string): Promise<User> {
  try {
    const response = await api.get(`/users/${userId}`);
    return response.data;
  } catch (error) {
    if (error instanceof NetworkError) {
      throw new UserFetchError("Network error occurred");
    }
    throw new UserFetchError("Failed to fetch user data");
  }
}

// ❌ Bad
async function fetchUserData(userId: string): Promise<User> {
  const response = await api.get(`/users/${userId}`);
  return response.data;
}
```

## Error Handling #2

**Always include traceable context** (method, URL, params) for error messages to aid debugging.

```typescript
// ✅ Good
try {
  const result = await api.getUser(userId);
  return result;
} catch (error) {
  throw new Error(
    `Failed to fetch user (ID: ${userId}, Method: GET, URL: /api/users/${userId}): ${error.message}`
  );
}

// ❌ Bad
try {
  const result = await api.getUser(userId);
  return result;
} catch (error) {
  throw new Error(`Failed to fetch user: ${error.message}`);
}
```

## Performance and Best Practices

### Async/Await

- Prefer async/await over Promise chains
- Always await promises in try-catch blocks
- Use Promise.all for parallel operations

```typescript
// ✅ Good
async function loadUserData(userIds: string[]): Promise<User[]> {
  try {
    const promises = userIds.map((id) => fetchUserData(id));
    return await Promise.all(promises);
  } catch (error) {
    console.error("Failed to load user data:", error);
    throw error;
  }
}

// ❌ Bad
function loadUserData(userIds: string[]): Promise<User[]> {
  return Promise.all(userIds.map((id) => fetchUserData(id)));
}
```

### Null and Undefined Handling

- Use optional chaining (`?.`) and nullish coalescing (`??`)
- Provide default values for optional parameters
- Use strict equality (`===`, `!==`)

```typescript
// ✅ Good
const userName = user?.profile?.name ?? "Anonymous";
const count = items?.length ?? 0;

if (status === "active") {
  // handle active status
}

// ❌ Bad
const userName = (user && user.profile && user.profile.name) || "Anonymous";
const count = (items && items.length) || 0;

if (status == "active") {
  // handle active status
}
```

## Testing Conventions

### Test Structure

- Use descriptive test names that explain the scenario
- Follow the AAA pattern (Arrange, Act, Assert)
- Mock external dependencies

```typescript
// ✅ Good
describe("UserService", () => {
  describe("createUser", () => {
    it("should create a new user with valid data", async () => {
      // Arrange
      const userData = { name: "John", email: "john@example.com" };
      const mockApi = jest.fn().mockResolvedValue({ id: 1, ...userData });

      // Act
      const result = await createUser(userData, mockApi);

      // Assert
      expect(result).toEqual({ id: 1, ...userData });
      expect(mockApi).toHaveBeenCalledWith("/users", userData);
    });
  });
});
```

## Common Patterns

### Singleton Pattern

```typescript
class DatabaseConnection {
  private static instance: DatabaseConnection;
  private constructor() {}

  static getInstance(): DatabaseConnection {
    if (!DatabaseConnection.instance) {
      DatabaseConnection.instance = new DatabaseConnection();
    }
    return DatabaseConnection.instance;
  }
}
```

### Factory Pattern

```typescript
interface User {
  id: number;
  name: string;
  type: "admin" | "regular";
}

class UserFactory {
  static createAdmin(id: number, name: string): User {
    return { id, name, type: "admin" };
  }

  static createRegular(id: number, name: string): User {
    return { id, name, type: "regular" };
  }
}
```

### Builder Pattern

```typescript
class UserBuilder {
  private user: Partial<User> = {};

  withId(id: number): UserBuilder {
    this.user.id = id;
    return this;
  }

  withName(name: string): UserBuilder {
    this.user.name = name;
    return this;
  }

  build(): User {
    if (!this.user.id || !this.user.name) {
      throw new Error("User must have id and name");
    }
    return this.user as User;
  }
}

// Usage
const user = new UserBuilder().withId(1).withName("John").build();
```

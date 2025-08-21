---
description: React Component Structure Rules
alwaysApply: true
globs: ["**/*.tsx", "**/*.jsx", "**/*.ts", "**/*.js"]
---

# React Component Structure Rules

## Component Organization

**File Structure**: Use CamelCase folders for complex components with multiple files
**Internal Files**: Use kebab-case for internal files (index.tsx, types.ts, schemas.ts)
**Main Component**: Export default function with PascalCase name

```typescript
// ✅ Good - Complex component structure
components / UserForm / index.tsx; // Main component + re-exports
types.ts; // Props, interfaces, constants
schemas.ts; // Zod schemas
utils.ts; // Helper functions
hooks.ts; // Custom hooks (if applicable)
api.ts; // API calls (if applicable)
styles.css; // Component-specific styles
```

## Component Internal Structure

**Order of declarations** within the component file:

```typescript
// 1. Imports (external → internal → relative)
import { useState, useEffect } from "react";
import { useTranslation } from "react-i18next";
import { useForm } from "react-hook-form";
import { useQuery, useMutation } from "@tanstack/react-query";
import type { User, FormData } from "./types";
import { UserSchema } from "./schemas";
import { getDefaultFormValues } from "./utils";

// 2. Constants (if any)
const DEFAULT_TIMEOUT = 5000;

// 3. Helper functions (pure/stateless)
// Pure functions: same input → same output, no side effects, no external dependencies
// Stateless functions: no useState, no persistent variables, no component state
function getDefaultFormValues(): FormData {
  return {
    name: "",
    email: "",
    role: "user",
  };
}

// 4. Component
export default function UserForm({ userId, onSubmit }: UserFormProps) {
  // 5. State variables
  const [isSubmitting, setIsSubmitting] = useState(false);
  const [error, setError] = useState<string | null>(null);

  // 6. Hooks (grouped by purpose)
  const { t } = useTranslation();
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<FormData>({
    defaultValues: getDefaultFormValues(),
  });

  // React Query hooks (custom hook implementations are in another file)
  const { data: user, isLoading } = useQuery({
    queryKey: ["user", userId],
    queryFn: () => fetchUser(userId),
  });

  const mutation = useMutation({
    mutationFn: updateUser,
    onSuccess: () => {
      onSubmit?.();
    },
  });

  // 7. Event handlers (use regular functions, not arrow functions)
  function handleFormSubmit(data: FormData) {
    setIsSubmitting(true);
    setError(null);

    try {
      mutation.mutate({ id: userId, ...data });
    } catch (err) {
      setError(err instanceof Error ? err.message : "Unknown error");
    } finally {
      setIsSubmitting(false);
    }
  }

  function handleCancel() {
    // Cancel logic
  }

  // 8. Side effects
  useEffect(() => {
    if (user) {
      // Update form with user data
    }
  }, [user]);

  // 9. Early returns for loading/error states
  if (isLoading) {
    return <LoadingSpinner />;
  }

  if (error) {
    return <ErrorMessage message={error} />;
  }

  // 10. JSX fragments (break into smaller chunks)
  const formHeader = (
    <div className="form-header">
      <h2>{t("user.edit.title")}</h2>
      <p>{t("user.edit.description")}</p>
    </div>
  );

  const formFields = (
    <div className="form-fields">
      <input {...register("name")} placeholder={t("user.name")} />
      <input {...register("email")} placeholder={t("user.email")} />
      <select {...register("role")}>
        <option value="user">{t("user.role.user")}</option>
        <option value="admin">{t("user.role.admin")}</option>
      </select>
    </div>
  );

  const formActions = (
    <div className="form-actions">
      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? t("common.saving") : t("common.save")}
      </button>
      <button type="button" onClick={handleCancel}>
        {t("common.cancel")}
      </button>
    </div>
  );

  // 11. Main return (keep it small)
  return (
    <form onSubmit={handleSubmit(handleFormSubmit)} className="user-form">
      {formHeader}
      {formFields}
      {formActions}
    </form>
  );
}
```

## Hook Organization

**Group hooks by purpose** in this order:

1. **i18n hooks** (useTranslation)
2. **Form hooks** (react-hook-form)
3. **Query hooks** (react-query queries - custom hook implementations are in another file)
4. **Mutation hooks** (react-query mutations - custom hook implementations are in another file)
5. **Custom hooks** (miscellaneous)

```typescript
// ✅ Good - Grouped hooks
const { t } = useTranslation();
const { register, handleSubmit } = useForm();

const { data: user, isLoading } = useQuery({...});
const { data: settings } = useQuery({...});

const createUserMutation = useMutation({...});
const updateUserMutation = useMutation({...});

const { theme } = useTheme();
const { user } = useAuth();
```

## Schema Management

**Move schemas to separate files** when they have dependencies or are complex
**Keep simple schemas inline** if they have no dependencies

```typescript
// ✅ Good - schemas.ts
import { z } from "zod";

export const UserSchema = z.object({
  id: z.number(),
  name: z.string().min(1),
  email: z.string().email(),
  role: z.enum(["user", "admin"]),
});

// ✅ Good - Inline for simple schemas
const SimpleSchema = z.object({
  name: z.string(),
  email: z.string().email(),
});
```

## JSX Fragment Strategy

**Break large JSX into smaller chunks** using const variables
**Keep main return statement small** (no screen scrolling needed)
**Use descriptive names** for JSX fragments

```typescript
// ✅ Good - JSX fragments
const userInfo = (
  <div className="user-info">
    <h3>{user.name}</h3>
    <p>{user.email}</p>
  </div>
);

const userActions = (
  <div className="user-actions">
    <button onClick={handleEdit}>Edit</button>
    <button onClick={handleDelete}>Delete</button>
  </div>
);

return (
  <div className="user-card">
    {userInfo}
    {userActions}
  </div>
);
```

## Event Handler Conventions

**Use regular functions** (not arrow functions) for event handlers
**Follow naming pattern**: `handle` + Action + Context
**Include proper TypeScript typing**

```typescript
// ✅ Good
function handleFormSubmit(data: FormData) {
  // Submit logic
}

function handleUserDelete(userId: string) {
  // Delete logic
}

function handleEmailChange(event: React.ChangeEvent<HTMLInputElement>) {
  // Change logic
}

// ❌ Bad - Arrow functions
const handleSubmit = (data: FormData) => {
  // Submit logic
};
```

## Early Returns

**Handle loading/error states early** to reduce nesting
**Use conditional rendering** for different states

```typescript
// ✅ Good - Early returns
if (isLoading) {
  return <LoadingSpinner />;
}

if (error) {
  return <ErrorMessage message={error} />;
}

if (!user) {
  return <NotFound />;
}

// Main component logic
return <UserProfile user={user} />;

// ❌ Bad - Nested conditionals
return (
  <div>
    {isLoading ? (
      <LoadingSpinner />
    ) : error ? (
      <ErrorMessage message={error} />
    ) : !user ? (
      <NotFound />
    ) : (
      <UserProfile user={user} />
    )}
  </div>
);
```

## Import Organization

**Group imports in this order**:

1. **React and external libraries**
2. **Internal modules** (using @ alias)
3. **Relative imports**

```typescript
// ✅ Good - Organized imports
import { useState, useEffect } from "react";
import { useTranslation } from "react-i18next";
import { useForm } from "react-hook-form";

import type { User, FormData } from "@/types";
import { UserService } from "@/services";

import type { UserFormProps } from "./types";
import { UserSchema } from "./schemas";
import { getDefaultFormValues } from "./utils";
```

## Type Safety

**Use proper TypeScript typing** for all props and state
**Use `import type`** for type-only imports
**Define interfaces for complex props**

```typescript
// ✅ Good - types.ts
export interface UserFormProps {
  userId: string;
  onSubmit?: () => void;
  onCancel?: () => void;
}

export interface FormData {
  name: string;
  email: string;
  role: "user" | "admin";
}
```

description:
globs:
alwaysApply: false

---

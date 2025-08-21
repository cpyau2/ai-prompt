---
description: JavaScript/TypeScript Library Conventions
alwaysApply: true
globs: ["**/*.js", "**/*.ts", "**/*.jsx", "**/*.tsx"]
---

# JavaScript/TypeScript Library Conventions

## Ant Design (v5)

**Baseline**: Version 5
**Avoid deprecated syntax**

### Component Usage

**Button Groups**: Use `Space.Compact` instead of `Button.Group`
**Modals**: Use `destroyOnHidden` instead of `destroyOnClose`

```typescript
// ✅ Good
import { Space, Button, Modal } from 'antd';

<Space.Compact>
  <Button>Cancel</Button>
  <Button type="primary">Submit</Button>
</Space.Compact>

<Modal
  title="Title"
  destroyOnHidden={true}
  open={isOpen}
  onCancel={handleCancel}
>
  Content
</Modal>

// ❌ Bad
<Button.Group>
  <Button>Cancel</Button>
  <Button type="primary">Submit</Button>
</Button.Group>

<Modal
  title="Title"
  destroyOnClose={true}
  open={isOpen}
  onCancel={handleCancel}
>
  Content
</Modal>
```

## Zod (v4)

**Baseline**: Version 4
**Avoid deprecated syntax**

```typescript
// ✅ Good
import { z } from "zod";

const UserSchema = z.object({
  id: z.number(),
  name: z.string(),
  email: z.string().email(),
});

// ❌ Bad - deprecated syntax
const UserSchema = z
  .object({
    id: z.number(),
    name: z.string(),
    email: z.string().email(),
  })
  .strict(); // .strict() is deprecated in v4
```

## MinIO JS (v8)

**Baseline**: Version 8
**Avoid deprecated syntax**

```typescript
// ✅ Good
import { Client } from "minio";

const minioClient = new Client({
  endPoint: "play.min.io",
  port: 9000,
  useSSL: true,
  accessKey: "your-access-key",
  secretKey: "your-secret-key",
});

// ❌ Bad - deprecated syntax
const minioClient = new Client({
  endPoint: "play.min.io",
  port: 9000,
  secure: true, // 'secure' is deprecated, use 'useSSL'
  accessKey: "your-access-key",
  secretKey: "your-secret-key",
});
```

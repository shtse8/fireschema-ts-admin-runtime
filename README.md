# 🔥 @shtse8/fireschema-ts-admin-runtime

[![npm version](https://badge.fury.io/js/%40shtse8%2Ffireschema-ts-admin-runtime.svg)](https://badge.fury.io/js/%40shtse8%2Ffireschema-ts-admin-runtime)

**Bring Robust Type Safety to Your Node.js Firestore Backend!**

This package provides the runtime core for TypeScript (Admin SDK) code generated by [FireSchema](https://github.com/shtse8/FireSchema), the essential tool for defining and enforcing your Firestore schema in code.

## Stop Fighting Runtime Errors in Your Backend

Using the `firebase-admin` SDK directly can lead to:

-   Unsafe data access and manipulation.
-   Runtime errors from simple typos in field names during updates or queries.
-   Inconsistent data structures across different parts of your backend.
-   Difficulty ensuring required fields are present.

These issues slow down development and make your backend less reliable.

## FireSchema + This Runtime = Secure & Efficient Backend Development 🚀

**FireSchema** generates type-safe models, collection references, query builders, and update builders specifically for the Admin SDK, based on your JSON Schema.

This **`@shtse8/fireschema-ts-admin-runtime`** package contains the necessary base classes and utilities that power the generated code. It works seamlessly with the official `firebase-admin` SDK.

**Why Use It?**

-   **🔒 Maximum Type Safety:** Eliminate a whole class of runtime errors in your backend logic.
-   **⚙️ Increased Productivity:** Less boilerplate, more focus on business logic. Enjoy autocompletion and compile-time checks.
-   **✅ Enhanced Reliability:** Enforce your data schema consistently across your backend services.
-   **☁️ Perfect For:** Node.js backends, Cloud Functions for Firebase, server-side applications needing privileged Firestore access.

## Installation

This package is designed to work with code generated by the main `fireschema` tool. Install both this runtime and the `firebase-admin` SDK in your Node.js project:

```bash
npm install @shtse8/fireschema-ts-admin-runtime firebase-admin
# or
yarn add @shtse8/fireschema-ts-admin-runtime firebase-admin
# or
pnpm add @shtse8/fireschema-ts-admin-runtime firebase-admin
```

## Usage

You'll primarily interact with the classes generated by the `fireschema` CLI, which utilize this runtime package behind the scenes.

**Example (using generated code):**

```typescript
import * as admin from 'firebase-admin';
import { firestore } from './_setup'; // Your initialized Admin Firestore instance
import { UsersCollection } from './generated/firestore-admin/users.collection'; // Generated by FireSchema
import { UserAddData } from './generated/firestore-admin/users.types'; // Generated by FireSchema
const { FieldValue } = admin.firestore; // From Admin SDK

const usersCollection = new UsersCollection(firestore); // Generated class uses this runtime

async function runAdmin() {
  const newUser: UserAddData = { displayName: 'Admin User', email: 'admin@example.com', roles: ['editor'] };
  const ref = await usersCollection.add(newUser); // Type-safe add!

  const user = await usersCollection.get(ref.id); // Type-safe get!
  console.log(user?.displayName);

  // Type-safe query!
  const editors = await usersCollection.query().whereRoles("array-contains", "editor").getData();
  console.log(`Found ${editors.length} editors.`);

  await usersCollection.update(ref.id)
    .setLastLogin(FieldValue.serverTimestamp()) // Type-safe update!
    .commit();
}
```

## Discover the Full Power of FireSchema!

This runtime enables type safety for the Admin SDK. To learn how to define schemas and generate code for all supported platforms, check out the main FireSchema documentation:

**➡️ [Full FireSchema Documentation & Guides](https://shtse8.github.io/FireSchema/)**

---

*This package provides the runtime support for the `typescript-admin` target in FireSchema.*
# Migration `20200530102700-fix-field-name`

This migration has been generated by Trevor Plant at 5/30/2020, 10:27:00 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
PRAGMA foreign_keys=OFF;

CREATE TABLE "quaint"."new_Contact" (
"createdAt" DATE NOT NULL DEFAULT CURRENT_TIMESTAMP ,"email" TEXT NOT NULL  ,"id" INTEGER NOT NULL  PRIMARY KEY AUTOINCREMENT,"message" TEXT NOT NULL  ,"name" TEXT NOT NULL  )

INSERT INTO "quaint"."new_Contact" ("createdAt", "email", "id", "name") SELECT "createdAt", "email", "id", "name" FROM "quaint"."Contact"

PRAGMA foreign_keys=off;
DROP TABLE "quaint"."Contact";;
PRAGMA foreign_keys=on

ALTER TABLE "quaint"."new_Contact" RENAME TO "Contact";

PRAGMA "quaint".foreign_key_check;

PRAGMA foreign_keys=ON;
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200530094537-create-contact..20200530102700-fix-field-name
--- datamodel.dml
+++ datamodel.dml
@@ -1,7 +1,7 @@
 datasource DS {
   provider = "sqlite"
-  url = "***"
+  url      = env("DATABASE_URL")
 }
 generator client {
   provider      = "prisma-client-js"
@@ -18,7 +18,7 @@
 model Contact {
     id          Int @id @default(autoincrement())
     name        String
     email       String
-    messege     String
+    message     String
     createdAt   DateTime @default(now())
 }
```



# Migration `20200417141516-removed-resource-to-project-relation`

This migration has been generated by Alex Karavil at 4/17/2020, 2:15:16 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
ALTER TABLE "public"."Resource" ADD COLUMN "projectId" integer   ;

ALTER TABLE "public"."Resource" ADD FOREIGN KEY ("projectId")REFERENCES "public"."Project"("id") ON DELETE SET NULL  ON UPDATE CASCADE

DROP TABLE "public"."_ProjectToResource";
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200417130937-small-changes..20200417141516-removed-resource-to-project-relation
--- datamodel.dml
+++ datamodel.dml
@@ -1,7 +1,7 @@
 datasource db {
   provider = "postgresql"
-  url = "***"
+  url      = env("DATABASE_URL")
 }
 generator client {
   provider = "prisma-client-js"
@@ -11,9 +11,9 @@
   id          Int        @default(autoincrement()) @id
   name        String
   description String?
   tasks       Task[]
-  resources   Resource[] @relation(references: [id])
+  resources   Resource[]
   completed   Boolean    @default(false)
 }
 model Task {
@@ -25,9 +25,8 @@
   completed   Boolean @default(false)
 }
 model Resource {
-  id          Int       @default(autoincrement()) @id
+  id          Int     @default(autoincrement()) @id
   name        String
   description String?
-  projects    Project[] @relation(references: [id])
 }
```



---
title: Prisma Setup and Seeding
---

By following these steps, you’ll have Prisma set up with SQLite, including the ability to seed your database with initial data. You can now create and populate your database as needed.


### Step 1: Install Prisma CLI

```npm install prisma --save-dev```

Installs Prisma CLI as a development dependency in your project.

### Step 2: Initialize Prisma with SQLite as the Data Source

```npx prisma init --datasource-provider sqlite```

Creates a prisma folder containing:

schema.prisma: The main Prisma schema file.

.env: Environment variables file to configure the database connection.

Sets SQLite as the default database provider.

### Step 3: Create Database Tables

```npx prisma db push```

Pushes the Prisma schema to the database and generates tables based on the schema.

### Step 4: Generate Initial Migration

```npx prisma migrate dev --name init```

Creates an initial migration file named init to track schema changes.

Applies the migration to the database.

### Step 5: Open Prisma Studio

```npx prisma studio```

Launches a web-based GUI for viewing and editing database records.

### Step 6: Install Dependencies for Seeding

```npm install -D typescript ts-node @types/node```

TypeScript: Enables TypeScript in the project.

ts-node: Runs TypeScript files directly without compilation.

@types/node: Provides TypeScript definitions for Node.js.

### Step 7: Configure package.json

Add the following to your package.json:
```
"devDependencies": {
  "ts-node": "^10.9.2"
},
"prisma": {
  "seed": "ts-node prisma/seed.ts"
}
```
prisma.seed: Defines the command to execute the seed script.

This points to the seed.ts file inside the prisma folder.

### Step 8: Configure tsconfig.json

Ensure the following configurations exist in your tsconfig.json:
```
"module": "commonjs",
"moduleResolution": "node",
```
module: Specifies CommonJS module syntax for compatibility with Node.js.

moduleResolution: Ensures TypeScript resolves modules using Node.js behavior.



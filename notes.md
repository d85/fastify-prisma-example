# Fastify with Prisma

Grab the postgress database from `https://github.com/tomanagle/awesome-docker-compose`

```sh
yarn init
```

```sh
tsc --init
```

```sh
# dependencies
yarn add @prisma/client@^3.10.0 fastify@^3.27.2 fastify-zod@^0.0.2 zod zod-to-json-schema fastify-jwt fastify-swagger@^4.15.0
```

```sh
# devdependencies 
yarn add ts-node-dev typescript @types/node --dev
```

```sh
# initialise prisma
npx prisma init --datasource-provider postgresql
```

```sh
# migrate the schema
npx prisma migrate dev --name init
```

Regarding Fastify, docker expects your host to be `0.0.0.0`.

## Setup Prisma

After pointing the createUser route `(POST /api/users)` handler to the user controller, we need to setup prisma for interaction with the database.

Run

```sh
npx prisma init --datasource-provider postgresql
```

to initialise prisma. 

This will create a `.env` file with a placeholder database url

```sh
DATABASE_URL="postgresql://johndoe:randompassword@localhost:5432/mydb?schema=public"
```

It will also create `prisma/schema.prisma`

```prisma
// This is your Prisma schema file,
// learn more about it in the docs: https://pris.ly/d/prisma-schema

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```

This is where we will define our `user` and `product` models

```prisma
...
model User {
  id Int @id @default(autoincrement())
  email String @unique
  name String?
  password String
  salt String
  products Product[]
}

model Product {
  id Int @id @default(autoincrement())
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  title String @db.VarChar(255)
  content String?
  price Float
  owner User @relation(fields: [ownerId], references: [id])
  ownerId Int
}
```
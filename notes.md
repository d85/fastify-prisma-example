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
yarn add @prisma/client fastify fastify-zod zod zod-to-json-schema fastify-jwt fastify-swagger
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

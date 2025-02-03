# Connect to Prisma Postgres from Cloudflare Workers

You can build applications on Cloudflare Workers that connect to Prisma Postgres with a few configuration steps!
This project is a full sample based on Prisma's [sample project](https://github.com/prisma/prisma-examples/tree/latest/databases/prisma-postgres).

## Get this project running

1. Run `npm install` to install project dependencies.
1. Rename `.dev.vars.example` to `.dev.vars` and set your `DATABASE_URL` to the one provided in your Prisma Postgres instructions (this is required for local development using [Cloudflare Workers Secrets](https://developers.cloudflare.com/workers/configuration/secrets/)).
2. Run `npx prisma migrate dev` to create the tables in your Postgres database based on your schema.
3. Run `npx prisma generate --no-engine` to create a Prisma Client with the Accelerate extension.
4. Run `npm run dev` to run the project, and navigate to `http://localhost:8787` to see the results.
5. Run `npx wrangler secret put DATABASE_URL` to set up your DATABASE_URL secret in Cloudflare.
6. Run `npm run deploy` to deploy the project. 

## Add Prisma Postgres to your own Cloudflare Worker project

1. Run `npm install prisma @prisma/client@latest @prisma/extension-accelerate` to install the Prisma edge client and the Prisma Accelerate extension. 
2. Run `npx prisma init` to create your `prisma/schema.prisma` schema files, which define the schema of your database.
3. Run `npx prisma migrate dev` to create the tables in your Prisma Postgres database.
4. Run `npx prisma generate --no-engine` to create a Prisma Client with the Accelerate extension.
5. Configure your database URL with Cloudflare Workers and Prisma. You need to override the datasourceUrl in the PrismaClient instantiation with the database url provided by Cloudflare environment variables. https://www.prisma.io/docs/orm/reference/prisma-client-reference#programmatically-override-a-datasource-url.
4. Run `npm run dev` to run the project, and navigate to `http://localhost:8787` to see the results.
5. Run `npx wrangler secret put DATABASE_URL` to set up your DATABASE_URL secret in Cloudflare.
6. Run `npm run deploy` to deploy the project.

## Troubleshooting

* To connect to Prisma Postgres when developing locally using `wrangler dev`, you must disable [WARP](https://developers.cloudflare.com/cloudflare-one/connections/connect-devices/warp/).

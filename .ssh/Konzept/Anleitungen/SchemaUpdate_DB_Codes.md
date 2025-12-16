# Version 2

  1. sudo docker compose exec web npx prisma migrate deploy --schema src/pages/schema.prisma
  2. sudo docker compose exec web npm run db:seed


# Version 1
- Purpose: regenerate the Prisma client after schema changes and apply migrations so the DB structure
    matches the code.

- Reuse this command chain whenever you add or modify Prisma schema models/migrations:

# 1. Befehl

sudo docker compose exec web npx prisma generate --schema src/pages/schema.prisma

     – immediately after editing schema.prisma or adding a model/migration, to refresh the Prisma client used by the Next.js app.

# 2. Befehl

sudo docker compose exec web npx prisma migrate deploy --schema src/pages/schema.prisma

    – after generating a new migration (or pulling one from git) to apply it to the running database; also re-run before seeding if your DB might be out of date.

  Use both steps together whenever the backend schema changes to keep the generated client and database
  schema aligned.
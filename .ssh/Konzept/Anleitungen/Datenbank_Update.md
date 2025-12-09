# DB Update Guide

  - Start services – ensure the app and database containers are running before touching
    Prisma:
    sudo docker compose up -d db web
  - Apply migrations – run Prisma inside the web container (it already has the right schema
    path):
    sudo docker compose exec web npx prisma migrate deploy --schema prisma/schema.prisma
  - Regenerate client – keep the Prisma Client in sync:
    sudo docker compose exec web npx prisma generate
  - Seed data (optional) – if your change needs refreshed demo data:
    sudo docker compose exec web npm run db:seed
  - Troubleshooting tips
      - If docker compose exec web … errors with “service is not running”, rerun the first
        step.
      - If the port 3001 is already in use when starting web, stop the process that occupies
        it or adjust the port mapping, then start the container again.
      - When running Prisma outside Docker, override the connection string:
        DATABASE_URL="postgresql://dais:dais@localhost:5432/dais" npx prisma migrate deploy
        --schema src/pages/schema.prisma

  Following those steps keeps the database schema in sync whenever you add or modify Prisma
  models.

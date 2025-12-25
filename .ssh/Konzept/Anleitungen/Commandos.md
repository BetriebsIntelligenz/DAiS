# Docker Container stoppen mit Volumes
    sudo docker compose down --volumes

# Docker Container mit neuen Build starten
    sudo docker compose up --build -d

# Database Migration nach Löschung
    sudo docker compose exec web npx prisma migrate deploy --schema src/pages/schema.prisma
    sudo docker compose exec web npx prisma migrate deploy --schema src/pages/schema.prisma
    sudo docker compose exec web sh -c "npx prisma migrate deploy --schema src/pages/schema.prisma && npm run db:seed"

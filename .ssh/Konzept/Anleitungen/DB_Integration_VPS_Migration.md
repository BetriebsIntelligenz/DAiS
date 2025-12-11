1. Ins Verzeichnis wechseln
cd DAISV2/DAiS

2. Aktuelle Docker löschen
docker compose down --volumes

3. Wieder Starten
docker compose up -d db web

4. DB initialisieren
docker compose exec web npx prisma migrate deploy --schema src/pages/schema.prisma

5. Schema starten
docker compose exec web npx prisma migrate deploy --schema src/pages/schema.prisma

(Optional: 6. Seed einspielen)
 docker compose exec web sh -c "npx prisma migrate \
    deploy --schema src/pages/schema.prisma && npm run
  db:seed"
> Für einen vollständigen Reset gehst du folgendermaßen vor:

# 1.
cd DAISV2/DAiS
– einmalig, bevor du irgendetwas mit Docker machst.

# 2.
sudo docker compose down --volumes
– stoppt alle Container und entfernt DB‑Volumes, damit wirklich alles sauber ist.

# 3.
sudo docker compose up -d db web
– startet Datenbank + Web neu (Web braucht die DB bereits laufend).

# 4.
sudo docker compose exec web npx prisma migrate deploy --schema src/pages/schema.prisma
– wendet alle Migrationen im Container an (einmal reicht; Schritt 5 ist dam redundant).

# 5. (Optional)
sudo docker compose exec web npm run db:seed
– füllt die neue DB mit Seed‑Daten. Falls du gern alles in einem Rutsch machst, kannst du stattdessen d bibefehl aus Schritt 6 verwenden.

# 6.
(Nur wenn du neue Prisma‑Typen brauchst)
sudo docker compose exec web npx prisma generate --schema src/pages/schema.prisma
– generiert Client‑Artefakte. Danach läuft die App gegen eine frische, migrierte DB; zusätzliche migrate deploy Aufrufe brauchst du nicht mehr.
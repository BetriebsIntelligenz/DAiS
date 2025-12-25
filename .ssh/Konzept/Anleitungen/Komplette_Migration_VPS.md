# Auf Computer
Aktuelle GIT Version deployen (Beide_GIT_Updates.md)

# Auf VPS
1. Neuen Ordner erstellen
    ```
    mkdir dais
    cd dais
    ```
2. Repo klonen. Dabei darauf achten, dass der aktuelle Branch im VPS mit dem Branch im Computer identisch ist.
    ```
    git clone https://github.com/BetriebsIntelligenz/DAiS.git
    ```
3. Docker Compose starten
    ```
    docker compose up --build -d
    ```
4. Prisma-Migration laufen lassen (DB_Integration_VPS_Migration.md)
    ```
    docker compose exec web npx prisma migrate deploy
    ``` 
5. Seed laufen lassen (optional)
    ```
    docker compose exec web npx prisma db seed
    ``` 

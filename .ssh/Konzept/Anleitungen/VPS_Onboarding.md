DAiS Deploy Guide (VPS via SSH)
  _ Voraussetzungen: Git + Docker + Docker Compose installiert, SSH-
  Zugang zum VPS, Repo github.com/BetriebsIntelligenz/DAiS erreichbar._

  1. VPS vorbereiten
      - Per SSH einloggen.
      - Pakete aktualisieren: sudo apt update && sudo apt upgrade -y
      - Docker + Compose installieren (falls nicht vorhanden):

        curl -fsSL https://get.docker.com | sudo sh
        sudo usermod -aG docker $USER
        sudo apt install docker-compose-plugin -y
        (Abmelden/neu anmelden, damit die Docker-Gruppe greift.)
  2. Repo klonen

     git clone https://github.com/BetriebsIntelligenz/DAiS.git
     cd DAiS

     (Alternativ via SSH-URL, falls du einen Deploy-Key nutzt.)
  3. Env-Dateien setzen
      - Produktionswerte in .env und .env.docker eintragen (DB-Creds,
        Secrets etc.).
      - Beispiel: cp .env.example .env &&
        cp .env.docker .env.production und Werte anpassen.
  4. Docker Build & Start

     docker compose down -v            # falls Restbestände existieren
     docker compose up --build -d
      - Der Dockerfile baut Next.js (inkl. Prisma generate).
      - Das Compose-File startet Web + Postgres (Port-Mapping anpassen,
        z. B. 3000:3000).
  5. Migration & Seed im Container

     docker compose exec web npx prisma migrate deploy
     docker compose exec web npx prisma db seed   # optional, lädt
  Programme/Rewards/Journals

     (Bei Erfolg: „No pending migrations“ bzw. „Seed data created“.)
  6. Firewall & Domain
      - VPS-Firewall öffnen (ufw allow 3000/tcp o. ä.).
      - Falls Domain/Reverse-Proxy (Nginx) genutzt wird, Proxy auf den
        Web-Container-Port zeigen lassen.
  7. Health Check
      - Browser/curl auf http://<VPS-IP>:<mapped-port>/ → Login-Screen
        und App testen.
      - Logs prüfen: docker compose logs -f web.
  8. Updates/Deployments
      - Pull neuester Code: git pull origin main.
      - Rebuild und restart: docker compose down && docker compose up
        --build -d.
      - Prisma-Migration bei Bedarf erneut laufen lassen.
  9. Backup/DB
      - Postgres-Dump regelmäßig via docker compose exec db pg_dump -U
        dais dais > backup.sql.
      - .env und pgdata sichern (Volume-Backup oder docker cp).
  10. Monitoring
      - docker compose ps, docker compose logs.
      - Optional: Systemd-Unit oder Watchtower für automatisches
        Restart/Updates.

  Damit hast du einen reproduzierbaren Deployment-Flow auf jedem VPS
  mit Docker. Sag Bescheid, wenn du z. B. Systemd-Units oder einen
  Reverse-Proxy-Config-Snippet brauchst.

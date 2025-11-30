# 1. PC: Aktuelle Version in GIT deployen
    git add .
    git commit -m "feat: add requirements kanban with xp tracking"
    git push -u origin main

# 2. VPS: Neue GIT Downloaden und Docker bauen
    git clone https://github.com/BetriebsIntelligenz/DAiS.git
    cd DAiS
    docker compose up --build -d
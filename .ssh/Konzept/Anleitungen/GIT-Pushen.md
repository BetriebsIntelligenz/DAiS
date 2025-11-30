Hier der Ablauf, um deinen aktuellen Stand ins Remote https://github.com/BetriebsIntelligenz/DAiS.git zu bekommen:

  1. Remote setzen (falls noch nicht vorhanden):

  - git remote add origin https://github.com/BetriebsIntelligenz/DAiS.git
    (Falls schon gesetzt, überspringen oder mit git remote -v prüfen.)

  2. Aktuellen Status checken:

  - git status

  3. Änderungen committen (z.B. auf Branch main oder eigenem Feature-Branch):

  - git checkout -b feature/anforderungen (wenn du einen neuen Branch willst)
  - git add .
  - git commit -m "feat: add requirements kanban with xp tracking"

  4. Pushen:

  - git push -u origin feature/anforderungen (oder main, je nach Branch-Policy)

  5. Wenn nötig, vorher Pull/merge:

  - git pull origin main (falls auf main arbeitest) und Konflikte lösen, dann erneut pushen.

  Sag Bescheid, falls ich die Commit-Message oder den Branch-Namen anpassen soll.
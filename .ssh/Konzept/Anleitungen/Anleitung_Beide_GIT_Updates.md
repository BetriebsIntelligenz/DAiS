# Beide GIT Updates

Kurzanleitung, um den lokalen Arbeitsstand zu sichern und denselben Stand auf GitLab/GitHub zu aktualisieren. Führe die Schritte nacheinander im Repository-Stamm (`/home/.../DAiS`) aus.

## 1. Aktuellen Zustand prüfen
```bash
git status -sb
```
Zeigt dir, welche Dateien geändert, neu oder gelöscht wurden und ob dein Branch dem Remote hinterherhinkt.

## 2. Alle Änderungen zum Commit vormerken
```bash
git add -A
```
Schiebt sämtliche Änderungen (inklusive neuer/gelöschter Dateien) in den Staging-Bereich, damit sie in den nächsten Commit aufgenommen werden.

## 3. Lokalen Snapshot erstellen
```bash
git commit -m "chore: local snapshot"
```
Legt einen Commit mit den gestagten Änderungen an. Passe die Nachricht an, falls du einen spezifischeren Kontext dokumentieren möchtest.

## 4. (Optional) Remotes bestätigen
```bash
git remote -v
```
Prüfe, ob `origin` (GitHub) auf `git@github.com:BetriebsIntelligenz/DAiS.git` und `gitlab` auf `git@gitlab.com:BetriebsIntelligenz/DAiS.git` zeigt. Fehlt ein Eintrag, kannst du ihn ergänzen oder korrigieren:
```bash
git remote add gitlab git@gitlab.com:BetriebsIntelligenz/DAiS.git
# bzw. git remote set-url gitlab <korrekte-url>
```

## 5. Branch nach GitHub (origin) pushen
```bash
git push origin feature/gamestyle
```
Überträgt deinen aktuellen Branch (`feature/gamestyle`) samt neuem Commit auf GitHub. Ersetze den Branch-Namen, wenn du auf einem anderen Branch arbeitest.

## 6. Branch nach GitLab spiegeln (gitlab)
```bash
git push gitlab feature/gamestyle
```
Synchronisiert denselben Stand mit dem GitLab-Remote. Auch hier ggf. den Branch-Namen anpassen.

## 7. Erfolg kontrollieren
```bash
git status -sb
```
Wenn keine Änderungen mehr offen sind und `## feature/gamestyle...origin/feature/gamestyle` angezeigt wird, sind lokale und Remote-Version synchron.

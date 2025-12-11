Führe folgende Änderungen durch. Prüfe dabei auch, ob im Admin Bereich zu diesem ein Einstellungsbereich gibt, und passe ggf. auch dort notwendige Inhalte an. Falls für die Anpassung Datenbank Änderungen notwendig sind, fasse kurz zusammen was du geändert hast.


** Status: Offen **
# Bereich:
MM5 — Day Planning
## Änderungen:
- entferne diesen bereich "Fortschritt: 3/3"
- Entferne die timer funktionalität
- Erstelle folgende neuen Features:
    - Folgende Aktivitäten zum abhacken:
        - Emails geprüft (ein feld für notiz zu einer email/ Textfeld)
        - Termine geprüft (ein texfeld zur eingabe welche vorbereitungen heute zu dem termin notwendig sind)
        - bei senden des formulars auf folgende seite weiterleiten http://localhost:3001/requirements ()
- Im kopfbereich der karte: Kopfbereich: „Heute ist Donnerstag, 11. Dezember“ (datum von heutigen tag)
- alle eingaben sollten wie bei (http://localhost:3001/programs/daily-checklist-body) in einem Verlauf ansehbar sein mit zeitstempel




** Status: Fertig **
# Bereich:
Neuer Bereich Namens: MED -- Meditation
Kategorie Bereich: Mind

## Features:
- Auswahl aus folgenden Dropdowns:
    - Sayajin Meditation
    - Earth Love Meditation
- Wenn mein ein Dropdown aklickt soll horizontal folgender Ablauf angezeigt werden:
    - Bei Sayajin Meditation:
        1. Durch Vibration und Visualisation Energieball um Körper erzeugen.
        2. Energieball um Wachsen lassen.
        3. Energieball in Statosphäre bewegen.
        4. Enegieball auf Erde splitten und an Energiebedürftige verteilen.

    - Bei Earth Love Meditation:
        1. Liebe an Erde senden
        2. Dankbarkeit an Erde senden

## Aufgaben
    1. Implemetiere das Programm genauso wie die bisherigen Programme
    2. Erstelle alle notwendigen Datenbank Änderungen im aktuellen Schema und zeige beim Output wie die neuen Änderungen in die laufende Docker Datenbank eingespielt werden können (Kurze Anleitung, benutze zur erstellung ähnliche Befehle wie hier bereits verwendet: .ssh/Konzept/Anleitungen/DB_Integration_VPS_Migration.md)
    3. Erstelle zu dem Programm im Admin Bereich einen Bereich, wo man anpassungen machen kann (Ähnlich wie bei den anderen Programmen)


** Status: Fertig **
# Bereich:
DB1 — Daily Body Checklist
## Änderungen:
- Bei "Morning Sport absolviert" folgende Auswahlfelder hinzufügen:
    - Calistenics
    - Freeletics
    - Schattenboxen
    - Laufen
    - Schwimmen
    - Boxsack
    - Fitness
- Zusätzlich soll hinter jedes auswahlfeld noch eine freies eingabefeld hinzugefügt werden, in dem die minuten eintragen kann
- Ändere den Timer so, dass man Start, Pause, Stop drücken kann und dass der Timer bei jedem unterpunkt (bsp. Kältebad)
- Entferne den Bereich "Kältebad" und "Sleep Tracker Wert"
- Nenne den Bereich um von "Daily Body Checklist" zu "Morgensport".
- Entferne den "Quick Mode" Button
- Ändere den Text  "Sport, Ernährung, Kältebad und Sleep Tracking." zu Morgen Sport Routine
- entferne den Text "DB1"

Ändere noch folgendes auf der Zweiten Seite von "MS1 — Morgensport":
- bei quality Ratings: ändere die namen der ratings zu foglenden:
    - Fokus zu Kraft
    - Tiefe zu Motivation
- Entferne diese Bereiche (Kriterien

Programm vollständig durchgezogen
Mind mindestens 70% Fokus
Realistisch
Nicht realistisch
) und "Regel-Check erfüllt"
- entferne auch die bereiche "Result & Reflektion" & "XP Vorschau"

Implementiere noch, dass unterhalb des bereichs "Morning Sport absolviert" ein dropdown erstellt wiird, den man anklicken kann und die durchgeführten MS1 — Morgensport eingaben sehen kann. die eingaben sollen kurz zusammengefasst bei "Programm abschließen" gespeichert werden. die eingaben sollen mit einem zeitstempel gespeichert werden (nutze zur umsetzung bereits vorhandene Code Strukturen wie bei Anforderungen oder Journals)


```
** Status: Offen **
# Bereich:

## Änderungen:
- 
```


** Status: Fertig **
# Bereich:
/mm1-incantations

## Änderungen:
- Entferne den schritt für schritt modus und erstelle stattdessen eine checkbox liste (jeder text soll eine kleine karte sein , die man mit der checkbox abhacken kann)#
- es soll foglende auswahlmöglichkeiten geben: 
    - Reichtum ist mein natürlicher Zustand	
    - Ich bin ein Magnet für Geld und Erfolg.	
    - Ich bin Energie.	
    - Ich bin gesund.	
    - Ich bin dankbar für meine Gesundheit.
unterhalb der karten soll eine scale (wie bei body morgen training) sein von 1 bis 10 mit den Titel "Intensivität"
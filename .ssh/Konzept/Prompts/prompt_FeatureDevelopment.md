# Änderung
Führe folgende Änderungen durch. Prüfe dabei auch, ob im Admin Bereich zu diesem ein Einstellungsbereich gibt, und passe ggf. auch dort notwendige Inhalte an. Falls für die Anpassung Datenbank Änderungen notwendig sind, fasse kurz zusammen was du geändert hast.



# Neu Erstellung
Erstelle folgedes neues Feature. Wenn du dafür neue SQL Anpassungen machst, gebe einen Hinweis bei deinem Output und falls mögliche führe die SQL Updates eigenständig durch (Anleitung: .ssh/Konzept/Anleitungen/DB_Integration_VPS_Migration.md). Nutze für die Entwicklung immer zuerst bereits implementierte Code strukturen und funktionen, und nur wenn du für die umsetzung dieses neues Features neue Funktionen brauchst entwickele sie neu. füge auch ein neues modul in "Cards" und "XP Center" ein um dieses neue Feature anpassen und ändern zu können.


** Status: Offen **
# Bereich: Mind

Name: Lesen

## Anforderungen:
- Der bereich soll man lese fortschritt eintragen können, mit gelesenen seiten anzahl und buch, dass aus einem dropdown auswählbar ist.
- der dropdown der bücher liste kann im admin bereich immer aktualisiert werden um neue bücher und auch bücher aus der liste zu löschen. bei änpassung soll diese änderung direkt in der karte ersichtlich sein.
- in der karten ansicht soll man einen log sehen können mit den einträgen (datum und uhrzeit) und seitenanzahl. nutze für die implementierung bereits vorhandene code strukturen (logging bereits in "http://localhost:3001/programs/daily-checklist-body", "verlauf anzeigen" implementiert. nur bei lese log soll der dropdown gleich geöffnet anzeigt werden, damit man gleich den log sehen kann)


# Vorlage #######################################################################

## Änderungen ###################################################################

** Status: Offen **
# Bereich:

# Kategorie:
- 

## Änderungen:
- 

## Neu Erstellungen #############################################################

** Status: Offen **
# Bereich:

## Anforderungen:
- 

# ###############################################################################



** Status: Fertig **
# Bereich:
Daily Human Checklist


# Kategorie:
- Human

## Änderungen:
- Im Admin Bereich soll man Personen angelegt werden können mit Auswahl wie (Familie, Freund, Kollege, Business Partner, Network) via dropdown vergeben können
- Es soll in den Admin Bereich soll man dann je erstellter Person täglich / wöchentlich aufgaben zu ordnen können wie (WhatsApp Nachricht, Anruf, E-Mail, Treffen, Video Call)
- Bei der Karten Ansicht (http://localhost:3001/programs/daily-checklist-human) soll man dann aktiviäten tracken können wie (WhatsApp Nachricht, Anruf, E-Mail, Treffen, Video Call). zu jede eingabe soll ein log / verlauf (nutze bereits vorhanden code strukturen im code um die implementierung zu vereinfachen) pro Person erstellt werden den man in dieser anischt mittels einem dropdown ansehen kann.
- auf der karten ansicht soll man auch eine live statistik sehen können von der kontakt verteilung je person.
- Alle Anpassungen des systems sollen im admin bereich möglich sein.



** Status: Fertig **
# Bereich:
Haushalt

# Kategorie:
- ENVIRONMENT

## Anforderungen:
Es soll möglich sein Karten anzulegen für wochentage. dabei soll es eine liste von aufgaben geben die man den karten zuordnen kann und die immer zum abhacken sind. implementiere auch eine wochen ansicht funktion, wo im wochenstrahl (montag - sonntag) angezeigt wird wann welche "Haushalts" Karte gespeichert wurde.
    - 1.Aufgeräumt
    - 2.Geschirr in Spühlmaschine getan
    - 3.Wäsche gewaschen
    - 4.Boden gewischt
    - 5.Müll entsorgt
    - 6.Handwerkliche Aufgabe erledigt
    - 7.Essen zubereitet
    - 8.Einkaufen gewesen
- Jede eingabe soll wie im "Morning Sport absolviert" Verlauf geloggt werden (wende die gleichen codes an)
- Im Admin Bereich soll volle bearbeitung und anpassung dieses features möglich sein.




** Status: Fertig **
# Bereich:
Cheklist

## Anforderungen:
- Erstelle eine Checklist Tabelle für folgende Punkte mit einem 5 Stufen Radio Button reihe:
    - State
    - Körperhaltung
    - Energy
    - Gesunde Ernährung
    - Fokus
    - Konzentration
    - Disziplin
- Jede eingabe soll wie im "Morning Sport absolviert" Verlauf geloggt werden (wende die gleichen codes an)




** Status: Fertig **
# Bereich:
State Controll

## Änderungen:
- Alle States (Bsp. LIGHT) sollen untereinander in einer tabelle stehen. jedes der states soll einen eigenen schiebregler / slider haben.
- bei jeder eingabe soll unterhalb eine speicherung (zum ausklappen) entstehen (nutze den gleichen code).
- entferne noch die timer (00:00 / Start / Pause)
- entferne die weiteren seiten nach der eingabe (bsp. Fortschritt: 1/7
LOVE LIGHT HERO LEADER INNOVATOR POWER HUMAN IQ SOURCE Quality Ratings Fokus: 6 Tiefe: 6 Zufriedenheit: 6 Kriterien Programm vollständig durchgezogen Mind mindestens 70% Fokus Realistisch Nicht realistisch State Check nach dem Programm (-) Regel-Check erfüllt Result & Reflektion Was habe ich konkret erreicht? Was hat sich an meinem State oder Verhalten verändert? Was nehme ich mit? XP Vorschau Basis XP: 500 · Durchschnittsqualität: 6.0 mind: 100%), sodass die eingaben die auf seite 1 davon sind die ganze programm seite ausmachen. 

---



** Status: Fertig **
# Bereich:
Wake Up Programm

## Anforderungen:
- Eine Chekliste mit folgenden Inhalten:
    - Earth Love Meditation
    - Dankbarkeits Meditation
    - Visualisierung
    - Power Health Shot
    - Pump Up Session
- Die Eingaben sollen wie bei "Verlauf - Day Planning Log" bei "Day Planning" immer gespeichert werden mit zeitstempel



** Status: Fertig **
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
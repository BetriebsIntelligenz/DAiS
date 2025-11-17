> Prompt bei ChatGPT

Erstelle eine beschreibung folgender software. das ziel ist es anhand dieser beschreibung einem coder agent diese applikation entwickeln zu lassen. reichere dieses konzept mit dem Daten aus diesem Projekt (DAiS) an. 

# Konzept der Applikation
- Durchführen von Programmen mittels Formular
- Tracking von Aktivitäten
- Sammeln von Punkten fur Aufgaben

# System Beschreibung
Der User bediehnt das Programm Formular und führt übungen durch. er gibt im formular werte ein und bestätigt checkboxen bei der durchführung der übungen. mit jeder eingabe sammelt der user punkte und kann diese im score dashboard ansehen. bei der ansicht belohnungen kann der user dann die erarbeiteten punkte gegen davor selbst definierte prämien eintauschen.

# Interfaces
## Seite: Menu
## Seite: Programm Formular
## Seite: Score Dashboard
## Seite: Belohnungen
## Seite: Admin Dashboard
## Seite: Journale

# Anforderungen
- Komplett Mobil orientiert
- Sehr ästetische und modernes Eingabe Formular
- Es soll ein sicheres login möglich sein, user profile sollen vorhanden sein (alles in Postgres)
- Farbgebung: Schöne Ästetische Gelb farbverläufe wählen. Weiß und gelb mit viel gelb anteil
- Das Programm Formular soll dynamische weiterleitungen erlauben, dass heißt dass die Einheiten und Übungen (aus den dokumenten im Ordner DAiS) entweder als einzelnes gesendet werden können oder mit weiter die nächsten übungen kommen.
- erstelle vollumfänglich das komplette sql schema für diese applikation in postgres und bereite die dokumente die ich in die datenbank manuell eingeben muss als datein zum kopieren und pasten vor.
- bei belohnungen soll der user sehen können welche belohnungen er gegen wie viel punkte wann eingetauscht hat. er soll auch seinen aktuellen punkte stand sehen und die preise für die belohnungen.s
- Bei Journale soll der User mit einem HTML Editor einen Journal schreiben können (Es gibt drei journale entnehme sie den daten, lern journal, erfolgs journal, dankbarkeits journal). bei jedem speichern soll de neue text unterhalb dem letzten block hinzugefügt werden. damit sieht der user die historie des journals. ein eintrag soll immer mit datum und uhrzeit gespeichert werden.
- In der Admin ansicht soll der user neue programme hinzufügen und bestehende verwalten und ändern können. zudem soll er neue belohnungen hinzufügen können und den preis dafür eingeben und ändern können.
- Das Programm Menu soll nach den kategorien (Mind, Body, Human, Environment, Business) strukturiert sein. die programme sollen in diese kategorien sortiert werden. zuerst soll immer in der hauptansicht alle programm blöcke angezeigt werden. erst nach dem klick auf ein programm öffnet sich die formular ansicht.


# Hilfreiche Dokumente:
.ssh/Konzept/Prompts/Input_Systemdescription.md



# Technologie
- Nextjs
- Postgres

Als Test System soll ich mit npn dev eine umegbung haben. dazu kann ich davor schon den postgres container lokal erstellen und die applikation schon da einbinden bis dann die applikation auch zu einem docker container erstellt wird.
Final soll das System in zwei Docker Containern laufen und mittels einem docker-compose file erstellt werden.


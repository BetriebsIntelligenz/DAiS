Hier ist eine komplette, für einen Coder-Agent verwertbare Beschreibung inkl. Postgres-Schema und vorbereiteten Seed-Dateien.

---

## 1. Fachliche Beschreibung der DAiS-App

Die App ist eine digitale Umsetzung des DAiS-Systems (DAiS / ☼ DAiS / ✺DAIS 2025 / DAIZ, STATE CONTROLL, RULES CHECKLIST usw.).
Sie verbindet **Programme**, **Checklisten**, **States** und **XP-Punkte** in einer mobilen Web-App.

### Kern-Idee

* User wählen aus einem **Programmen-Menü** (Mind, Body, Human, Environment, Business).
* Sie führen Programme über ein **dynamisches Formular** aus (z. B. „Incantations“, „Visualisierungstraining“, „Morning Program“, „State Controll“, „Rules Checklist“, „Day Checklist“).
* Jede bestätigte Übung / Checkbox / Bewertung erzeugt **XP-Punkte** in der Kategorie (Mind / Body / …).
* Im **Score Dashboard** sieht der User:

  * Gesamt-XP
  * XP nach Kategorien
  * Verlauf der Aktivitäten / Programme
* Unter **Belohnungen** kann der User XP gegen selbst definierte Rewards eintauschen (z. B. „Kinoabend“, „Freier Tag“, „Neue Uhr“).

  * Er sieht: aktuelle XP, verfügbare Rewards mit Preis, sowie Historie der Einlösungen.
* Unter **Journale** kann der User in drei Journals schreiben:

  * **Lern Journal**
  * **Erfolgs Journal**
  * **Dankbarkeits Journal**
  * Jeder Speichern-Klick erzeugt einen neuen Block (HTML), chronologisch mit Datum/Uhrzeit.

### Seiten / Interfaces

#### 1. Menu

* Vollbild-Mobile-Ansicht mit 5 großen Karten:

  * **Mind**
  * **Body**
  * **Human**
  * **Environment**
  * **Business**
* Jede Karte öffnet eine Liste von Programmen (Blöcke) aus diesem Bereich:

  * Beispiele Mind:

    * MM1 – Incantations (DAiS)
    * MM3 – Visualisierungstraining (DAiS)
    * MM4 – Ziele Vorlesen (DAiS)
    * MM5 – Day Planning (DAiS)
    * STATE CONTROLL
    * RULES CHECKLIST
    * Daily Checklist Mind (☼ DAiS / DAIZ)
  * Body:

    * Morning Sport / Sport Programm (☼ DAiS / DAIZ)
    * Energize / Kältebad / Freeletics / Sleep Tracker
    * Daily Checklist Body
  * Human:

    * Family Program / Humans / Chat Program / Meet Program
    * Daily Checklist Humanity
  * Environment:

    * Environment Program / Haushalt / Cleaning / Garden / Shaggy Program
    * Daily Checklist Environment
  * Business:

    * Business Development Program
    * Virtuelles Kundencenter Program
    * Immobilien Projektentwicklungs Programm
    * Daily Checklist Business

#### 2. Programm Formular

* Für jedes Programm existiert ein **konfigurierbares Formular**, das in der DB modelliert ist (Programm → Units → Exercises).

* Eingabetypen (konfigurierbar pro Exercise):

  * Checkbox (Ja/Nein)
  * Multi-Select
  * Skalen (z. B. 1–5, 1–10 für STATE CONTROLL Levels LOVE, LIGHT, HERO, LEADER, INNOVATOR, POWER HUMAN, IQ SOURCE)
  * Text / Textarea
  * Zahl / Minuten / Stunden
  * HTML/Journaling (optional)

* Beispiele aus DAiS:

  * **MM1 – Incantations**

    * Ziele (Auswendig Können, Verinnerlichen, Verstärken neuer Gehirnstrukturen)
    * State (Skala 1–5 für Begeisterung, Energy, Selbstsicherheit)
    * Role (Coach/Spirit, Skala 1–5)
    * Ritual (mehrere „Ich bin…“-Sätze, 5x wiederholen)
    * Quality & Result (Fokus ≥ 70 %?, alle Incantations erledigt?)
    * XP-Optionen (300/600/900 XP)
  * **MM5 – Day Planning**

    * Fragen: „Was ist das wichtigste…?“, „Was sind meine Ziele heute?“, Termine, Optimierung, E-Mails/Briefe gecheckt.
  * **STATE CONTROLL**

    * LOVE / LIGHT / HERO / LEADER / INNOVATOR / POWER HUMAN / IQ SOURCE (1–10).
  * **RULES CHECKLIST**

    * Rauchfrei, Gesund, Diszipliniert, Reichtum, Erfolg, Mind Push, State Controll, Action, Meditation, Social Value, Family Value, Daily Body Workout (Ja/Nein).
  * **DAY / WEEK / MONTH / XP (☼ DAiS, ✺DAIS 2025, DAIZ)**

    * Day: Morgen/Mittag/Abend mit Sayajin Meditation, Incantations, Ziele, Motivation, Sport, Cleaning, Brain Development, Mind State Check, Family Activities, Haushalt, Research, Drinks & Food Tracker, Journals, Daily Checklists.
    * Week: Briefe, Mails, Finanzen, Termine (Office/Administration).
    * Month: Monats-Check / Planung.
    * XP: Manuelles Verteilen von XP auf Mind/Body/Human/Environment/Business.

* **Dynamische Weiterleitungen / Flow**

  * Das Formular kann Programme in zwei Modi ausspielen:

    * **Einzel-Modus**: nur eine Einheit/Übung (z. B. nur „Incantations“ heute).
    * **Flow-Modus**: mehrere Units/Exercises nacheinander (z. B. vollständiges Morning Program).
  * Die Flow-Logik orientiert sich an den vorhandenen DAiS-Flows (z. B. „Programm auswählen → Abschnitt MORGEN/TAG/ABEND → Unterprogramm auswählen“).

* Beim Absenden eines Formulars entsteht:

  * 1 `program_run` (Session)
  * n `program_run_exercise_value` (Antworten)
  * 1+ `xp_transaction` (automatische XP-Gutschriften je nach Antworten)

#### 3. Score Dashboard

* Anzeige pro User:

  * Gesamt-XP (Summe aller `xp_transaction` vom Typ `earn` minus `spend`).
  * XP nach Kategorien: Mind / Body / Human / Environment / Business.
  * Letzte Aktivitäten (Liste der letzten `program_runs` mit Programmnamen, Datum, XP).
  * Optional: State-Übersicht (z. B. Durchschnitts-LOVE aus STATE CONTROLL).

#### 4. Belohnungen

* User sieht:

  * **Verfügbare Rewards**: Name, Beschreibung, XP-Preis.
  * **Aktuellen XP-Stand** (berechnet aus `xp_transaction`).
  * **Historie der Einlösungen**: Welche Belohnung, wann eingelöst, Status (pending/approved/rejected/cancelled).
* Ein Klick auf „Einlösen“ erzeugt:

  * `reward_redemption` (pending)
  * `xp_transaction` vom Typ `spend` mit negativem XP-Betrag.
* Admin kann im Admin-Dashboard den Status auf „approved“ setzen.

#### 5. Journale

* Drei Journals (aus ✺DAIS / ☼ DAiS / DAIZ abgeleitet):

  * `Lern Journal`
  * `Erfolgs Journal`
  * `Dankbarkeits Journal`
* UI:

  * Rich-Text / HTML-Editor (z. B. TipTap, Quill etc.).
  * Beim Speichern wird **nicht** überschrieben, sondern ein **neuer Eintrag** (`journal_entry`) angelegt.
  * Anzeige: chronologische Blöcke mit Datum/Uhrzeit + HTML Inhalt.

#### 6. Admin Dashboard

* Bereiche:

  * **Programme verwalten**

    * Programm anlegen/bearbeiten (Name, Code, Kategorie/Area, Beschreibung, Frequenz, erwartete Dauer, XP).
    * Programm Units/Exercises konfigurieren (Label, Typ, Optionen, XP).
  * **Belohnungen verwalten**

    * Rewards anlegen/bearbeiten/deaktivieren.
    * XP-Preis definieren.
  * **XP-Anpassungen**

    * Manuelle XP-Buchungen (z. B. Übertrag aus altem System).
  * Optional: Export der Daten (CSV).

---

## 2. Technische Architektur

* **Frontend**: Next.js (Full SPA/SSR, mobil-optimiertes Design).

  * Hauptfarben: Weiß + Gelb mit Gelb-Verläufen.
  * Fokus auf große, gut klickbare Elemente und Multi-Step-Forms.
* **Backend**:

  * API-Layer (Next.js API Routes oder separates Node/Express) mit:

    * Auth (JWT/Session)
    * CRUD für Programme, ProgramRuns, XP, Rewards, Journals.
* **Datenbank**: PostgreSQL

  * Läuft zunächst lokal im Docker-Container.
* **Deployment**:

  * Final: 2 Docker-Container:

    * `web` (Next.js App)
    * `db` (Postgres)
  * `docker-compose.yml` verbindet beide.

---

## 3. Postgres Schema (`schema.sql`)

```sql
-- ============================================================================
-- Extensions
-- ============================================================================
CREATE EXTENSION IF NOT EXISTS "pgcrypto";

-- ============================================================================
-- Enums
-- ============================================================================
DO $$
BEGIN
    IF NOT EXISTS (SELECT 1 FROM pg_type WHERE typname = 'input_type') THEN
        CREATE TYPE input_type AS ENUM (
            'checkbox',
            'multi_select',
            'scale_1_5',
            'scale_1_10',
            'number',
            'text',
            'textarea',
            'html',
            'date',
            'time'
        );
    END IF;

    IF NOT EXISTS (SELECT 1 FROM pg_type WHERE typname = 'xp_transaction_type') THEN
        CREATE TYPE xp_transaction_type AS ENUM ('earn', 'spend', 'adjust');
    END IF;

    IF NOT EXISTS (SELECT 1 FROM pg_type WHERE typname = 'program_frequency') THEN
        CREATE TYPE program_frequency AS ENUM ('daily', 'weekly', 'monthly', 'custom');
    END IF;

    IF NOT EXISTS (SELECT 1 FROM pg_type WHERE typname = 'program_mode') THEN
        CREATE TYPE program_mode AS ENUM ('single', 'flow');
    END IF;

    IF NOT EXISTS (SELECT 1 FROM pg_type WHERE typname = 'reward_status') THEN
        CREATE TYPE reward_status AS ENUM ('pending', 'approved', 'rejected', 'cancelled');
    END IF;

    IF NOT EXISTS (SELECT 1 FROM pg_type WHERE typname = 'journal_code') THEN
        CREATE TYPE journal_code AS ENUM ('learn', 'success', 'gratitude');
    END IF;
END$$;

-- ============================================================================
-- User & Profile
-- ============================================================================
CREATE TABLE IF NOT EXISTS app_user (
    id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email         VARCHAR(320) NOT NULL UNIQUE,
    password_hash TEXT         NOT NULL,
    display_name  TEXT,
    timezone      TEXT         NOT NULL DEFAULT 'Europe/Berlin',
    is_admin      BOOLEAN      NOT NULL DEFAULT FALSE,
    created_at    TIMESTAMPTZ  NOT NULL DEFAULT now(),
    updated_at    TIMESTAMPTZ  NOT NULL DEFAULT now()
);

CREATE TABLE IF NOT EXISTS user_profile (
    user_id     UUID PRIMARY KEY REFERENCES app_user(id) ON DELETE CASCADE,
    first_name  TEXT,
    last_name   TEXT,
    birthdate   DATE,
    avatar_url  TEXT,
    bio         TEXT,
    goals_text  TEXT,
    created_at  TIMESTAMPTZ NOT NULL DEFAULT now(),
    updated_at  TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- ============================================================================
-- Areas / Kategorien (Mind, Body, Human, Environment, Business)
-- ============================================================================
CREATE TABLE IF NOT EXISTS area (
    id          SERIAL PRIMARY KEY,
    code        TEXT NOT NULL UNIQUE,   -- 'mind', 'body', 'human', 'environment', 'business'
    name        TEXT NOT NULL,          -- Anzeige-Name
    description TEXT
);

-- ============================================================================
-- Programme
-- ============================================================================
CREATE TABLE IF NOT EXISTS program (
    id                     UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    code                   TEXT UNIQUE,   -- z.B. 'MM1', 'MM4', 'STATE', 'RULES'
    area_id                INTEGER NOT NULL REFERENCES area(id),
    name                   TEXT    NOT NULL,
    description            TEXT,
    is_active              BOOLEAN NOT NULL DEFAULT TRUE,
    default_frequency      program_frequency NOT NULL DEFAULT 'daily',
    default_weekly_target  INTEGER,             -- z.B. 7 für "täglich"
    estimated_minutes      INTEGER,             -- durchschnittliche Dauer
    source_form            TEXT,                -- 'DAiS', '☼ DAiS', '✺DAIS 2025', 'DAIZ', 'STATE CONTROLL', etc.
    created_by             UUID REFERENCES app_user(id),
    created_at             TIMESTAMPTZ NOT NULL DEFAULT now(),
    updated_at             TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- Programm-Units (logische Abschnitte innerhalb eines Programms)
CREATE TABLE IF NOT EXISTS program_unit (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    program_id  UUID    NOT NULL REFERENCES program(id) ON DELETE CASCADE,
    position    INTEGER NOT NULL,
    title       TEXT    NOT NULL,  -- z.B. 'Ziele', 'STATE', 'ROLE', 'RITUAL'
    description TEXT,
    xp_base     INTEGER NOT NULL DEFAULT 0,
    is_optional BOOLEAN NOT NULL DEFAULT FALSE,
    UNIQUE (program_id, position)
);

-- Exercises/Feldelemente innerhalb einer Unit
CREATE TABLE IF NOT EXISTS program_exercise (
    id               UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    program_unit_id  UUID        NOT NULL REFERENCES program_unit(id) ON DELETE CASCADE,
    position         INTEGER     NOT NULL,
    key              TEXT,                 -- maschinenlesbar (z.B. 'focus_70_percent', 'smoke_free')
    label            TEXT        NOT NULL, -- Label für UI
    help_text        TEXT,
    input_type       input_type  NOT NULL,
    config           JSONB,               -- Optionen (Skalenwerte, Checkbox-Optionen etc.)
    xp_value         INTEGER     NOT NULL DEFAULT 0,
    is_required      BOOLEAN     NOT NULL DEFAULT FALSE,
    UNIQUE (program_unit_id, position)
);

-- ============================================================================
-- Ausführungen (Runs) & Antworten
-- ============================================================================
CREATE TABLE IF NOT EXISTS program_run (
    id               UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id          UUID NOT NULL REFERENCES app_user(id) ON DELETE CASCADE,
    program_id       UUID NOT NULL REFERENCES program(id) ON DELETE CASCADE,
    mode             program_mode NOT NULL DEFAULT 'flow',
    started_at       TIMESTAMPTZ  NOT NULL DEFAULT now(),
    completed_at     TIMESTAMPTZ,
    total_xp_earned  INTEGER       NOT NULL DEFAULT 0,
    note             TEXT
);

CREATE INDEX IF NOT EXISTS idx_program_run_user ON program_run(user_id);
CREATE INDEX IF NOT EXISTS idx_program_run_program ON program_run(program_id);

CREATE TABLE IF NOT EXISTS program_run_exercise_value (
    id                 UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    program_run_id     UUID NOT NULL REFERENCES program_run(id) ON DELETE CASCADE,
    program_exercise_id UUID NOT NULL REFERENCES program_exercise(id) ON DELETE CASCADE,
    value_text         TEXT,
    value_number       NUMERIC,
    value_boolean      BOOLEAN,
    value_json         JSONB,
    created_at         TIMESTAMPTZ NOT NULL DEFAULT now(),
    UNIQUE (program_run_id, program_exercise_id)
);

CREATE INDEX IF NOT EXISTS idx_prev_run ON program_run_exercise_value(program_run_id);

-- ============================================================================
-- Rewards & XP
-- ============================================================================
CREATE TABLE IF NOT EXISTS reward (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name        TEXT    NOT NULL,
    description TEXT,
    xp_cost     INTEGER NOT NULL,
    is_active   BOOLEAN NOT NULL DEFAULT TRUE,
    created_by  UUID REFERENCES app_user(id),
    created_at  TIMESTAMPTZ NOT NULL DEFAULT now(),
    updated_at  TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE IF NOT EXISTS reward_redemption (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    reward_id   UUID NOT NULL REFERENCES reward(id),
    user_id     UUID NOT NULL REFERENCES app_user(id) ON DELETE CASCADE,
    xp_cost     INTEGER NOT NULL,
    status      reward_status NOT NULL DEFAULT 'pending',
    created_at  TIMESTAMPTZ NOT NULL DEFAULT now(),
    approved_at TIMESTAMPTZ,
    comment     TEXT
);

CREATE INDEX IF NOT EXISTS idx_reward_redemption_user ON reward_redemption(user_id);

CREATE TABLE IF NOT EXISTS xp_transaction (
    id                    UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id               UUID NOT NULL REFERENCES app_user(id) ON DELETE CASCADE,
    area_id               INTEGER REFERENCES area(id),
    program_run_id        UUID REFERENCES program_run(id) ON DELETE SET NULL,
    reward_redemption_id  UUID REFERENCES reward_redemption(id) ON DELETE SET NULL,
    type                  xp_transaction_type NOT NULL,
    xp_amount             INTEGER NOT NULL,
    description           TEXT,
    created_at            TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE INDEX IF NOT EXISTS idx_xp_user ON xp_transaction(user_id);
CREATE INDEX IF NOT EXISTS idx_xp_area ON xp_transaction(area_id);

-- ============================================================================
-- Journale
-- ============================================================================
CREATE TABLE IF NOT EXISTS journal_type (
    id          SERIAL PRIMARY KEY,
    code        journal_code NOT NULL UNIQUE,  -- 'learn', 'success', 'gratitude'
    name        TEXT         NOT NULL,
    description TEXT
);

CREATE TABLE IF NOT EXISTS journal_entry (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id         UUID NOT NULL REFERENCES app_user(id) ON DELETE CASCADE,
    journal_type_id INTEGER NOT NULL REFERENCES journal_type(id),
    content_html    TEXT NOT NULL,
    created_at      TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE INDEX IF NOT EXISTS idx_journal_entry_user ON journal_entry(user_id);
CREATE INDEX IF NOT EXISTS idx_journal_entry_type ON journal_entry(journal_type_id);

-- ============================================================================
-- Optionale Tabelle: Manuelle XP-Inputs (z.B. DAIZ "MANUELL XP")
-- ============================================================================
CREATE TABLE IF NOT EXISTS manual_xp_input (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id     UUID NOT NULL REFERENCES app_user(id) ON DELETE CASCADE,
    area_id     INTEGER REFERENCES area(id),
    xp_amount   INTEGER NOT NULL,
    note        TEXT,
    created_at  TIMESTAMPTZ NOT NULL DEFAULT now()
);
```

---

## 4. Seed-Daten zum Kopieren & Einfügen

### 4.1 `seed_areas.sql` (Kategorien / Menü)

```sql
-- seed_areas.sql
INSERT INTO area (code, name, description) VALUES
('mind',        'Mind',        'Mentale Programme, STATE CONTROLL, RULES CHECKLIST, Incantations, Visualisierungen, Day/WEEK/MONTH/XP Checks.'),
('body',        'Body',        'Körper, Sport, Energize, Schlaf, Ernährung, Kältebad, Daily Checklist Body.'),
('human',       'Human',       'Familie, Freunde, Social Value, Family Value, Family Program, Chat/Meet Programme.'),
('environment', 'Environment', 'Wohnung, Haushalt, Garten, Shaggy, Ordnung, Environment Program, Daily Checklist Environment.'),
('business',    'Business',    'Business Development, Finanzen, Virtuelles Kundencenter, Immobilien Projektentwicklung, Daily Checklist Business.');
```

---

### 4.2 `seed_journal_types.sql`

```sql
-- seed_journal_types.sql
INSERT INTO journal_type (code, name, description) VALUES
('learn',      'Lern Journal',         'Reflexion über Lernen, Kurse, Skill-Aufbau.'),
('success',    'Erfolgs Journal',      'Tägliche/Wöchentliche Erfolge, Wins & Fortschritte.'),
('gratitude',  'Dankbarkeits Journal', 'Dankbarkeit, Happiness, positive Fokussierung.');
```

---

### 4.3 `seed_programs_basic.sql`

(Grundprogramme aus DAiS / ☼ DAiS / ✺DAIS / DAIZ)

```sql
-- seed_programs_basic.sql
-- Mind-Programme (DAiS)
INSERT INTO program (code, area_id, name, description, default_frequency, default_weekly_target, estimated_minutes, source_form)
VALUES
('MM1', (SELECT id FROM area WHERE code = 'mind'),
 'Incantations',
 'Bei Incantations werden Sätze im "IST" Format nacheinander 5x gesprochen. Ziele: Begeisterung, Energy, Selbstsicherheit.',
 'daily', 6, 5, 'DAiS'),

('MM3', (SELECT id FROM area WHERE code = 'mind'),
 'Visualisierungstraining',
 'Visualisierungstraining: Zielvorstellung fühlen, Objekte detailliert sehen (Vision Hublot, Rolls Royce, 7.000.000€, Business, Haus usw.).',
 'daily', 7, 10, 'DAiS'),

('MM4', (SELECT id FROM area WHERE code = 'mind'),
 'Ziele Vorlesen',
 'Lesen der persönlichen Ziele und Milestones (Human Architecture System, Einkommen, Haus, Firmengebäude usw.).',
 'daily', 14, 5, 'DAiS'),

('MM5', (SELECT id FROM area WHERE code = 'mind'),
 'Day Planning',
 'Planung und Erhöhung der Effektivität des aktuellen Tages: wichtigste Aufgabe, Tagesziele, Termine, Optimierung, E-Mails/Briefe.',
 'daily', 5, 10, 'DAiS'),

('MT1', (SELECT id FROM area WHERE code = 'mind'),
 'DreamTour',
 'Wenn Timer klingelt: innerhalb der nächsten 5 Minuten Visualisation / Power-Nap-Tour mit allen Sinnen (Creator/Seher-Rolle).',
 'daily', 7, 3, 'DAiS'),

('MA8', (SELECT id FROM area WHERE code = 'mind'),
 '5 Areas Checklist',
 'Checklist der 5 Areas zur Abfrage der richtigen Zustände in Mind/Body/Human/Environment/Business.',
 'weekly', 7, 5, 'DAiS'),

('STATE', (SELECT id FROM area WHERE code = 'mind'),
 'STATE CONTROLL',
 'State Controll mit Skalen 1-10 für LOVE, LIGHT, HERO, LEADER, INNOVATOR, POWER HUMAN, IQ SOURCE.',
 'daily', 1, 5, 'STATE CONTROLL'),

('RULES', (SELECT id FROM area WHERE code = 'mind'),
 'RULES CHECKLIST',
 'Rules Checklist: Rauchfrei, Gesund, Diszipliniert, Reichtum, Erfolg, Mind Push, State Controll, Action, Meditation, Social/Family Value, Daily Body Workout.',
 'daily', 1, 5, 'RULES CHECKLIST'),

('DAY_CHECK_MIND', (SELECT id FROM area WHERE code = 'mind'),
 'Daily Checklist Mind',
 'Tägliche Mind-Checklist aus ☼ DAiS / DAIZ: Disziplin, richtige Entscheidungen, keine Prokrastination, State halten, Zielnähe, Lebensqualität.',
 'daily', 7, 5, '☼ DAiS / DAIZ'),

-- Body-Programme
('BODY_MORNING', (SELECT id FROM area WHERE code = 'body'),
 'Morning Sport',
 '☼ DAiS / DAIZ Sportprogramm: Freeletics, Barring, Fitness, Boxsack, Schattenboxen, Seilspringen, Joggen, Schwimmen, Kampfsport, Basketball.',
 'daily', 5, 30, '☼ DAiS / DAIZ'),

('SLEEP_TRACKER', (SELECT id FROM area WHERE code = 'body'),
 'Sleep Tracker',
 'Schlaf-Tracker (mindestens 5 Stunden, Healing Program 6h Schlaf).',
 'daily', 7, 1, '☼ DAiS / ✺DAIS'),

('DAY_CHECK_BODY', (SELECT id FROM area WHERE code = 'body'),
 'Daily Checklist Body',
 'Daily Checklist Body: Rauchfrei, gesund ernährt, Körper gepflegt, nur Wasser/Tee/Kaffee, Bewegung.',
 'daily', 7, 5, '☼ DAiS / DAIZ'),

-- Human-Programme
('FAMILY_PROG', (SELECT id FROM area WHERE code = 'human'),
 'Family Program',
 'Family Program mit Sonntagsessen, Sonntagsfrühstück, gemeinsamen Erlebnissen, Anya-Treffen usw.',
 'weekly', 1, 120, '☀ DAIZ'),

('HUMANS', (SELECT id FROM area WHERE code = 'human'),
 'Humans Programm',
 'Humans: Chat, Call, Video Call, Real Meeting, Erlebnisse für Kontakte wie Kimberly, Anya, Öcsi, etc.',
 'weekly', 2, 60, '☀ DAIZ'),

('DAY_CHECK_HUMAN', (SELECT id FROM area WHERE code = 'human'),
 'Daily Checklist Humanity',
 'Daily Checklist Humanity: Beziehung zur Familie verbessern, freundlich und respektvoll sein, ehrlich sein.',
 'daily', 7, 5, '☼ DAiS / DAIZ'),

-- Environment-Programme
('ENV_PROG', (SELECT id FROM area WHERE code = 'environment'),
 'Environment / Haushalt',
 'Environment Program: Aufräumen, Putzen, Wäsche waschen, Müll entsorgen, Pflege, Garten, Shaggy-Programm.',
 'daily', 7, 20, '☼ DAiS / ☀ DAIZ'),

('DAY_CHECK_ENV', (SELECT id FROM area WHERE code = 'environment'),
 'Daily Checklist Environment',
 'Daily Checklist Environment: Umwelt gepflegt, im Haushalt unterstützt, Umfeld ordentlich.',
 'daily', 7, 5, '☼ DAiS / DAIZ'),

-- Business-Programme
('BUS_DEV', (SELECT id FROM area WHERE code = 'business'),
 'Business Development Program',
 'Business Development Program: LinkedIn Netzwerk erweitern, Business Development, Akquiseplanung für nächsten Tag.',
 'daily', 5, 20, '✺DAIS 2025'),

('VKC', (SELECT id FROM area WHERE code = 'business'),
 'Virtuelles Kundencenter',
 'Virtuelles Kundencenter Programm: Business lunch, KPIs, Cloud-Software, Akquise von Mitarbeitern & Kunden.',
 'weekly', 3, 60, '☀ DAIZ'),

('IMMO_DEV', (SELECT id FROM area WHERE code = 'business'),
 'Immobilien Projektentwicklungs Programm',
 'Immobilien-Projektentwicklungs Programm: Projekte konzipieren, Baurecht, Investment, Wohnbau-Genossenschaften.',
 'weekly', 3, 120, '☀ DAIZ'),

('DAY_CHECK_BUS', (SELECT id FROM area WHERE code = 'business'),
 'Daily Checklist Business',
 'Daily Checklist Business: Umsatz generiert? Business optimiert? Netzwerk erweitert?',
 'daily', 7, 5, '☼ DAiS / DAIZ');
```

---

### 4.4 `seed_rewards_example.sql`

(Beispiel-Rewards, die du später im Admin anpassen kannst)

```sql
-- seed_rewards_example.sql
INSERT INTO reward (name, description, xp_cost)
VALUES
('Kinoabend', 'Ein Abend im Kino mit Familie/Freund(in).', 1500),
('Freier Tag', 'Ein komplett freier Tag ohne Verpflichtungen.', 3000),
('Neues Buch', 'Ein neues Buch zur persönlichen Entwicklung.', 1000),
('Kurzurlaub', 'Wochenendtrip (Hotel, Reise etc.).', 10000);
```

---

### 4.5 Beispiel: Mapping eines Programms auf Units & Exercises (`seed_mm1_example.sql`)

Optionales Beispiel, wie du **MM1 – Incantations** in Units/Exercises aufbaust.
(Die anderen Programme folgen dann dem gleichen Muster.)

```sql
-- seed_mm1_example.sql
-- Beispiel: Program Units & Exercises für MM1 (Incantations)

-- 1) Unit "Ziele" anlegen
WITH u_ziele AS (
    INSERT INTO program_unit (program_id, position, title, description, xp_base, is_optional)
    VALUES (
        (SELECT id FROM program WHERE code = 'MM1'),
        1,
        'Ziele',
        'Auswendig Können der Incantations, Verinnerlichen des neuen Mindsets, Verstärken neuer Gehirnstrukturen.',
        0,
        FALSE
    )
    RETURNING id
)
INSERT INTO program_exercise (program_unit_id, position, key, label, help_text, input_type, config, xp_value, is_required)
SELECT
    u_ziele.id, 1, 'incantations_memorized',
    'Auswendig Können der Incantations',
    NULL,
    'checkbox',
    NULL,
    100,
    FALSE
FROM u_ziele;

-- 2) Unit "STATE" (z.B. Begeisterung, Energy, Selbstsicherheit)
WITH u_state AS (
    INSERT INTO program_unit (program_id, position, title, description, xp_base, is_optional)
    VALUES (
        (SELECT id FROM program WHERE code = 'MM1'),
        2,
        'STATE',
        'Selbsteinschätzung der Emotionen (z.B. Begeisterung, Energy, Selbstsicherheit).',
        0,
        FALSE
    )
    RETURNING id
)
INSERT INTO program_exercise (program_unit_id, position, key, label, help_text, input_type, config, xp_value, is_required)
SELECT
    u_state.id, 1, 'state_begeisterung',
    'Begeisterung (1-5)',
    'Wie stark war deine Begeisterung während der Incantations?',
    'scale_1_5',
    '{"min":1,"max":5}'::jsonb,
    50,
    FALSE
FROM u_state;

-- 3) Unit "RITUAL" (Incantation-Sätze)
WITH u_ritual AS (
    INSERT INTO program_unit (program_id, position, title, description, xp_base, is_optional)
    VALUES (
        (SELECT id FROM program WHERE code = 'MM1'),
        3,
        'RITUAL',
        'Incantation-Sätze 5x wiederholen.',
        0,
        FALSE
    )
    RETURNING id
)
INSERT INTO program_exercise (program_unit_id, position, key, label, help_text, input_type, config, xp_value, is_required)
SELECT
    u_ritual.id, 1, 'incantation_family',
    'Ich bin ein liebevoller Mensch und kümmere mich gut um meine Familie und Freunde.',
    '5x Wiederholen',
    'checkbox',
    NULL,
    100,
    FALSE
FROM u_ritual;

-- 4) Unit "QUALITY / RESULT"
WITH u_result AS (
    INSERT INTO program_unit (program_id, position, title, description, xp_base, is_optional)
    VALUES (
        (SELECT id FROM program WHERE code = 'MM1'),
        4,
        'QUALITY / RESULT',
        'Qualität und Ergebnis der Session (Fokus >= 70%, alle Sätze erledigt?).',
        0,
        FALSE
    )
    RETURNING id
)
INSERT INTO program_exercise (program_unit_id, position, key, label, help_text, input_type, config, xp_value, is_required)
SELECT
    u_result.id, 1, 'focus_70_percent',
    'Fokus bei mindestens 70%?',
    NULL,
    'checkbox',
    NULL,
    300,
    TRUE
FROM u_result;
```

> Hinweis: Du kannst dieses Muster für andere Programme (STATE, RULES, DAY-Checklists, BODY/HUMAN/ENV/BIZ-Programme) wiederholen.

---

Wenn du möchtest, kann ich dir im nächsten Schritt direkt:

* ein Beispiel-`docker-compose.yml` für Next.js + Postgres,
* sowie eine grobe Next.js API-Struktur (Ordnerstruktur, beispielhafte Routen für Programme/XPs/Journals) skizzieren.

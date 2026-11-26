# Boku no Natsuyasumi (PS1) — Master-Plan: Deutsch-Patch (`boku-ps1-de`)

Willkommen im stufenweisen Agenten-Ausführungsplan für die **deutsche Übersetzung** von *Boku no Natsuyasumi* (PlayStation 1, `SCPS-10088`), aufbauend auf der Open-Source-Toolchain und Vorarbeit des englischen Patches.

---

## 1. Projekt-Kurzüberblick & Ausgangslage

| Bereich | Befund aus der Projektanalyse |
|---|---|
| **Basis-ROM (`rom/`)** | Verifiziert! `Boku no Natsuyasumi - Summer Holiday 20th Century (Japan).bin` hat den exakten Redump-SHA-1 (`5959bf7d9835d0a60aeb0143e2d0fc564bfea9fa`). |
| **Technisches Fundament** | Komplette Python-Pipeline (`boku/`), VWF-Renderer-Patches (`asm/`, MIPS/armips), automatische Container-Relocation, programmatischer Textur-Typesetter (`GameFace`, `Bean`, `Sprout`) und Sektor-EDC/ECC-Generator sind **fertig vorhanden**. |
| **Gesamtumfang Text** | **3.538 Einträge** verteilt auf 42 Textdateien (keine Binärdateien von Hand nötig!). |
| **Zeichensatz / Umlaute** | **ASCII-Umschrift (`ae`, `oe`, `ue`, `Ae`, `Oe`, `Ue`, `ss`)** — z. B. *Räume → Raeume*, *Größe → Groesse*, *Käfer → Kaefer*. Dadurch funktionieren alle **3 Schriftsysteme** (Dialog-VWF, Mini-Pixelfonts `Bean`/`Sprout` auf Buttons/Büchern und PS1-BIOS-Memory-Card Shift-JIS) sofort ohne Font-Neubau! |
| **Übersetzungs-Strategie** | **Dual-Source KI-Übersetzung**: Die KI erhält gleichzeitig das **japanische Originalskript** (aus `disc/script/`) **UND** die **geprüfte englische Vorlage inkl. Kontext-Notizen (`# NOTE`), Story-Bibel & Glossar**. So vermeiden wir „Stille-Post-Fehler" und behalten alle Wortspiele & Charakterstimmen. |

---

## 2. Inhaltsverzeichnis der Stufenpläne (`/plan`)

Jede Stufe ist als eigenständiges Arbeitspaket für KI-Agenten konzipiert und hat klare **Voraussetzungen**, **Aufgaben**, **Abnahmekriterien (Gates)** und **Fortschritts-Berichtspflichten**:

| Stufe | Datei | Titel & Fokus | Umfang / Ziel | Status |
|---|---|---|---|---|
| **Analyse** | [progress/00-projektanalyse.md](progress/00-projektanalyse.md) | **Initiale Projekt- & Machbarkeitsanalyse** | Architektur, Zahlen, technische Fallen & Lösungen | `[x] Abgeschlossen` |
| **Stufe 1** | [01-umgebung-und-import.md](01-umgebung-und-import.md) | **Windows-Umgebung, Tooling & Disc-Import** | `uv`, `armips`, `xdelta3`, `boku import` + `extract`, erster Test-Build | `[x] Abgeschlossen` |
| **Stufe 2** | [02-deutsche-stilbibel-glossar.md](02-deutsche-stilbibel-glossar.md) | **Deutsche Stilbibel, Anrede-Regeln & Glossar** | Du/Sie-System, Japanismen, Charakterstimmen, 60 Insektennamen, `ae/oe/ue/ss`-Regelwerk | `[x] Abgeschlossen` |
| **Stufe 3** | [03-engine-und-pipeline-anpassung.md](03-engine-und-pipeline-anpassung.md) | **Engine-, Linter- & Pipeline-Anpassung für Deutsch** | Deutsche `SPEAKER_LABELS`, `Ja \| Nein` 6-Zellen-Fix (`TITLE.OVL`), `locked.tsv`-Reset, Umlaut-Linter | `[x] Abgeschlossen` |
| **Stufe 4** | [04-ui-menues-und-arrays.md](04-ui-menues-und-arrays.md) | **UI, Menüs, Items & Insektenbuch (`arrays.txt`)** | 314 Einträge: Memory Card, Optionen, Items, Fische, Drachen, Sumo-Moves, Code-Labels | `[x] Abgeschlossen` |
| **Stufe 5** | [05-texturen-und-tagebuch.md](05-texturen-und-tagebuch.md) | **Programmatische Texturen & Bildertagebuch** | 300 Einträge in `translation/textures/`: Titelmenü, Buttons, Schilder, Lexika, 93 Tagebuchseiten | `[x] Abgeschlossen` |
| **Stufe 6** | [06-hauptskript-31-tage.md](06-hauptskript-31-tage.md) | **Hauptskript: Haus-Events & Alle 31 Sommertage** | 2.801 Einträge (`shared.txt` + `day01.txt`–`day31.txt`) in 6 kontrollierten Batches | `[x] Abgeschlossen` |
| **Stufe 7** | [07-videos-und-sprachclips.md](07-videos-und-sprachclips.md) | **FMV-Untertitel, Titelsong & Epiloge** | 89 zeitgesteuerte Einträge (`movies.txt` & `clips.txt`) inkl. Lesegeschwindigkeits-Prüfung | `[x] Abgeschlossen` |
| **Stufe 8** | [08-qa-build-und-deutsch-patch.md](08-qa-build-und-deutsch-patch.md) | **Gesamt-QA, Emulator-Tests & Deutsch-Patch-Release** | 0 Lint-Fehler, Mockup-Check, HTML-Reader-Review, Emulator-Test & `.xdelta`/`.ppf`-Erstellung | `[x] Abgeschlossen` |

---

## 3. Pflicht-Workflow für ausführende KI-Agenten

Jeder Agent, der an diesem Projekt arbeitet, **muss** sich an folgende goldene Regeln halten:

1. **Vor Beginn lesen:**
   - Lies immer zuerst diese Datei (`plan/README.md`), den **letzten Bericht** in [`plan/progress/`](progress/README.md) und die **Detaildatei der aktuellen Stufe**.
2. **Urheberrechts-Trennung strikt wahren (aus `CLAUDE.md`):**
   - Niemals Original-Bytes, extrahierte Spieldateien, japanische Originaltexte oder gerippte Texturen außerhalb von `disc/`, `work/` und `build/` ablegen. In `translation/` steht ausschließlich deutscher (bzw. vor Übersetzung englischer) Text + englische/deutsche Notizen ohne japanische Schriftzeichen (`test_translation_has_no_japanese.py`).
3. **ASCII-Umlaut-Konvention (`ae`, `oe`, `ue`, `ss`) strikt einhalten:**
   - `ä → ae`, `ö → oe`, `ü → ue`, `Ä → Ae`, `Ö → Oe`, `Ü → Ue`, `ß → ss` (Beispiel: *Räume → Raeume*, *schön → schoen*, *für → fuer*, *Straße → Strasse*, *groß → gross*).
   - Keine deutschen typografischen Anführungszeichen (`„..."`), sondern gerade Anführungszeichen (`"..."`) nur für Begriffe innerhalb eines Satzes — gesprochene Dialogzeilen bekommen **gar keine** äußeren Anführungszeichen (der Renderer setzt `Sprecher「...」` automatisch!).
4. **Nichts kürzen, um Platz zu sparen ("Nothing is cut to fit"):**
   - Dialogboxen haben 3 Zeilen im breiten Band unter der Szene; überlange Container werden vom Build-System automatisch verschoben (`relocate.py` / `array_relocate.py`).
   - Wenn eine Zeile den Pixel-Lint (`uv run boku lint`) reißt, wird bei unvertonten Zeilen ein Seitenumbruch (` // `) ergänzt oder bei festen UI-Boxen präzise, natürlich-deutsche Wortwahl gewählt — niemals sinnentstellend gekürzt.
5. **Nach jedem großen Step: Fortschrittsbericht schreiben!**
   - Nach Abschluss einer Stufe (und bei Stufe 6 nach jedem Tages-Batch) **muss** ein Bericht unter [`plan/progress/`](progress/README.md) angelegt und die Status-Tabelle oben in `plan/README.md` aktualisiert werden.

---

## 4. Übersicht des Übersetzungsvolumens nach Dateien

```
translation/
├── days/
│   ├── arrays.txt        (  314 Einträge — Menüs, Items, Insekten, Code-Labels, Save-Titel)
│   ├── shared.txt        (  750 Einträge — Tagesunabhängige Haus-/Untersuchungs-Events)
│   └── day01..day31.txt  (2.085 Einträge — Alle Story- & Tages-Events vom 1. bis 31. August)
├── textures/
│   ├── ui.txt            (   18 Einträge — Titelbildschirm, Optionen, Erinnerungen, Credits-Card)
│   ├── buttons.txt       (   52 Einträge — Stein-Buttons, Sprechblasen, Stempelkarte, Käfig)
│   ├── signs.txt         (   10 Einträge — Strandschild, Saoris Brief, Türschild, Jagdschild)
│   ├── records.txt       (   13 Einträge — Angel-Rekorde & Käfertausch-Karte)
│   ├── sumo.txt          (   42 Einträge — Käfer-Sumo-HUD, Ränge, Sieges-Techniken & Glossen)
│   ├── kite.txt          (    3 Einträge — Drachenflug-HUD: Wind, Tempo, Höhe)
│   ├── books.txt         (   69 Einträge — Insekten-Enzyklopädie & Drachen-Lexikon)
│   └── diary.txt         (   93 Einträge — Bokus Bildertagebuch-Seiten NIKKI_001..099)
├── clips.txt             (   46 Einträge — Käfer-Sumo-Stimmen, Nacht 1 & 5 Epiloge mit Timings)
└── movies.txt            (   43 Einträge — Intro/Outro-FMVs, Zwischensequenzen & Titelsong)
────────────────────────────────────────────────────────────────────────────────────────────
GESAMT:                    3.538 Einträge
```

# Fortschrittsbericht — Stufe 5: Programmatische Texturen & Bildertagebuch (`translation/textures/`)

- **Datum:** 2026-11-26
- **Status:** Abgeschlossen
- **Bearbeitete Dateien:**
  - `translation/textures/ui.txt` (18 Einträge)
  - `translation/textures/buttons.txt` (52 Einträge)
  - `translation/textures/signs.txt` (10 Einträge)
  - `translation/textures/records.txt` (13 Einträge)
  - `translation/textures/kite.txt` (3 Einträge)
  - `translation/textures/sumo.txt` (42 Einträge)
  - `translation/textures/books.txt` (69 Einträge)
  - `translation/textures/diary.txt` (93 Einträge)
  - `translation/status.tsv` (`screens`, `sumo`, `kite`, `diary`, `books` auf `reviewed`, `2026-11-26`)
  - `work/textures-de/` (148 neu gerenderte PNGs über CLUT 0)
  - `plan/progress/05-texturen-und-tagebuch.md`, `plan/progress/README.md`, `plan/README.md`

---

## 1. Was wurde gemacht?

- **Block A — UI, Buttons, HUD & Schilder (138 Einträge):**
  - `ui.txt`: Titelmenü (`Neues Spiel`, `Weiter`, `Sommeralbum`, `Optionen`), Konfigurationsmenü (`Menue`, `Stimme + Text`, `Abbruch OK`, `Nur Stimme`, `Kein Abbruch`, `Stereo`, `Mono`, `Aktion`, `Abbruch`, `Rennen`, `Unter- // menue`), Album (`Sommer- // Erinnerungen`) und Epilog-Credits (`Produktion und Copyright`).
  - `buttons.txt`: Alle 13 `33x13`/`36x13`-Stein-Buttons + `SUB.back` auf `Ende` vereinheitlicht; Schreibtisch-/Taschen-/Sumo-/Insektenkasten-Sprechblasen (`Zeug`, `Flug`, `Angel`, `Box`, `Leer`, `Netz`, `Deal`, `Rein`, `Rang`, `Fach`, `Raus`, `Zur.`, `Vor`, `Frei- // lassen`, `Lupe // Detail`, `Arten- // liste`, `Angel- // zeug`), Stempelkarte (`Radio- // Gymnastik // Stempelkarte`, `Einen gesunden Sommer!`) und Käfig-Stern (`Wow!`).
  - `signs.txt`: Strandschild (`Flut!`, `Badeverbot`), Saoris Abschiedsbrief (`Leb wohl. // Du warst // ein echt guter // Kerl.` + `Deine Saori`), Türschild (`Zutritt // verboten!`), Tauschheft (`Sumo // Tausch- // Heft`) und Jagdwarnschild (`GEFAHR!`, `Haeuser nah,`, `Schussgefahr!`, `Praefektur // Jagdbund`).
  - `records.txt` & `kite.txt`: Angel-/Sumo-Rekorde (`St.`, `Groesse`, `Schnitt`, `Rekord`, `Koeder (Wurm)`, `Tenkara (Klein)`, `Tenkara (Gross)`, `Fang 8/`, `S`, `N`, `So viel wert wie`, `Saege-Kaefer`) und Drachen-HUD (`Wind`, `Fahrt`, `Hoehe`).
  - `sumo.txt`: `Energie`, `Leicht`/`Stark`/`King`, `Siegeszug`, alle 22 Zugnamen (synchron zu `arrays.txt`) und alle 15 deutschen Kurz-Glossen (`<= 122 px`).
- **Block B — Insekten- & Drachen-Lexikon (`books.txt`, 69 Einträge):**
  - Alle 9 Insekten-Doppelseiten (`mzkan@0`–`8`, exakte Artnamen aus dem Glossar) und 8 Drachen-Doppelseiten (`tzkan@0`–`7`, exakte Drachennamen + `Anfaenger`/`Mittelstufe`/`Fortgeschritten`/`Meister`/`Stufe ?`) vollständig ins Deutsche übertragen.
- **Block C — Bokus Bildertagebuch (`diary.txt`, 93 Einträge):**
  - `nikki@NIKKI_001` bis `nikki@NIKKI_100` in kurzen, kindlichen Drittklässler-Sätzen (`ae/oe/ue/ss`, ohne `"` und `( )`) auf max. 5 linierte Zeilen in `GameFace` gesetzt.
- **Visuelle Stichproben (`work/textures-de/`):**
  - `_DATA_T_TITLE.BIN__000014.png`, `_DATA_MZKAN0.BIN__00004c.png`, `_DATA_M_FILES.BIN_M_I14000.BIN__000214.png`, `_DATA_M_FILES.BIN_M_I23000.BIN__000354.png` und `_DATA_NIKKI.BIN_NIKKI_001__000000.png` visuell geprüft — alle Texte sitzen sauber ohne Überlappung oder Abschneiden.

---

## 2. Wichtige Entscheidungen & Gelöste Probleme

1. **Pixelgrenzen auf UI-Tafeln & Schildern:**
   - `T_TITLE.2`: `Sommeralbum` (passt in `128x16 px`, statt `Sommer-Erinnerungen` mit `133 px`).
   - `M_C15.1`: `Badeverbot` (passt in `155 px` sichtbare Breite bei 2×).
   - `M_I18.0`: `Zutritt // verboten!` (passt in `112x72 px`).
   - `M_S01000.0`: `Sumo // Tausch- // Heft` (passt in `70 px` bei 2× in Zeile 1).
   - `M_I23000`: `Schussgefahr!` und `Praefektur // Jagdbund` umgehen Einschusslöcher und Zeichnung sauber.
2. **Stein-Buttons (`33x13 px`) & `Bean`-Button-Regel (`test_real_texture_buttons.py`):**
   - `Zurueck` (`49 px`) passt auf keinen der `33x13`-Steinbuttons → einheitlich `Ende` verwendet.
   - `MZ02.release` (`Frei- // lassen`), `MZ02.magnifier` (`Lupe // Detail`), `SAMP.species_list` (`Arten- // liste`) und `FS_WAL.tackle` (`Angel- // zeug`) so formuliert, dass sie planmäßig die `Bean`-Schrift benötigen (`test_a_button_is_set_small_only_where_the_games_glyphs_do_not_fit` grün).
3. **`books.txt` (`Bean` 108/110 px):**
   - `Ritterfalter-Familie` statt `Schwalbenschwanz-Familie` (`111 px > 108 px`).
   - `Rechteckdrachen mit Mittelspannung` statt `Mittelspann-Rechteckdrachen` (`127 px > 110 px`, da `Bean` nur an Leerzeichen umbricht).

---

## 3. Qualitäts- & Test-Nachweis (Gates)

- **`uv run boku textures check --out work/textures-de`:** Exit 0 — **`16 families built` (`259312 byte edits`, `148 rebuilt image(s)`), 0 Zurückweisungen**.
- **`uv run ruff check .`:** Exit 0 (`All checks passed!`).
- **`uv run pytest -q` (Vollständige Suite):** Exit 0 — **`1940 passed, 148 skipped in 527.57s (0:08:47)`**, **0 failures, 0 errors**.

---

## 4. Übergabe an den nächsten Agenten / Offene Punkte

- **Stufe 6 (`plan/06-hauptskript-31-tage.md`) ist bereit:**
  - Alle 314 Einträge in `arrays.txt` und alle 300 Einträge in `textures/*.txt` sind auf Deutsch festgezogen und verifiziert.
  - Als Nächstes folgen die 2.835 Dialog- und Ereigniszeilen in `translation/days/shared.txt` und `day01.txt`–`day31.txt` in den 6 kontrollierten Batches (6a–6f).

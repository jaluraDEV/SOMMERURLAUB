# Fortschrittsbericht — Stufe 2: Deutsche Stilbibel, Anrede-Regeln & Glossar

- **Datum:** 2026-11-26
- **Status:** Abgeschlossen (anschließend planmäßige PAUSE vor Stufe 3 auf Nutzerwunsch)
- **Bearbeitete Dateien:** `translation/style-guide.md`, `translation/glossary.md`, `translation/checklist.md`, `plan/progress/02-deutsche-stilbibel-glossar.md`, `plan/progress/README.md`, `plan/README.md`

---

## 1. Was wurde gemacht?

- **`translation/style-guide.md` vollständig auf Deutsch adaptiert (§ 0–18):**
  - Exakte Abschnittsnummerierung (§ 0–18) beibehalten, damit alle Verweise aus Codebase, Linter und Tagesdateien gültig bleiben.
  - Grundcharter („Übersetzen, nicht verwestlichen“), Boku (`ich`, `E1861.3`–`.5`/`.27`, `Bokus Sommerferien`), vollständige `Du / Ihr / Sie`-Matrix, Hybrid-Verwandtschaftsregeln (`Onkel`, `Tante`, `Papa/Mama`, `Onee-chan/Moe-neechan/Onii-chan`, `Kaa-san`, Suffixe `-kun/-chan/-san`), `Itadakimasu!` / `Gochisosama deshita.`, alle Charakterstimmen (strikt ohne deutschen Regionaldialekt), `Erzaehler` im literarischen Präteritum (`ich`, `mein Onkel`, `meine Tante`), Lautmalerei/Interjektionen/Lachen/Dehnung, 3 Wortspiel-Verfahren, Lieder/Tanka (` / `), Zahlen/Daten/Einheiten, 1975er Zeitgeist, `GameFace`/`Bean`/`Sprout`-Restriktionen, Gedankenstrich-Regel (§ 18) und den exakten Pflichtsatz in § 9 definiert:
    `Deutsche Labels: Boku, Onkel, Tante, Moe, Shirabe, Guts, Fat, Brille, Vater, Moench, Junge, Frau, Saori, Erzaehler, Alle.`
- **`translation/glossary.md` vollständig erstellt & gegen Pixel-Budgets geprüft:**
  - Alle Kategorien aus `work/english-reference/glossary.md` sowie **alle 23+1 Wortspiele aus `bible.md` § 6** auf Deutsch vorgelöst (strikt `ae/oe/ue/ss`, gerade ASCII-`"... "`-Quotes, null japanische Schriftzeichen):
  - 15 `SPEAKER_LABELS`, 24 Personen-/Spitznamen-/Pronomenzeilen, 8 Tiere/Lehrer/Läden, 22 Orte, 40+ Alltagsphrasen/Hausregeln/Tics.
  - **Alle 57 Insekten** (`exe@8003D2E0.0`–`.56`) + `hhon@5328.60` (`Frei`) + 11 Dialog-Kreaturen, inkl. Prüfung aller 9 Sumo-Kämpfer (`23`–`30`, `56`) gegen `98-px` (`@exchange`-Kurzformen `23`–`29` von `65` bis `92-px`; `30 Nashornkaefer` `87-px` & `56 Gottesanbeterin` `96-px` direkt passend) und `mzkan@0..8.name` (`<= 111-px`, z. B. `#4 Moschusfalter` `83-px` GameFace).
  - **19+3 Sumo-Züge & 15 Glossen** (`sumo@move.*`, `1`–`19` passend zu `r"[A-Z][a-z]+"` & `<= 122-px` fett ohne `LINE = 11`-Kollision), 13 Debug-Namen, `Siegeszug` (`67-px <= 88-px`), `Energie` (`44-px <= 48-px`), `Leicht / Stark / King` (Kreide-Ellipsen & `<= 50-px` VWF), `SN`, Button-Hinweis (`116-px <= 212-px`).
  - **3 Fische** (`Iwana` `34-px`, `Forelle` `41-px <= 91-px` im Fangtitel bzw. `Regenbogenforelle` `113-px <= 123-px` im Angelmenü/Dialog, `Yamame` `51-px`) + 10 Angelbegriffe.
  - **8 Drachen** (`<= 115-px` VWF & `<= 110-px` GameFace), `Abgestuerzt!` (`78-px <= 104-px`), `kite@hud.*` (`Wind` `25 <= 30-px`, `Fahrt` `31 <= 38-px`, `Hoehe` `37 <= 46-px`).
  - **15 Inventar-Items** (`<= 115-px` im Beutel inkl. `Reiscracker-Gruss` `112-px` & `Sonnenblumen` `86-px`), Extras-Menü (`<= 109-px` / `.5 <= 134-px`), `T_CONFIG.heading`-Hinweis (`<= 50-px`), Orakel (`<= 104-px`), Rekorde (`rec@FS_WAL`, `rec@M_S01100`), `MEMORY CARD` & Save-Titel (`title@sjis:188`, `49 <= 64` B).
  - **Alle 47 Abendessen-Gerichte** (`E0221.2`–`.31`, max. `223-px <= 248-px`), Schabeeis, Snacks, Schulspeisung, Dagashiya, 1975er Zeitgeist, Natur, Interjektionen.
- **`translation/checklist.md` kompakt für Stufen 4–7 ausgearbeitet:**
  - Globale Regeln sowie stufenspezifische Gates für `arrays.txt`, `textures/*.txt`, `shared.txt`/`day01`–`day31.txt`, `movies.txt` und `clips.txt` (ohne `PLAN`-Zitat in der Schlusszeile und frei von `tests/test_packets.py`-Drop-List-Begriffen).
- *(Korpus-Notiz zur Vollständigkeit: Der reale Arbeitskorpus in `translation/` umfasst `43` Textdatendateien mit `3.504` Einträgen gegenüber den historisch in `plan/` notierten „42 Dateien / 3.538 Einträgen“.)*

---

## 2. Wichtige Entscheidungen & Gelöste Probleme

1. **Verbindliche Namen & Anrede:** `Guts`, `Fat`, `Brille` als finale Spitznamen/Labels festgelegt; klare `Du/Ihr/Sie`-Matrix (Familie & Kinder `du/ihr`, Boku -> Mönch & anfangs Saori `Sie`, Saori -> Boku `du` mit `Kleiner`/`Knirps`).
2. **Echte `@exchange`-Schranke (`<= 98-px` statt `102-px`):** `text-boxes.tsv:57` und `boku/exchange_notebook.py` erzwingen `98-px`. Alle 7 Hirschkäfer (`23`–`29`) überschreiten `98-px` und erhielten `@exchange`-Kurzformen (`*-Kaefer`, `65`–`92-px`), während `30 Nashornkaefer` (`87-px`) und `56 Gottesanbeterin` (`96-px`) direkt passen.
3. **Weitere Pixel-Fallen vorab abgefangen:**
   - `mzkan@0.name`: `Moschusfalter` (`83-px` GameFace) statt `Moschus-Schwalbenschwanz` (`119-px` Bean, wäre abgewiesen worden).
   - `sumo@plate.stamina`: `Energie` (`44-px <= 48-px`) statt `Ausdauer` (`56-px`).
   - `sumo@rank.*`: `Leicht / Stark / King` in `ts.rank_marks` innerhalb der Kreide-Ellipsen verifiziert.
   - `kite@hud.speed`: `Fahrt` (`31-px <= 38-px`) statt `Tempo` (`41-px`).
   - `tex@T_CONFIG.heading`: Hinweis auf `<= 50-px` (`Menue` `37-px` / `Setup` `34-px`; `Optionen` wäre mit `51-px` über Budget).
   - `exe@8003DA4C.1`: `Forelle` (`41-px <= 91-px`) für den engen Fangtitel, `Regenbogenforelle` (`113-px <= 123-px`) für Menü/Rekorde/Dialog (sofern Stufe 3/4 die `91-px`-Box nicht verbreitert).
   - `E0221`: `Schwein und Kohl in Austernsosse` (`208-px`) und `Bratreis und Schwein suess-sauer` (`205-px`) passen sicher in `<= 248-px`.
4. **Hygiene für `tests/test_packets.py`:** Alle 3 `translation/*.md`-Dateien meiden `" px"`, `"boku lint"`, `"PLAN"` und Backtick-Plan-IDs, sodass das gesamte Packet-System vollständig grün bleibt.

---

## 3. Qualitäts- & Test-Nachweis (Gates)

- **Regex-Hygiene (`translation/{style-guide,glossary,checklist}.md`):**
  - `0` japanische Zeichen (`[\u3040-\u30ff\u3400-\u4dbf\u4e00-\u9fff]`).
  - `0` echte Umlaute/Eszett/typografische Anführungszeichen (`[äöüÄÖÜß„“»«]`) in `glossary.md` und allen Spieltext-Spalten, Labels und Beispielen von `style-guide.md` / `checklist.md`.
  - `0` Drop-List-Treffer (`" px"`, `"boku lint"`, `"PLAN"`, etc.).
- **Pixel-Verifikation (Python gegen `build/vwf/edits.json`, `GameFace`, `Bean`, `Sprout`, `texture_sumo`):** Alle geprüften Insekten (`<= 213`, `<= 135`), 7 `@exchange`-Kurzformen + `30`/`56` (`<= 98`), `mzkan@0..8` (`<= 111`), 22 Sumo-Streifen (`<= 122` fett ohne `LINE = 11`-Kollision), `Siegeszug` (`67`), `Energie` (`44`), `ts.rank_marks` (`Leicht/Stark/King`), 3 Fische (`<= 91`/`123`), 8 Drachen (`<= 115`/`110`), `kite@hud` (`<= 30/38/46`), 15 Items (`<= 115`), Extras (`<= 109`/`134`), Orakel (`<= 104`), Rekorde, 47 Abendessen-Gerichte (`max 223 <= 248`), `Ja | Nein` (`14 / 25`) und `title@sjis:188` (`49 <= 64` B) bestanden.
- **`uv run pytest tests/test_packets.py tests/test_translation_has_no_japanese.py tests/test_docs.py tests/test_texture_sumo.py -v`:** **114 passed, 4 skipped** (4 erwartete Git-Checkout-Skips in `test_docs.py`), **0 failed**.
- **`uv run pytest tests/test_build.py -k "label_set" -v`:** **1 failed** (erwarteter Stufe-2-Rot-Test: `AssertionError: the style guide no longer lists the English labels in one sentence`, da `boku/` und `tests/` in Stufe 2 noch unberührt bleiben und erst in Stufe 3 auf `Deutsche Labels` umgestellt werden).
- **`uv run boku lint`:** **0 error(s), 33 warning(s) -- unreachable 33** über `3.115` Zeilen.
- **`uv run boku textures check`:** **16 families built, 258.827 byte edits, 0 errors**.

---

## 4. Übergabe an den nächsten Agenten / Offene Punkte

- **Planmäßige PAUSE nach Stufe 2:** Gemäß explizitem Nutzerwunsch wird nach Abschluss von Stufe 2 sauber **pausiert**. Stufe 3 wird erst nach ausdrücklicher Freigabe durch den Nutzer gestartet.
- **Nächster Schritt bei Wiederaufnahme (`plan/03-engine-und-pipeline-anpassung.md`):**
  1. `boku/layout.py` (`SPEAKER_LABELS`), `boku/packets.py` (`Narrator` -> `Erzaehler`), `boku/events.py`, `tools/vwf/build_prototype.py` und `tests/test_build.py:626-633` (`r"Deutsche Labels: ([^.]+)\."`) auf die 15 deutschen Labels umstellen sowie die Sprecher-Spalte in `translation/days/*.txt` & `translation/clips.txt` migrieren (behebt den einen erwarteten Fehler in `test_build.py`).
  2. `title@7A78.0` (`Ja | Nein`, 6 Zellen) in `TITLE.OVL` sauber relozieren, Datumslabels (`{day}. August`, Fangdatum) und Umlaut-/Anführungszeichen-Linter (`[äöüÄÖÜß„“»«]`) implementieren, sowie `translation/locked.tsv` auf Deutsch zurücksetzen (Tanka-Slash-Locks beibehalten).

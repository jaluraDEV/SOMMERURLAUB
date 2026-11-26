# Fortschrittsbericht — Stufe 3: Engine-, Linter- & Pipeline-Anpassung für Deutsch

- **Datum:** 2026-11-26
- **Status:** Abgeschlossen
- **Bearbeitete Dateien:**
  - `boku/layout.py`, `boku/arrays.py`, `boku/build.py`, `boku/lint.py`, `boku/code_text.py`, `boku/packets.py`, `boku/texture_text.py`
  - `asm/labels.asm`, `tools/vwf/build_prototype.py`
  - `translation/days/README.md`, `translation/locked.tsv`, `translation/days/*.txt` (33 Dateien, Sprecher-Spalte; `arrays.txt` `exe@code:80037544` auf Platzhalter `Caught {day}.{month}.`), `translation/clips.txt` (Sprecher-Spalte)
  - `tests/test_build.py`, `tests/test_lint.py`, `tests/test_layout.py`, `tests/test_array_relocate.py`, `tests/test_packets.py`, `tests/test_code_text.py`, `tests/test_real_date_labels.py`, `tests/test_real_walkers.py`, `tests/test_texture_text.py`, `tests/test_translation.py`, `tests/test_reader.py`, `tests/test_clip_subs.py`, `tests/test_coverage.py`
  - `build/vwf/edits.json`, `build/days/` (neu gebaut)
  - `plan/progress/03-engine-und-pipeline-anpassung.md`, `plan/progress/README.md`, `plan/README.md`

---

## 1. Was wurde gemacht?

- **Deutsche `SPEAKER_LABELS` & Sprecher-Migration:**
  - `SPEAKER_LABELS` in `boku/layout.py` auf alle 15 deutschen Labels aus `translation/style-guide.md` § 9 umgestellt (`Boku`, `Onkel`, `Tante`, `Moe`, `Shirabe`, `Guts`, `Fat`, `Brille`, `Vater`, `Moench`, `Junge`, `Frau`, `Saori`, `Erzaehler`, `Alle`).
  - `japanese_speaker()` und `system_part()` in `boku/packets.py` (`"Narrator"` -> `"Erzaehler"`, deutsche Packet-Hinweise), `UNLABELLED` in `tools/vwf/build_prototype.py` (`("Erzaehler", "(unlabelled)")`) sowie die Formatbeispiele in `translation/days/README.md` aktualisiert.
  - Sprecher-Spalte (inkl. Chöre mit `", "`) in **34 Dateien** (`translation/days/*.txt` inkl. `arrays.txt` + `translation/clips.txt`) über exakt **933 Zeilen** migriert (`Uncle->Onkel`, `Aunt->Tante`, `Specs->Brille`, `Father->Vater`, `Monk->Moench`, `Boy->Junge`, `Woman->Frau`, `Narrator->Erzaehler`).
- **6-Zellen-Relokation für `title@7A78.0` (`Ja | Nein` in `TITLE.OVL`):**
  - `RELOCATABLE_ARRAYS = frozenset({"title@7A78"})` in `boku/arrays.py` ergänzt und `relocatable(array)` erweitert (ohne `"R"` in `RELOCATABLE_SHAPES` aufzunehmen, damit die 4 Banner-`"R"`-Arrays nicht kollidieren).
  - `lay_out_answer_pair()` in `boku/layout.py` um `size: int | None = None` erweitert: Zell-Limit nur bei festem `size`, Ausgabe-`words` auf `max(cells, len(words))` gepolstert.
  - `boku/build.py` und `boku/lint.py` übergeben `byte_limit(...)` als `size`; `boku/lint.py` übergibt bei fehlerfreiem `lay_out_answer_pair` `context.array_words[row.line_id] = laid.words` an `array_room`.
  - Mit Unit-Tests (`tests/test_layout.py`, `tests/test_array_relocate.py`, `tests/test_lint.py`) und MIPS-Emulator-Test (`tests/test_real_walkers.py`) verifiziert: 6-Zellen-`"Ja | Nein"` reloziert sauber in `TITLE.OVL`s Tail (`>= 0x800820EC`), schreibt `0x8007CFF8`/`0x8007D000` um und patcht `SPLIT=1`, `COUNT=6`.
- **Deutsche Datums-Labels (`title@code:8007BB60` & `exe@code:80037544`):**
  - `DATE_LABELS` in `boku/code_text.py` auf `"{day}. August"` (`vwf_save_date_label`) und `DateLabel("vwf_caught_label", ("{day}", "{month}"), "Fang {day}.{month}.")` umgestellt.
  - In `asm/labels.asm` (`vwf_caught_label`) `{month}` (`8`) und `{day}` (`s3`) im Mess- und Zeichenblock sowie bei den beiden `NUMBER_DRAW`-Aufrufen bei **0 Byte Nettowachstum** getauscht (`vwf_routines` endet weiterhin bei `0x8002585C`, 4 Bytes frei vor `0x80025860`).
  - Beide Formate (`"{day}. August"`, `"Fang {day}.{month}."`) sowie `Caught {day}.{month}.` über `tests/test_code_text.py` und MIPS-Ausführung auf dem neugebauten Image (`tests/test_real_date_labels.py`) verifiziert.
- **`translation/locked.tsv` zurückgesetzt:**
  - Alle 101 englischen Wort-Locks entfernt (`work/english-reference/locked.tsv` unverändert als Sicherung). Nur die 3 sprachneutralen Tanka-Slash-Locks (`E2515.0`, `E2515.4`, `E2712.0` -> `phrase`, ` / `) beibehalten, damit `tests/test_locked.py` und `tests/test_packets.py` grün bleiben.
- **Umlaut-/Anführungszeichen-Linter & deutsche `ADDITIVE_WORDS`:**
  - `FORBIDDEN_GERMAN` (`[äöüÄÖÜß]`), `FORBIDDEN_QUOTES` (`[„“»«]`) und `german_ascii_problems()` in `boku/lint.py` implementiert und für alle Tages-/Array-Zeilen, `translation/movies.txt` (`lint_movies`), `translation/clips.txt` (`lint_clip_file`), `boku/texture_text.py` (`ink_of()`) und `boku/packets.py` (`check_answer()`) aktiviert (Fehlermeldung enthält `"Umlaut gefunden — bitte ASCII-Umschrift ae/oe/ue/ss verwenden"` bzw. ASCII-Quote-Hinweis).
  - `ADDITIVE_WORDS` (12 deutsche ASCII-Füllwörter) und `SETTLED_PHRASES` (`"sehr wohl"`, `"meine wenigkeit"`) in `boku/lint.py` auf Deutsch umgestellt.

---

## 2. Wichtige Entscheidungen & Gelöste Probleme

1. **Platzhalter-Reihenfolge von `exe@code:80037544` in `translation/days/arrays.txt`:** Da `DATE_LABELS["exe@code:80037544"]` nun `("{day}", "{month}")` erwartet und `vwf_caught_label` in `asm/labels.asm` Tag vor Monat zeichnet, wurde der Platzhalter in `translation/days/arrays.txt` auf `Caught {day}.{month}.` aktualisiert (Inhaltsübersetzung `Caught` -> `Fang` folgt planmäßig in Stufe 4). So bleiben `boku lint`, `boku build` und `tests/test_real_date_labels.py` durchgehend konsistent und grün.
2. **Kein `"R"` in `RELOCATABLE_SHAPES`:** Stattdessen `RELOCATABLE_ARRAYS = frozenset({"title@7A78"})`, um Kollisionen mit den 4 Banner-`"R"`-Arrays in `boku/array_relocate.py` zu vermeiden.
3. **`vwf_caught_label` ohne Byte-Wachstum:** Da `vwf_routines` (`0x80025120..0x80025860`) nur 4 Bytes Reserve hat, wurden die `{day}`- und `{month}`-Blöcke exakt instruktionsgleich getauscht (`SPRITE_DIGIT + MONTH_GAP` nach beiden Zahlen für 1 px Abstand vor dem Punkt).

---

## 3. Qualitäts- & Test-Nachweis (Gates)

- **VWF- & Disc-Rebuild:**
  - `tools/vwf/build_prototype.py --edits-only --out build/vwf`: Exit 0 (`free from 0x8002585C`, 129 byte edits).
  - `boku build --vwf build/vwf/edits.json --translation translation/days --textures translation/textures --name days --out build/days --skip-unfitted`: Exit 0 (`2983 line(s) laid out, 0 refused, 33 left retail`).
- **`ruff check .`:** Exit 0 (`All checks passed!`).
- **`ruff format --check .`:** Exit 0 (`218 files already formatted`).
- **`boku lint`:** Exit 0 (`0 error(s), 190 warning(s) -- additive-word 1, unreachable 33, voice-note 156`; `voice-note`-Warnungen stammen planmäßig von den 156 englischen `# VOICE`-Notizen in `days/*.txt` vor Stufe 6).
- **`boku textures check`:** Exit 0 (`16 families built ... 258827 byte edits`).
- **`pytest -q` (Vollständige Suite):** Exit 0 — **`1940 passed, 148 skipped in 522.75s (0:08:42)`**, **0 failures, 0 errors** (Skips nur für optionale Emulator-Boots mit `BOKU_EMU_TESTS=1`, `chdman`, `.git`, `sips`, `ffmpeg`, `trial`, `sample.mcd`).

---

## 4. Übergabe an den nächsten Agenten / Offene Punkte

- **Stufe 4 (`plan/04-ui-menues-und-arrays.md`) ist bereit:**
  - `translation/days/arrays.txt` behält vorerst seinen englischen Inhalt (nur die Sprecher-Spalte `Uncle` -> `Onkel` und der Platzhalter `Caught {day}.{month}.` wurden angepasst).
  - In Stufe 4 werden alle 314 Einträge in `arrays.txt` ins Deutsche übersetzt — inklusive `title@7A78.0` -> `Ja | Nein`, `title@code:8007BB60` -> `{day}. August` und `exe@code:80037544` -> `Fang {day}.{month}.` — sowie `translation/textures/sumo.txt` (`sumo@move.1`–`.19`) bytegleich mit `musi@2C.13`–`.31` synchronisiert.
  - Die 156 `voice-note`-Warnungen auf englischen `# VOICE`-Notizen in `translation/days/*.txt` und `arrays.txt` verschwinden sukzessive mit deren Übersetzung in Stufe 4 bzw. Stufe 6.

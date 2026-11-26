# Stufe 3: Engine-, Linter- & Pipeline-Anpassung für Deutsch

**Ziel:** Die wenigen Stellen im Python-Code (`boku/`) und in den Tests (`tests/`), die aktuell hartcodierte englische Annahmen treffen, sauber auf den Deutsch-Patch umstellen — inklusive Lösung des **6-Zellen-Problems bei `Ja | Nein`** auf dem Memory-Card-Bildschirm und eines automatischen **Umlaut-Linters**.

---

## 1. Identifizierte Code-Stellen aus der Projektanalyse

Die Architektur von `boku-ps1` ist zu 98 % sprachunabhängig, aber unsere Code-Analyse hat **5 konkrete technische Stellen** gefunden, die wir anpassen müssen, bevor die Übersetzung startet:

### Stelle 1: `SPEAKER_LABELS` (`boku/layout.py` & `boku/packets.py` & `tests/test_build.py`)
- **Ist-Zustand:** `boku/layout.py` (Zeile 391) prüft jedes Sprecher-Feld gegen `SPEAKER_LABELS = frozenset({"Boku", "Uncle", "Aunt", ...})` und setzt das Label direkt vor `「` ins Spielbild (`Uncle「...」`). `tests/test_build.py` (Zeile 628) gleicht diese Menge gegen `translation/style-guide.md` § 9 ab. Außerdem nutzt `boku/packets.py` (`LABEL_OF` / `SPEAKER_NAMES`) die Zuordnung von internen Codes (`OJI`, `OBA`, `FATHER`, ...) zu den Sprecher-Namen beim Generieren von Paketen.
- **Anpassung:**
  - `SPEAKER_LABELS` in `boku/layout.py` auf die deutschen Labels aus `style-guide.md` § 9 umstellen (`Onkel`, `Tante`, `Vater`, `Moench`, `Junge`, `Frau`, `Brille`, `Erzaehler`, `Alle`, plus unveränderte Eigennamen `Boku`, `Moe`, `Shirabe`, `Saori`, `Guts`, `Fat`).
  - Mapping in `boku/packets.py` synchronisieren, damit `uv run boku packet` und `uv run boku save-event` die deutschen Sprecher-Namen erzeugen und akzeptieren.

### Stelle 2: Memory-Card `Ja | Nein` (`title@7A78.0` in `boku/layout.py` / `boku/array_relocate.py`)
- **Ist-Zustand (Kritischer Fund!):** Auf dem Speicherkarten-Bildschirm (`TITLE.OVL`) teilen sich die beiden Antworten in `title@7A78.0` die **5 Zellen** des japanischen Originals (`はい` = 2 + `いいえ` = 3 → 5 Glyphen). `"Yes | No"` hat `3 + 2 = 5` Buchstaben und passte exakt in-place!
- **Problem auf Deutsch:** `"Ja | Nein"` braucht `2 + 4 = 6` Buchstaben → `lay_out_answer_pair` in `boku/layout.py` (Zeile 785) lehnt 6 Zellen in einem 5-Zellen-Feld ab!
- **Saubere Engineering-Lösung (keine Kürzung zu `"Ja | Nee"`!):**
  - Prüfe in `TITLE.OVL` die Referenz auf `0x80079A08 + 0x7A78` (bzw. wie der Drawer `0x8007CF7C` die Basisadresse lädt, z. B. `lui` + `addiu`).
  - Reloziere das kurze 6-Wort-Array in den freien Resident-/Overlay-Platz von `TITLE.OVL` (genau wie `boku/array_relocate.py` gewachsene Arrays verschiebt) und passe die `COUNT`-Konstante an `0x8007D064` (`slti v0, v0, 6` statt `5`) sowie `SPLIT` an `0x8007D03C` (`addiu v0, zero, 1` für `"Ja"`, Index 0..1) an! Pixelbreite: `"Ja"` (~14 px in 60 px Raum) und `"Nein"` (~28 px) passen optisch locker!

### Stelle 3: `translation/locked.tsv` & `tests/test_locked.py`
- **Ist-Zustand:** `translation/locked.tsv` erzwingt ca. 80 spezifische englische Formulierungen von Jay (`"This is the Sorano house..."`, `"Take"`, `"specks of light"`). Jede Änderung dieser Zeilen auf Deutsch lässt `boku save-event` und `pytest` fehlschlagen.
- **Anpassung:**
  - `translation/locked.tsv` ist bereits in `work/english-reference/locked.tsv` gesichert.
  - Leere die englischen Wort-Locks in `translation/locked.tsv` bis auf die Header-Zeile (und trage dort im Verlauf ab Stufe 4 gezielt wichtige deutsche Festlegungen ein, z. B. den Schrägstrich ` / ` im Tanka `E2515.0`).
  - Passe ggf. `tests/test_locked.py` Zeile 80 an, falls ein Test hartcodiert erwartet, dass `M27` bestimmte englische Text-Eigenschaften hat (Zeile 80 prüft nur `len(movie) == 1 and "\n" in movie[0]`, das bleibt auch auf Deutsch wahr!).

### Stelle 4: Neuer Linter-Check für verbotene Sonderzeichen & vergessene Umlaute (`boku/lint.py`)
- **Warum:** Bei 3.538 KI-übersetzten Zeilen passiert es leicht, dass ein Agent versehentlich ein echtes `ä`, `ö`, `ü`, `ß` oder typografische deutsche Anführungszeichen `„` / `“` schreibt.
- **Anpassung:**
  - Zwar fängt `unencodable` in `boku/layout.py` bereits jedes Zeichen ab, das keine Zelle in der Font-Map hat (also auch `äöüß„“`), **aber** wir fügen in `boku/lint.py` (und für `textures check`) einen glasklaren Hinweis hinzu, der bei `[äöüÄÖÜß]` direkt sagt: *"Umlaut gefunden — bitte ASCII-Umschrift ae/oe/ue/ss verwenden"*.
  - Außerdem prüfen wir die englische `ADDITIVE_WORDS`-Warnliste in `boku/lint.py` (die nach englischen Füllwörtern wie `just`, `really`, `quite` sucht): Im Deutschen erzeugen alte `# VOICE`-Kommentare sonst `voice-note`-Warnungen. Wir passen das sauber an (alte englische `# VOICE`-Zeilen werden beim Übersetzen entfernt; optional deutsche Füllwort-Heuristik wie `eigentlich`, `wirklich`, `halt` nur als sanfte Info oder deaktiviert).

### Stelle 5: Datums-Labels in `asm/labels.asm` & `boku/code_text.py` prüfen
- **Zwei dynamische Datums-Drawer:**
  1. `exe@code:80037544` (`Caught {month}/{day}`): Zeichnet erst Text, dann Monat `8`, dann Mitteltext, dann Tag `1..31`, dann Endtext (rechtsbündig an `CAUGHT_RIGHT = 77`).
     - Auf Deutsch z. B.: `Gef. {day}.{month}.` — **Achtung:** `DATE_LABELS` in `boku/code_text.py` erwartet die Reihenfolge `("{month}", "{day}")`! Entweder schreiben wir `Gefangen {month}/{day}` bzw. `Fang: {month}/{day}` (passt ohne ASM-Änderung sofort in die `("{month}", "{day}")`-Reihenfolge und ist super kurz, damit es nicht in lange Käfernamen ragt!), **oder** wir tauschen in `asm/labels.asm` (`vwf_caught_label`) Tag und Monat für deutsches `{day}.{month}.`! Das prüfen und lösen wir hier in Stufe 3 sauber!
  2. `title@code:8007BB60` (`August {day}`): Nimmt `("{day}",)` mit Präfix + Tag + Suffix!
     - **Mega-Vorteil der bestehenden Architektur:** `vwf_save_date_label` in `asm/labels.asm` unterstützt **bereits Präfix UND Suffix** rund um `{day}`! Das heißt: **`{day}. August`** (Präfix leer, Tag, Suffix `". August"`) funktioniert wahrscheinlich schon mit minimaler Prüfung des Abstands (`DIGIT_END`) out-of-the-box! Das verifizieren wir per Unit-Test!

---

## 2. Arbeitsschritte für den Agenten

1. Aktualisiere `SPEAKER_LABELS` in `boku/layout.py`, `boku/packets.py` und synchronisiere mit `translation/style-guide.md` § 9. *(Achtung: Da die bestehenden englischen `day*.txt` noch `Uncle`, `Aunt` etc. haben, entweder in einem kleinen Migrationsskript die Sprecher-Spalte in `translation/days/*.txt` und `clips.txt` direkt auf die deutschen Sprecher-Namen umstellen, damit der Build & die Tests jederzeit grün bleiben!)*
2. Implementiere die 6-Zellen-Unterstützung für `title@7A78.0` (`Ja | Nein`) inklusive Unit-Test.
3. Prüfe und teste `{day}. August` für `title@code:8007BB60` und entscheide/implementiere das Datumsformat für `exe@code:80037544` (`Fang {day}.8.` / `{day}.{month}.` oder `Fang: {month}/{day}`).
4. Setze `translation/locked.tsv` für Deutsch zurück und ergänze den Umlaut-Hinweis im Linter.
5. Führe `uv run pytest` und `uv run ruff check .` aus — **alle Tests müssen grün sein!**

---

## 3. Abnahmekriterien (Definition of Done)

- [ ] Deutsche `SPEAKER_LABELS` sind aktiv und in allen bestehenden Dateien migriert (Build bricht nirgends wegen unbekannter Sprecher).
- [ ] `title@7A78.0` akzeptiert und rendert `Ja | Nein` fehlerfrei ohne Zellen-Überlauf.
- [ ] `{day}. August` auf dem Speicherbildschirm ist per Test verifiziert.
- [ ] `translation/locked.tsv` blockiert keine deutschen Übersetzungen mehr.
- [ ] `uv run pytest` und `uv run boku lint` laufen fehlerfrei durch.
- [ ] **Fortschrittsbericht** `plan/progress/03-engine-und-pipeline-anpassung.md` wurde erstellt und `plan/README.md` aktualisiert.

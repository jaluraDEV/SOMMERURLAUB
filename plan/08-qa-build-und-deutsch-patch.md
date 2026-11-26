# Stufe 8: Gesamt-QA, Visuelle Prüfung, Emulator-Tests & Deutsch-Patch-Release

**Ziel:** Den fertigen deutschen Patch aus allen übersetzten Komponenten zusammenbauen (`build/days/`), jede Zeile und jede Textur durch alle automatischen und visuellen Qualitäts-Gates schicken, Spielstände für gezielte In-Game-Tests generieren und am Ende die fertigen Patch-Dateien (`.xdelta` und `.ppf`) gegen das japanische Original-ROM erzeugen.

---

## 1. Arbeitsschritte für die Endabnahme

### Schritt 8.1: Vollständige Automatische Qualitäts-Gates (0-Fehler-Pflicht)
1. **Gesamt-Linter & Coverage-Prüfung:**
   ```powershell
   uv run boku lint
   uv run boku textures check --out work/textures-de
   uv run boku coverage
   ```
   - `boku lint`: **0 Fehler** (keine abgeschnittenen Zeilen, keine echten Umlaute, keine kaputten `[SEL]`-Menüs, keine zu schnellen Untertitel).
   - `boku coverage`: Prüft für jeden der 31 Tage jede erreichbare Zeile — **0 `missing`**, **0 `refused`**, **0 `not-event`**.
2. **Komplette Test-Suite:**
   ```powershell
   uv run pytest
   uv run ruff check .
   ```
   - Prüft u. a. Sektor-EDC/ECC-Integrität, Container-Relocation, keine japanischen Zeichen in `translation/`, Status-Tabelle `status.tsv` vollständig und konsistent.

### Schritt 8.2: Kompletten Deutsch-Build & Visuelle Mockups erzeugen
1. **VWF-Edit-Set + Deutsches Disc-Image + HTML-Reader bauen:**
   ```powershell
   uv run python tools/vwf/build_prototype.py --edits-only --out build/vwf
   uv run boku build --vwf build/vwf/edits.json --translation translation/days --textures translation/textures --name days-de --out build/days
   uv run boku reader --build build/days
   ```
   *(Hinweis: Ohne `--skip-unfitted` aufrufen! Wenn **alles** passt, baut das Image ohne eine einzige ausgelassene Zeile!)*
2. **Alle Dialogseiten als PNG-Mockups rendern (ohne Emulator!):**
   ```powershell
   uv run python tools/vwf/mockup.py
   ```
   - Zeichnet jede einzelne Seite des Spiels exakt in der Geometrie des Dialogbands unter `work/mockup/`. Ideal für schnelle optische Stichproben auf unschöne Zeilenumbrüche oder Worttrennungen!
3. **HTML-Gesamt-Reader (`work/reader/index.html`) prüfen:**
   - Zeigt das gesamte Spiel in Spielreihenfolge: Japanisch neben Deutsch, alle gesetzten Texturen direkt neben den Original-Texturen und die Epilog-Zeitachsen über den Endbildern!

### Schritt 8.3: Konsistenz- & Sprach-Feinschliff (Ganzheits-Check)
Ein dedizierter QA-Durchgang prüft quer über alle Dateien:
- Stimmen alle Item-, Insekten-, Drachen- und Ortsnamen in `day01`–`day31`, `shared.txt`, `arrays.txt`, `books.txt` und `diary.txt` zu 100 % überein?
- Gibt es versehentlich übrig gebliebene englische Wörter (z. B. `Yes | No`, `Back`, `Yeah`, `Huh?`, `Uncle`, `Auntie`)? (Gezielte Regex-Suche über `translation/`!)
- Sind Du/Sie-Wechsel (Familie = *du*, Mönch = *Sie*, Saori = anfangs *Sie* von Boku / *du* von ihr) überall konsistent?

### Schritt 8.4: In-Game-Prüfung im Emulator (DuckStation / Beetle PSX)
1. Falls Beetle PSX Core + PS1-BIOS vorhanden sind:
   - Generiere die Test-Memory-Cards für **jeden Morgen vom 2. bis 31. August + alle 5 Enden + Käfer-Sumo**:
     ```powershell
     # Über make.sh duckstation-cards oder direkt via run_core.py + boku save
     ```
   - Alternativ kann das gebaute `build/days/image.cue` direkt vom User in **DuckStation** oder **RetroArch (Beetle PSX)** geöffnet werden, um Titelmenü, Intro-Film (`M27`), Tag-1-Ankunft, Optionen, Memory Card (`Ja | Nein`, `{day}. August`), Käferfang & Tagebuch live im Spiel zu erleben!

### Schritt 8.5: Fertige Deutsch-Patch-Dateien generieren (`.xdelta` & `.ppf`)
1. Erzeuge die offiziellen Patch-Dateien gegen das verifizierte japanische Original-Image (`disc/image.img`):
   ```powershell
   uv run boku patch --modified build/days/image.img --out build/patch
   ```
   - Erzeugt den **xdelta3-Patch** (komplett inkl. aller relozierten Sektoren & FMV-Hooks) sowie optional den **PPF-Patch** + SHA-1-Prüfsummen!
2. **Round-Trip-Verifikation des Patches:**
   Wende den erzeugten Patch testweise auf das frische Original-ROM aus `rom/` an:
   ```powershell
   uv run boku apply-patch disc/image.img build/patch/<PATCH_DATEI> --out build/verify-patched.img
   ```
   und bestätige, dass die SHA-1-Prüfsumme von `verify-patched.img` exakt mit `build/days/image.img` übereinstimmt!

---

## 2. Abnahmekriterien (Definition of Done — Projektabschluss!)

- [ ] `uv run boku build` läuft **ohne `--skip-unfitted`** mit 0 ausgelassenen Zeilen durch.
- [ ] `uv run boku lint`, `uv run boku textures check` und `uv run boku coverage` melden **100 % Abdeckung & 0 Fehler**.
- [ ] Keine versehentlichen englischen Reste, keine echten Umlaute (`äöüß`), keine japanischen Zeichen in `translation/`.
- [ ] Fertiger Deutsch-Patch liegt getestet und hash-verifiziert unter `build/patch/` bereit.
- [ ] **Abschlussbericht** `plan/progress/08-qa-build-und-deutsch-patch.md` wurde erstellt und alle Stufen in `plan/README.md` stehen auf `[x] Abgeschlossen`.

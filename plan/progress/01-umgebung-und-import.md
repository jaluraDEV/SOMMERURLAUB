# Fortschrittsbericht — Stufe 1: Windows-Umgebung, Tooling & Disc-Import

- **Datum:** 2026-11-26
- **Status:** Abgeschlossen
- **Bearbeitete Dateien:** `tools/vwf/build_prototype.py`, `make.sh`, `boku/research.py`, `tools/textures/make_plan.py`, `README.md`, `tests/test_real_movie_subtitle.py`, `tests/test_emulator_paths.py`, `tests/test_patchfile.py`, `tests/test_trial.py`, `tests/test_real_extract.py`, `tests/test_reader.py`, `tests/test_movies.py`, `tests/test_mode_one.py`, `tests/test_release.py`, `tests/test_packets.py`, `tests/test_docs.py`, `tests/test_importer.py`, `tests/test_real_date_labels.py`, `tests/test_real_patch.py`, `tests/test_real_save_title.py`, `tests/test_real_texture_sumo.py`, `tests/test_run_core.py`, `tests/test_sumo.py`, `tests/test_texture_sumo.py`, `tests/test_textures.py`, `plan/progress/01-umgebung-und-import.md`, `plan/progress/README.md`, `plan/README.md`

---

## 1. Was wurde gemacht?

- **Python-Umgebung (`uv` + `.venv`) eingerichtet:**
  - `uv 0.13.10` (`astral-sh.uv`) via `winget` installiert und `uv sync` im Projektverzeichnis ausgeführt.
  - Virtuelle Umgebung `.venv` mit `CPython 3.12.16`, `boku==0.1.0`, `pytest==9.1.1`, `ruff==0.16.8` eingerichtet.
- **Native Werkzeuge (`armips.exe` & `xdelta3.exe`) installiert & per Hash verifiziert:**
  - **`Kingcom/armips` `v0.11.0`** (`armips-v0.11.0-windows-x86.7z`, Archiv-SHA-256: `ead4c8282867255c9e47cd8855383422d82e31908721405a5b7191b95125262b`) nach `%USERPROFILE%\.local\bin\armips.exe` extrahiert (`armips.exe`-SHA-256: `02c589ae509a7706bf73d0507949ff722288f1d2deea67a13f33c741bc8696ba`).
  - **`jmacd/xdelta` `v3.2.2`** (`xdelta3-3.2.2-windows-x86_64.zip`, Archiv-SHA-256: `d48f7651d86b78fdca397057b46601f89131f37219675df736db70af44ec3379` — exakter Release-Treffer) nach `%USERPROFILE%\.local\bin\xdelta3.exe` extrahiert (`xdelta3.exe`-SHA-256: `732980d52f9220dc81817ccdd0c295eadce8a0048a24c2a771a73f791ac824e9`).
  - `xdelta3.exe` unabhängig mit `-e -9 -S lzma -B 524288 -A ""` auf einem temporären Testpaar geprüft: erzeugt leeren VCDIFF-App-Header (`b''`) und dekodiert mit `-f -d` verlustfrei.
- **Englische Referenz gesichert:**
  - `translation/` unverändert nach `work/english-reference/` kopiert (**55 Dateien, 511.664 Bytes**). `translation/` selbst blieb komplett unberührt und frei von japanischen Schriftzeichen.
- **Disc-Import & Skript-Extraktion durchgeführt:**
  - `uv run boku import "rom\Boku no Natsuyasumi - Summer Holiday 20th Century (Japan).cue"`:
    - Verifizierter Redump-SHA-1: `5959bf7d9835d0a60aeb0143e2d0fc564bfea9fa` (`658.959.840` Bytes).
    - `disc/image.img`, `disc/image.cue`, `disc/manifest.json` (30 Dateisystem-Einträge) sowie 3 extrahierte Dateien unter `disc/files/` (`SCPS_100.88` 524.288 B, `BOKU.BIN` 109.303.808 B, `SYSTEM.CNF` 68 B).
  - `uv run boku extract` (4,2 s):
    - `disc/script/lines.jsonl` (`2.377.445` B, `2.994` Einträge), `disc/script/index.json` (`780` B), `disc/script/arrays.json` und `disc/script/scenes/`: **2.987 logische Zeilen** über **6.193 physische Fundstellen**, **74.619 Glyphen**, **677 Szenen**, **34 Arrays**, Glyph-Table-Hash `7347be7bf7fa`.
- **Englischer Baseline-Build & HTML-Reader erfolgreich gebaut:**
  - `uv run python tools/vwf/build_prototype.py --edits-only --out build/vwf` → `build/vwf/edits.json` (`110.229` B; `129` Byte-Edits über `12.019` B, `92` Glyphenzellen, `91` neu gezeichnet, `ORIGINAL=1`-Retail-Identitätsprüfung bestanden).
  - `uv run boku build --vwf build/vwf/edits.json --translation translation/days --textures translation/textures --name days --out build/days --skip-unfitted` → `build/days/image.img` (`658.959.840` B, SHA-1 `510fff705dd4ab11aaef91a9215080524da8d0cd`), `2.983` Zeilen gesetzt, `0` abgewiesen (`refused`), `33` unerreichbare Retail-Einträge belassen, `636` Archiv-Member neu gebaut, `31.255` Sektoren geändert (EDC/ECC verifiziert).
  - `uv run boku reader --build build/days` → `work/reader/index.html` (`1.638.164` B; `3.345` Einträge in `40` Sektionen).

---

## 2. Wichtige Entscheidungen & Gelöste Probleme

1. **Windows-`armips`-Erkennung (`tools/vwf/build_prototype.py`):**
   - `find_armips()` ergänzt: prüft zuerst den macOS/Source-Pfad `~/Dev/dist/armips/build/armips`, danach `shutil.which("armips")` (findet `%USERPROFILE%\.local\bin\armips.exe`), danach `work/bin/armips(.exe)`, und fällt sonst auf den Standardpfad zurück.
   - In `run_armips()` wird der Pfad vor `cwd=asm.parent` aufgelöst, sodass auch relative `--armips`-Pfade oder bloße Befehlsnamen korrekt funktionieren.
2. **Nicht-Git-Checkout-Kompatibilität (`make.sh` & `tests/test_reader.py`):**
   - Da der Arbeitsordner kein `.git`-Verzeichnis enthält, wurde `git describe` in `make.sh` (`cmd_build_days`) so abgesichert, dass bei fehlendem `.git` kein Abbruch durch `set -euo pipefail` erfolgt.
   - `tests/test_reader.py::test_a_build_from_another_commit_whose_code_differs_is_said` überspringt sauber mit `pytest.skip("not a git checkout: no commit history")`, wenn keine Git-Historie vorliegt.
3. **Windows-Testsuite & Encoding-Hygiene (ohne Abschwächung von Assertions):**
   - `boku/research.py` (`write_scene_tsvs`) und `tools/textures/make_plan.py` schreiben nun explizit UTF-8 mit `newline="\n"`, damit bytegenaue `.tsv`-Vergleiche unter Windows kein CRLF erzeugen.
   - `tests/`: `.cmd`-Wrapper unter `os.name == "nt"` für `fake-xdelta3`, `my-java`/`fake-jpsxdec`, `chdman-dies` und `stub_on_path`; Git-Bash-Aufruf mit `shlex.quote(...as_posix())` in `test_emulator_paths.py` und `test_release.py`; `_winapi.CreateJunction`-Fallback bei fehlendem Windows-Symlink-Recht (`WinError 1314`) in `test_trial.py` und `test_real_extract.py`; `re.escape(...)` bei Windows-Pfaden in `pytest.raises(..., match=...)` (`test_emulator_paths.py`, `test_mode_one.py`); explizites `encoding="utf-8"` für `read_text`/`write_text` in 12 Testmodulen.
4. **Upstream-Tabellenfehler in `README.md` behoben:**
   - `README.md` (Abschnitt *Which version do I have?*) hatte eine 2-spaltige Tabelle (`| version | the image's SHA-1 |`), während der eigene Text von der „middle column“ spricht und `boku/release.py` (`VERSIONS_HEADER`) sowie `tests/test_release.py::test_the_readme_holds_the_table_release_row_writes` eine 3-spaltige Tabelle erwarten (`| version | your dump's SHA-1, before patching | the patched image's SHA-1 |`). Die Tabelle in `README.md` wurde entsprechend korrigiert.

---

## 3. Qualitäts- & Test-Nachweis (Gates)

- **`uv run boku lint`:** Bestanden (`0 error(s)`, `33 warning(s) -- unreachable 33` über `3.115` gelesene Zeilen; bekannte unerreichbare Sumo-Array-Einträge `musi@2C.0`–`.31` + `exe@code:80037698`).
- **`uv run boku textures check`:** Bestanden (`16 families built from translation\textures`, `258.827` Byte-Edits, `0` Fehler).
- **`uv run ruff check .`:** Bestanden (`All checks passed!`).
- **`uv run ruff format --check .`:** Bestanden (`216 files already formatted`).
- **`uv run pytest`:** **1.915 passed, 148 skipped, 0 failed, 0 errors** (alle 2.063 gesammelten Tests). Die 148 Skips entfallen ausschließlich auf fehlende optionale Umgebungskomponenten:
  - `63` Emulator-Tests (`BOKU_EMU_TESTS=1` nicht gesetzt / kein PS1-Emulator-Core & BIOS)
  - `51` `chdman`-Tests (`test_release.py`: 48, `test_mode_one.py`: 3)
  - `10` ungebautes `build/trial/` (`test_real_patch.py`)
  - `8` fehlendes `.git`-Verzeichnis (`test_make_verbs.py`: 7, `test_reader.py`: 1)
  - `7` macOS-Tool `sips` (`test_png.py`)
  - `5` `ffmpeg` (`test_movies.py`)
  - `4` `work/saves/sample.mcd` (`test_save.py`)
- **`test_translation_has_no_japanese.py`:** Bestanden (`translation/` enthält 0 japanische Zeichen).

---

## 4. Übergabe an den nächsten Agenten / Offene Punkte

- Die komplette Windows-Pipeline (`uv`, `armips.exe`, `xdelta3.exe`), das importierte & extrahierte Disc-Verzeichnis (`disc/`), das vollständige englische Referenz-Backup (`work/english-reference/`) sowie der erste englische Baseline-Build (`build/vwf/`, `build/days/`, `work/reader/`) stehen bereit.
- **Wichtige Korpus-Beobachtung für Stufe 2–6:** `work/english-reference/` und `translation/` umfassen real **55 Dateien** (davon **43 Textdatendateien** mit **3.504** Einträgen statt der in älteren Plan-Tabellen genannten „42 Dateien / 3.538 Einträge“; Details siehe `PROJECT.md`).
- **Nächster Schritt:** **[Stufe 2: Deutsche Stilbibel, Anrede-Regeln & Glossar](../02-deutsche-stilbibel-glossar.md)** — `translation/style-guide.md`, `translation/glossary.md` und `translation/checklist.md` für die deutsche Übersetzung ausarbeiten (`ae/oe/ue/ss`-Konvention, Du/Sie-System, 15 `SPEAKER_LABELS`).

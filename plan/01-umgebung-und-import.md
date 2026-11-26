# Stufe 1: Windows-Umgebung, Tooling & Disc-Import

**Ziel:** Alle benötigten CLI-Werkzeuge unter Windows lauffähig machen, das japanische Basis-ROM (`rom/*.bin`) über die offizielle Pipeline importieren, das japanische Skript extrahieren und einmal unverändert den aktuellen (englischen) Build erfolgreich durchlaufen lassen, um eine 100% funktionierende Baseline zu beweisen.

---

## 1. Ausgangslage auf diesem System (aus Analyse)

- **Betriebssystem:** Windows (PowerShell + Git for Windows installiert unter `C:\Program Files\Git\`, d. h. Git Bash ist unter `C:\Program Files\Git\bin\bash.exe` verfügbar!).
- **ROM vorhanden & verifiziert:**
  - Pfad: `rom/Boku no Natsuyasumi - Summer Holiday 20th Century (Japan).bin` (`.cue` liegt daneben)
  - Gemessener SHA-1: `5959BF7D9835D0A60AEB0143E2D0FC564BFEA9FA` → **exakter Redump-Treffer!**
- **Noch fehlende Tools im PATH:**
  1. `uv` (Python-Paket- und Umgebungsmanager — verwaltet automatisch Python ≥ 3.12 + `pytest` + `ruff`)
  2. `armips` (MIPS-Assembler für `asm/*.asm` → wird von `tools/vwf/build_prototype.py` benötigt)
  3. `xdelta3` (für das spätere Erstellen der `.xdelta`-Patchdatei in Stufe 8; `.ppf` wird bereits in reinem Python gebaut)

---

## 2. Arbeitsschritte für den Agenten

### Schritt 1.1: `uv` und Python 3.12+ einrichten
1. Installiere `uv` (z. B. via `winget install --id=astral-sh.uv -e` oder offizielles PowerShell-Skript).
2. Prüfe im Projektordner `uv sync` — `uv` lädt automatisch eine passende Python-Version (laut `.python-version` / `pyproject.toml`) sowie `pytest` und `ruff` herunter.
3. Führe die disc-unabhängigen Unit-Tests aus:
   ```powershell
   uv run pytest -k "not real"
   ```

### Schritt 1.2: `armips` (und `xdelta3`) bereitstellen
1. Lade das offizielle Windows-Release-Binary von **armips** (z. B. GitHub `Kingcom/armips` Release `armips.exe`) und lege es entweder in den `PATH` oder lokal unter einem gitignorierten Tool-Pfad wie `work/bin/armips.exe` ab.
   - *Hinweis zu `tools/vwf/build_prototype.py`:* Prüfe Flag `--armips <PFAD>` (oder Umgebungsvariable / `shutil.which("armips")`). Falls `build_prototype.py` auf macOS-Pfad `~/Dev/dist/armips/build/armips` zurückfällt, stelle sicher, dass `shutil.which("armips")` unter Windows `armips.exe` findet.
2. Lade `xdelta3.exe` (für Stufe 8) ebenfalls bereit oder installiere es via Winget/Scoop, damit `uv run boku patch` später sofort funktioniert.

### Schritt 1.3: Englische Referenz sichern (Backup)
Bevor später ab Stufe 3/4 Dateien in `translation/` überschrieben werden, legen wir in `work/english-reference/` eine vollständige lokale Referenzkopie des originalen englischen `translation/`-Ordners an:
```powershell
Copy-Item -Path translation -Destination work\english-reference -Recurse -Force
```
*(Wichtig: Dadurch können Übersetzungs-Agenten in Stufe 4–7 jederzeit die geprüfte englische Zeile + `# NOTE`-Kommentare neben dem japanischen Original nachschlagen!)*

### Schritt 1.4: Disc-Import & Skript-Extraktion ausführen
1. Importiere das Basis-ROM in `disc/`:
   ```powershell
   uv run boku import "rom\Boku no Natsuyasumi - Summer Holiday 20th Century (Japan).cue"
   ```
   *(Erzeugt `disc/image.img`, `disc/image.cue`, `disc/manifest.json` und entpackt alle Archivdateien nach `disc/files/`.)*
2. Extrahiere das japanische Spielskript & die Szenen-Graphen:
   ```powershell
   uv run boku extract
   ```
   *(Erzeugt `disc/script/lines.jsonl` und `disc/script/scenes/`.)*

### Schritt 1.5: Baseline-Build & Linter-Test (Englisch)
Prüfe, ob die komplette Build-Kette unter Windows sauber durchläuft:
1. VWF-Renderer & Edit-Set bauen:
   ```powershell
   uv run python tools/vwf/build_prototype.py --edits-only --out build/vwf --armips <PFAD_ZU_ARMIPS_ODER_IM_PATH>
   ```
2. Linter & Textur-Check testen:
   ```powershell
   uv run boku lint
   uv run boku textures check
   ```
3. Komplettes Test-Image + HTML-Reader bauen:
   ```powershell
   uv run boku build --vwf build/vwf/edits.json --translation translation/days --textures translation/textures --name days --out build/days --skip-unfitted
   uv run boku reader --build build/days
   ```
4. Optional: Ein Windows-Hilfsskript `make.ps1` (oder Nutzung von Git Bash `& "C:\Program Files\Git\bin\bash.exe" ./make.sh ...`) testen, damit alle Befehle unter Windows mit einem Einzeiler aufrufbar sind.

---

## 3. Abnahmekriterien (Definition of Done)

- [ ] `uv run pytest` läuft grün durch (inkl. der `test_real_*`-Tests, die keine Emulator-Binaries benötigen).
- [ ] `disc/image.img` und `disc/script/lines.jsonl` existieren lokal.
- [ ] `work/english-reference/` enthält das vollständige Backup der englischen Übersetzungsdateien.
- [ ] `build/vwf/edits.json`, `build/days/image.img` und `work/reader/index.html` lassen sich fehlerfrei unter Windows bauen.
- [ ] **Fortschrittsbericht** `plan/progress/01-umgebung-und-import.md` wurde erstellt und `plan/README.md` aktualisiert.

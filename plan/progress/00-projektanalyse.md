# Fortschrittsbericht 00 — Initiale Projekt- & Machbarkeitsanalyse

- **Datum:** 2026-11-26
- **Status:** Abgeschlossen
- **Analysierte Bereiche:** Gesamtes Repository (`CLAUDE.md`, `README.md`, `TECHNICAL.md`, `make.sh`, `boku/`, `asm/`, `tools/vwf/`, `translation/`, `tests/`, `rom/`)

---

## 1. Executive Summary: Wie gut eignet sich dieses Projekt für einen KI-Deutsch-Patch?

**Hervorragend — besser könnte eine ROM-Hack-Basis kaum sein!**
Im Gegensatz zu klassischen PS1-ROM-Hacks mit kryptischen Binär-Tools ist `boku-ps1` eine hochmoderne, vollständig getestete Python- & MIPS-Assembler-Toolchain:
- Das gesamte Reverse Engineering (horizontales VWF-Textrendering statt vertikalem Japanisch, breites 3-Zeilen-Dialogband unter der Szene, automatisches Verschieben gewachsener Archive auf freie CD-Sektoren, programmatisches Übermalen & Setzen von Texturen, Live-Untertitel-Hooks für Videos und Voice-Only-Szenen, Sektor-EDC/ECC-Neuberechnung) ist **zu 100 % fertig entwickelt und getestet**.
- Alle übersetzbaren Inhalte liegen als saubere, ID-basierte Klartextdateien (`.txt`, Tab-getrennt) im Ordner `translation/` vor.
- Das vom User bereitgestellte Basis-ROM unter `rom/Boku no Natsuyasumi - Summer Holiday 20th Century (Japan).bin` wurde per SHA-1 geprüft:
  - **Gemessener SHA-1:** `5959BF7D9835D0A60AEB0143E2D0FC564BFEA9FA`
  - **Erwarteter Redump-SHA-1:** `5959bf7d9835d0a60aeb0143e2d0fc564bfea9fa` → **100 % Treffer!**

---

## 2. Exakte Bestandsaufnahme aller zu übersetzenden Texte

Insgesamt umfasst das komplette Spiel exakt **3.538 Text-Einträge** in 42 Dateien:

| Kategorie | Pfad | Dateien | Einträge | Besonderheiten |
|---|---|---|---|---|
| **Menüs, Items, Insekten & Code** | `translation/days/arrays.txt` | 1 | **314** | Strenge Box-Pixelbreiten (`text-boxes.tsv`), 57 Insektennamen, 60 Insektenbuch-Texte, Save-Titel |
| **Tagesunabhängige Events** | `translation/days/shared.txt` | 1 | **750** | Haus-Untersuchungen, Bad, Kühlschrank, Abendessen-Quiz, Schlafengehen |
| **Story-Skript (Tag 1–31)** | `translation/days/day01..31.txt` | 31 | **2.085** | Szenische Dialoge mit festen Seitenumbrüchen (` // `) bei Sprachausgabe |
| **Programmatische Texturen** | `translation/textures/*.txt` | 8 | **300** | Titelmenü, Optionen, Stein-Buttons, Sprechblasen, Schilder, 2 Lexika, **93 Tagebuchseiten** |
| **Code-Sprachclips & Epiloge** | `translation/clips.txt` | 1 | **46** | Käfer-Sumo-Rufe + 5 große Epiloge mit Sekunden-Timings vor der Sony-Endkarte |
| **FMV-Videos & Titelsong** | `translation/movies.txt` | 1 | **43** | Frame-genaue Untertitel (15 fps), max. 2 Zeilen à 318 px, max. 17 Zeichen/Sekunde |
| **GESAMT** | | **43** | **3.538** | |

---

## 3. Warum die Umlaut-Umschrift (`ae`, `oe`, `ue`, `ss`) technisch Gold wert ist

Im Spiel existieren **vier getrennte Text-Systeme**:
1. **Haupt-VWF-Renderer (`tools/vwf/build_prototype.py` + `placeholder-glyphs.txt`):** Nutzt die 12×12-Glyphentabelle aus `ONMEM.BIN` (`A–Z`, `a–z`, `0–9` + gezeichnete Satzzeichen).
2. **Textur-Hauptschrift (`boku/typeset.py` → `GameFace`):** Liest `A–Z`, `a–z`, `0–9` direkt zur Build-Zeit aus der Original-Disc-Schrifttextur aus — dort existieren keine Umlaute.
3. **Mini-Pixelfonts (`boku/faces/bean.txt` & `sprout.txt`):** Handgepixelte Kleinstschriften für kleine Buttons, Stempelkarte und die zweispaltigen Enzyklopädien — enthalten nur ASCII.
4. **PS1-BIOS Memory-Card-Titel (`boku/code_text.py` → `full_width`):** Wandelt ASCII in Full-Width Shift-JIS (`0xFF01..`) um — der japanische Shift-JIS-Standard besitzt überhaupt kein `ä`, `ö`, `ü` oder `ß`!

**Fazit:** Durch die Entscheidung für `ae`, `oe`, `ue`, `Ae`, `Oe`, `Ue` und `ss` (*Räume → Raeume*, *Käfer → Kaefer*, *Größe → Groesse*) funktionieren **alle vier Schriftsysteme sofort fehlerfrei**, ohne eine einzige Font-Grafik oder Assembler-Breitentabelle neu zeichnen zu müssen!

---

## 4. Gefundene technische Fallstricke im Code (und wie unser Plan sie löst)

Bei der tiefen Durchsicht von `boku/` und `tests/` wurden **6 wichtige Details** identifiziert, die bei einer naiven Übersetzung den Build gebrochen hätten und nun fest in **Stufe 1–4** eingeplant sind:

1. **Das `Ja | Nein` 6-Zellen-Problem (`title@7A78.0` in `boku/layout.py` Zeile 785):**
   - Auf dem Speicherkarten-Screen hat das japanische Original `はい` (2) + `いいえ` (3) = **5 Glyphen-Zellen**. Englisch `Yes` (3) + `No` (2) = **5 Zellen** passte zufällig exakt rein. Deutsch `Ja` (2) + `Nein` (4) = **6 Zellen** würde abgelehnt!
   - *Lösung in Stufe 3:* Sauberes Relozieren des 6-Zellen-Paars in `TITLE.OVL` + Anpassen der Zählkonstante `COUNT` an `0x8007D064` — keine unschöne Abkürzung nötig!
2. **Hartcodierte englische `SPEAKER_LABELS` (`boku/layout.py` Zeile 391 & `tests/test_build.py` Zeile 628):**
   - Der Builder schreibt das Sprecher-Label aus den `.txt`-Dateien direkt vor `「` ins Spiel (`Uncle「...」`) und prüft es gegen `SPEAKER_LABELS` und `style-guide.md` § 9.
   - *Lösung in Stufe 3:* Umstellung auf deutsche Labels (`Onkel`, `Tante`, `Vater`, `Moench`, `Junge`, `Frau`, `Brille`, `Erzaehler`, `Alle` + Eigennamen).
3. **Wort-Sperren aus dem Englischen (`translation/locked.tsv` & `tests/test_locked.py`):**
   - Erzwingt ca. 80 englische Lieblingsformulierungen des Original-Autors Jay.
   - *Lösung in Stufe 1 & 3:* Englische Referenz nach `work/english-reference/` sichern und `locked.tsv` für Deutsch zurücksetzen.
4. **Dynamische Datums-Anzeigen (`asm/labels.asm` & `boku/code_text.py`):**
   - `title@code:8007BB60` (`August {day}`) unterstützt in `vwf_save_date_label` bereits Präfix + Zahl + Suffix, sodass deutsches `{day}. August` unterstützt wird! `exe@code:80037544` (`Caught {month}/{day}`) wird in Stufe 3 sauber für Deutsch eingerichtet.
5. **Cross-File-Test zwischen `arrays.txt` und `textures/sumo.txt`:**
   - Die 19 Sumo-Techniken (`musi@2C.13`–`.31` und `sumo@move.1`–`.19`) sowie die 3 Ränge müssen in beiden Dateien wortgleich sein, sonst schlägt `pytest` fehl.
6. **Windows-Umgebung:**
   - `uv`, `armips` und `xdelta3` sind aktuell noch nicht im Windows-`PATH` installiert (Git inkl. Git Bash ist bereits vorhanden). Das wird als allererstes in **Stufe 1** sauber eingerichtet.

---

## 5. Übergabe an Stufe 1

Der Master-Plan (`plan/README.md`) sowie alle Einzelpläne (`01` bis `08`) sind fertiggestellt. Der nächste Schritt ist **[Stufe 1: Windows-Umgebung, Tooling & Disc-Import](../01-umgebung-und-import.md)** (oder vorab kurzes Feedback des Users zu eventuellen Namens-Wünschen für Stufe 2).

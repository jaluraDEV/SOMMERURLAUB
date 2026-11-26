# Stufe 5: Programmatische Texturen & Bildertagebuch (`translation/textures/`)

**Ziel:** Übersetzung und pixelgenaues Typesetting aller **300 Textur-Strings** in den 8 Dateien unter `translation/textures/` — inklusive Titelbildschirm, Buttons, Schildern in der Spielwelt, Insekten- & Drachen-Enzyklopädie sowie aller **93 Bildertagebuch-Einträge** von Boku!

---

## 1. Wie das Textur-System funktioniert (Kein Grafikprogramm nötig!)

Das Projekt besitzt einen vollautomatischen Pixel-Typesetter (`boku/typeset.py` + `boku/texture_*.py`):
- Beim Build nimmt Python die Original-TIM-Texturen aus `disc/files/`, übermalt den japanischen Text sauber mit dem lokalen Hintergrundmuster und setzt den deutschen Text aus `translation/textures/*.txt` pixelgenau hinein!
- Verwendet werden drei Schriftarten (automatisch je nach Rezept gewählt):
  1. **`GameFace`**: Die 12×12-Hauptschrift des Spiels (unterstützt `A–Z`, `a–z`, `0–9`, `! # % & ' * + , - . / : ; < = > ? @ _ |` — **Achtung: KEINE doppelten Anführungszeichen `"` und runde Klammern `( )` vermeiden**, da diese im Sheet vertikale Formen haben!).
  2. **`Bean` & `Sprout`** (`boku/faces/`): Zwei winzige Pixel-Schriften für kleine Sprechblasen, Buttons, Stempelkarte und die beiden Lexika (unterstützen ASCII `A–Z`, `a–z`, `0–9` sowie `-`, `"`, `[ ]`).
- **Eiserne Sicherheitsgarantie:** Wenn ein deutscher String auch nur **1 Pixel zu breit** oder **1 Zeile zu hoch** für sein Schild, seinen Stein-Button oder seine Tagebuchseite ist, **verweigert** `uv run boku textures check` ihn mit exakter Pixelangabe! Nichts wird jemals stillschweigend abgeschnitten!

---

## 2. Die 8 Textur-Dateien im Detail

### Block A: UI, Buttons, HUD & Schilder (138 Einträge)
1. **`ui.txt` (18 Einträge):**
   - Titelmenü (`tex@T_TITLE.0`–`.3`): `Neues Spiel`, `Weiter` / `Fortsetzen`, `Sommer-Erinnerungen` (Breite prüfen!), `Einstellungen` / `Optionen`.
   - Einstellungsmenü (`T_CONFIG.*`): `Optionen`, `Stimme + Text`, `Abbruch OK`, `Nur Stimme`, `Kein Abbruch`, `Stereo`, `Mono`, `Aktion`, `Abbruch`, `Rennen`, `Unter- // menue` (` // ` für Zeilenumbruch nur wo erlaubt!).
   - Album-Plakette (`T_MEMORY.heading`): `Sommer- // Erinnerungen` (max. 99 px pro Zeile!).
   - Epilog-Credits-Karte (`OTI.*`): `Produktion und Copyright` / `Sony Computer Entertainment Inc.`.
2. **`buttons.txt` (52 Einträge):**
   - 12× Stein-Button `Back` → **`Zurueck`** (prüfen, ob `Zurueck` auf alle 12 Steine passt — falls ein einzelner Stein extrem schmal ist, meldet `textures check` die exakte Pixelzahl!).
   - Sprechblasen am Schreibtisch, Tasche, Insektenkasten, Käfer-Sumo (`Sachen`, `Drachen // steigen`, `Angel- // zeug`, `Insekten- // kaefig`, `Haende // frei`, `Kescher`, `Tauschen`, `Freilassen`, `Lupe`, `Medizin`, `Spritze`, `Gute // Nacht`, ...).
   - Radio-Gymnastik-Stempelkarte (`PK_ITM.title` & `.footer` in `Sprout`): `Radio- // Gymnastik // Stempelkarte` & `Einen gesunden Sommer!`.
   - Käfig-Stern (`MITIM.rare`, max. 32 px inkl. Schatten!): `Wow!` oder `Selten` (`Wow!` passt sicher in 32 px!).
3. **`signs.txt` (10 Einträge):**
   - Strandschild (`M_C15`): `Flut!` / `Baden verboten` (2× vergrößerte Schrift, rechts am Bildschirmrand angeschnitten — mit `--out work/textures-de` optisch prüfen!).
   - Saoris Abschiedsbrief (`M_I14000`, Tag 28): Bis zu 5 Zeilen (` // `), max. 83 px pro Zeile (`Leb wohl. // Du warst // ein echt guter // Kerl.` + Signatur `Deine Saori` / `Von Saori`).
   - Türschild oben (`M_I18`): `Nicht // reinkommen!` oder `Zutritt // verboten!` (Kinder-Filzstift!).
   - Tauschheft-Cover (`M_S01000`): `Kaefer- // Tausch- // Heft` (3 Zeilen, 1. Zeile doppelt groß!).
   - Jagd-Warnschild (`M_I23000`): `GEFAHR!`, `Haeuser nah,`, `Vorsicht Schuss!`, `Jagdverband // der Praefektur` (exakt zwischen Einschusslöcher & Sterne eingepasst!).
4. **`records.txt` (13 Einträge):**
   - Angel-Rekordtafel (`FS_WAL.*`) & Käfertausch-Karte (`M_S01100.*`: `Gefangen 8/`, `S`, `N` passend zu `SN` aus `arrays.txt`, `Wert entspricht`, `Saege-Hirschk.`).
5. **`kite.txt` (3 Einträge):**
   - Drachenflug-HUD unten: `Wind`, `Tempo`, `Hoehe` (Achtung: `Wind` + `Tempo` nebeneinander über `m/h`!).
6. **`sumo.txt` (42 Einträge):**
   - `Ausdauer` (`stamina`), Ränge (`Schwach`, `Stark`, `Koenig` — identisch zu `arrays.txt` `musi@358`!), `Siegestechnik` (`move.heading`), die 22 Move-Namen (1–19 identisch zu `arrays.txt`!) und die **15 deutschen Kurz-Glossen** (`move.gloss-*`, max. 122 px fettgedruckt, z. B. `Frontal-Hinausstoss`, `Kopfstoss-Angriff`, `Armwurf ueber Schulter`).

### Block B: Insekten- & Drachen-Enzyklopädie (`books.txt`, 69 Einträge)
- **9 Doppelseiten Insekten-Lexikon (`mzkan@0`–`8`)** + **8 Seiten Drachen-Lexikon (`tzkan@0`–`7`)**.
- Titel in `GameFace`, Fließtext zweispaltig in `Bean`.
- **Wichtig:** Artnamen und Drachennamen **müssen** exakt dem Glossar & `arrays.txt` entsprechen! Keine doppelten Anführungszeichen `"` in `GameFace`-Titeln!

### Block C: Bokus Bildertagebuch (`diary.txt`, 93 Einträge)
- `nikki@NIKKI_001` bis `nikki@NIKKI_099` — das Herzstück der Atmosphäre!
- Jeder Eintrag wird auf **maximal 5 linierte Zeilen** (ca. 32 Zeichen pro Zeile in `GameFace`, **keine `"` und keine `( )`!**) unter Bokus Wachsmalbild gesetzt.
- **Stil:** Echte Drittklässler-Sätze auf Deutsch! Kurz, direkt, kindliche Logik bewahren (z. B. `NIKKI_002`: *„Kaefer sind schnell. Ich bin langsam. Ich habe nur 2 Beine. Die haben ganz viele. Ich verliere."*).

---

## 3. Arbeitsschritte für den Agenten

1. Bearbeite die Dateien in drei sauberen Teil-Schritten:
   - **5a:** `ui.txt`, `buttons.txt`, `signs.txt`, `records.txt`, `kite.txt`, `sumo.txt`
   - **5b:** `books.txt`
   - **5c:** `diary.txt`
2. Nutze als Quelle sowohl die Kommentare & englischen Texte in `work/english-reference/textures/` als auch (wo nötig) die exportierten Original-Texturen in `work/textures/` (`uv run boku textures export`).
3. Führe nach jedem Teil-Schritt sofort den Typesetting-Check mit Bild-Export aus:
   ```powershell
   uv run boku textures check --out work/textures-de
   ```
4. Inspiziere die erzeugten PNGs in `work/textures-de/` visuell (insbesondere Schilder `M_C15`, `M_I14000`, `M_I23000`, `T_TITLE`, `T_CONFIG`, Buttons und Stichproben von `NIKKI_*` & `MZKAN*`), um sicherzugehen, dass nichts gequetscht aussieht!
5. Aktualisiere `translation/status.tsv` für `screens`, `books` und `diary`.

---

## 4. Abnahmekriterien (Definition of Done)

- [ ] Alle 300 Einträge in allen 8 Dateien unter `translation/textures/` sind auf Deutsch (`ae/oe/ue/ss`).
- [ ] `uv run boku textures check --out work/textures-de` läuft mit **0 Zurückweisungen (0 refusals)** durch!
- [ ] Visuelle Stichproben der gerenderten PNGs in `work/textures-de/` bestätigen sauberes Layout auf Schildern, Buttons, Büchern und Tagebuchseiten.
- [ ] `uv run pytest` läuft komplett grün durch.
- [ ] **Fortschrittsbericht** `plan/progress/05-texturen-und-tagebuch.md` wurde erstellt und `plan/README.md` aktualisiert.

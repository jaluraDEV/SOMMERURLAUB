# Stufe 4: UI, Menüs, Items & Insektenbuch (`arrays.txt`)

**Ziel:** Vollständige Übersetzung und Pixel-Validierung aller **314 Einträge** außerhalb der Szenen-Skripte in `translation/days/arrays.txt` (Steuerungshilfe, Memory Card, Optionen, 57 Insektennamen + 60 Insektenbuch-Texte, Items + Beschreibungen, Fische, Drachen, Foto-Kommentare, Käfer-Sumo & Code-Labels).

---

## 1. Warum `arrays.txt` VOR den Dialogen übersetzt wird

1. **Verbindliche Namen im Spiel:** Wenn Boku im Dialog sagt *„Ich habe einen Riesen-Hirschkaefer gefangen!"* oder ein Item erhält, muss der Name im Dialog **buchstabengenau** mit dem Namen im Menü (`arrays.txt`) übereinstimmen.
2. **Strengste Pixel-Limits:** Während Dialoge ein breites 3-Zeilen-Band haben, sitzen Menü-Einträge in festen grafischen Rahmen (`research/data/text-boxes.tsv`). Wenn wir hier die exakten deutschen Begriffe festzurren und mit `uv run boku lint` auf den Pixel genau prüfen, steht das Fundament für alle anderen Dateien!

---

## 2. Spezialfälle & Technische Fallstricke in `arrays.txt`

Jeder Agent, der `arrays.txt` bearbeitet, **muss** diese 8 technischen Regeln beachten:

1. **Ameisen-Zähler (`exe@80029AFC.0`):**
   - Englisch: `"000 ants perished."`
   - **Zwingende Regel:** Der Programmcode überschreibt vor dem Zeichnen exakt die **Zellen 1 bis 3** (direkt nach dem ersten Zeichen `"`) mit drei Ziffern (`COUNTED_CELLS` in `boku/arrays.py`)!
   - Deutsch muss daher mit Anführungszeichen + `000` beginnen, z. B.: `"000 Ameisen sind gestorben."` oder `"000 Ameisen erledigt."`!
2. **Steuerungs-Hilfebildschirm (`exe@80029B20.0`–`.21`):**
   - Enthält spezielle Glyphen-Tokens wie `{G:1481}`, `{G:1482}`, `○`, `×`, `↓` — diese Tokens **niemals verändern**!
   - `.11` und `.12` bilden zusammen einen Satz über 2+1 Bildschirmzeilen (`boku/help_screen.py`).
3. **Insektennamen (`exe@8003D2E0.0`–`.56`) & Tauschbuch-Kurzformen (`@exchange`):**
   - Die 6 `@exchange`-Zeilen (`.23@exchange` bis `.30@exchange`) stehen rechts neben dem Größen-Abzeichen im Käfertausch-Heft und dürfen **maximal ~100 px** breit sein (z. B. `Miyama-Hirschk.` oder `Miyama-Kaefer`, `Riesen-Hirschk.`, `Zwerghirschk.`, `Saege-Hirschk.`, `Rotbein-Hirschk.`, `Nashornkaefer` — exakt mit `uv run boku lint` messen!).
4. **60 Insektenbuch-Einträge (`hhon@5328.0`–`.60`):**
   - Geschrieben aus **Bokus eigener Kinder-Perspektive** (Stilbibel § 10: lockere, kindliche Beobachtungen, kein trockenes Biologie-Lexikon!).
   - Insektenrufe (*kana-kana-kana*, *min-min-min*, *gii-chon*) bleiben wie gehört erhalten.
   - Achtung: Die Symbole `♂` und `♀` (`.23`, `.24`, `.27`, `.30`, `.56`–`.59`) stammen aus dem Font-Sheet (`WithSheetSymbols`) und bleiben exakt erhalten!
5. **Käfer-Sumo-Techniken (`musi@2C.0`–`.31`) — CROSS-FILE-TEST MIT `sumo.txt`!**
   - **WICHTIG:** Ein automatischer Test prüft, dass `musi@2C.13`–`.31` in `arrays.txt` **wortgleich** mit `sumo@move.1`–`.19` in `translation/textures/sumo.txt` übereinstimmen!
   - Echte Sumo-Techniken (`Buchikamashi`, `Tsuppari`, `Utchari`, `Uwatenage`, ...) bleiben als ein Wort japanisch; Spaß-Techniken (`Fighting spirit` → `Kampfgeist`, `Flip-over` → `Umwerfer` / `Rueckwurf`, `Mantis Scissors` → `Gottesanbeterin-Schere` — Pixelbreite prüfen!) werden in beiden Dateien synchron aktualisiert!
6. **Auswahlmenüs (`[SEL]`-Zeilen):**
   - Anzahl der durch ` | ` getrennten Felder ist im Code fest verdrahtet (`select-options`) und darf sich niemals ändern!
   - Beispiele: `Let it go? | Yes | No` → `Freilassen? | Ja | Nein`.
7. **Code-gezeichnete Labels (`exe@code:...`, `title@code:...`):**
   - `exe@code:800377F8`: Genau **2 Buchstaben** für Siege/Niederlagen (`WL` → **`SN`** für Siege/Niederlagen; synchron zu `records.txt`!).
   - `exe@code:80037698` (`Date mounted`): Ungenutzte Funktion ohne Aufrufer (`not-placeable` Warnung ist normal), trotzdem sauber übersetzen.
   - `exe@code:80037544` & `title@code:8007BB60`: Gemäß der Lösung aus Stufe 3 (`{day}. August` etc.).
   - `title@code:8007C8EC` (`) / )`) und `title@code:80080484` (`/31 / 0 / %`): Unverändert lassen!
8. **Memory-Card Save-Titel (`title@sjis:188`):**
   - Muss `{slot}` und `{day}` in genau dieser Reihenfolge enthalten, nur ASCII nutzen (`ae/oe/ue/ss`) und als Full-Width Shift-JIS inkl. zweistelliger Zahlen ≤ 64 Bytes bleiben (max. 27 Zeichen Text um die Platzhalter).
   - Beispiel: `Bokus Sommer {slot} {day}. August` (24 Zeichen → 48 + 8 + 1 = 57 Bytes ≤ 64 Bytes — passt perfekt!).

---

## 3. Arbeitsschritte für den Agenten

1. Erzeuge das Übersetzungspaket für die Arrays (`uv run boku packet --arrays`), um neben `work/english-reference/days/arrays.txt` auch alle japanischen Originalstrings vor Augen zu haben.
2. Übersetze `translation/days/arrays.txt` komplett ins Deutsche gemäß Glossar (Stufe 2) und `ae/oe/ue/ss`-Regel.
3. Synchronisiere direkt die 19 Sumo-Move-Zeilen in `translation/textures/sumo.txt` (`sumo@move.1`–`.19`), damit der Cross-File-Test grün bleibt.
4. Führe `uv run boku lint` aus und behebe **jeden einzelnen** `array-width`-, `array-lines`-, `array-bytes`- oder `unencodable`-Befund, bis **0 Fehler** für `arrays.txt` gemeldet werden!
5. Aktualisiere `translation/status.tsv` für `arrays`.

---

## 4. Abnahmekriterien (Definition of Done)

- [ ] Alle 314 Einträge in `translation/days/arrays.txt` sind auf Deutsch übersetzt (`ae/oe/ue/ss`, keine japanischen Zeichen).
- [ ] `uv run boku lint` meldet **0 Fehler** auf `arrays.txt`.
- [ ] `uv run pytest` läuft komplett grün durch.
- [ ] Falls Begriffe aus Platzgründen angepasst wurden, sind sie rückwirkend in `translation/glossary.md` aktualisiert, damit Stufe 5 & 6 dieselben Begriffe nutzen.
- [ ] **Fortschrittsbericht** `plan/progress/04-ui-menues-und-arrays.md` wurde erstellt und `plan/README.md` aktualisiert.

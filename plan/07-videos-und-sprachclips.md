# Stufe 7: FMV-Untertitel, Titelsong & Epiloge (`movies.txt` & `clips.txt`)

**Ziel:** Übersetzung und exakte Zeit-/Lesegeschwindigkeits-Abstimmung aller **89 zeitkritischen Audio-/Video-Untertitel** in `translation/movies.txt` (43 Cues) und `translation/clips.txt` (46 Cues).

---

## 1. Teil A: Die Film-Untertitel & der Titelsong (`translation/movies.txt`, 43 Einträge)

### Was enthalten ist:
- **`M27` (Intro-Film):** Vaters Satz am Autoradio, der große Eröffnungs-Monolog des erwachsenen Boku im Sommerflimmern, Bokus stiller Gedanke im schwarzen Bild (`caption`) und der **Titelsong** über den Credits (`panel`).
- **`M28` (Abspann-Film):** Schlusssatz des Erzählers + zweite Strophe des **Titelsongs** (`panel`).
- **`M60` (Feuerwerk, Tag 8):** Erzählermonolog am Fenster.
- **`M120` (Satellit, Tag 10):** Erzählermonolog, dessen Satz über das Video-Ende hinausläuft und in `day10.txt` (`E1008.0`) vollendet wird!
- **`M260` (Sonnenblumen-Traum, Tag 29):** Der traurige Winterwind-/Wolf-Traum.

### Strenge technische Regeln für `movies.txt` (geprüft von `boku lint` & `movie-timing`):
1. **Maximal 2 Zeilen à maximal 318 Pixel** pro Cue! Manueller Zeilenumbruch mit ` | ` (sonst bricht der Builder automatisch um).
2. **Erzähler-Klammern `『 』` (`cue-marks`):**
   - Im Gegensatz zu den Tagesdateien trägt `movies.txt` die Klammern `『` und `』` **direkt im Text**, und zwar **genau ein Paar pro ganzem Satz**, auch wenn sich der Satz über 4 oder 5 Cues erstreckt (`『` ganz am Anfang des ersten Cues des Satzes, `』` ganz am Ende des letzten Cues des Satzes, keine dazwischen!).
   - Gesang (Titelsong), Vaters Satz am Radio und `caption` bekommen **keine** `『 』`!
3. **Lesegeschwindigkeit (max. 17 Zeichen/Sekunde, min. 1,5 s Standzeit):**
   - Deutsch hat durch `ae/oe/ue/ss` manchmal ein paar Buchstaben mehr pro Sekunde.
   - Falls ein Cue über **17 Zeichen/Sekunde** liegt, wird nichts gekürzt, sondern entweder die Frame-Spanne im Rahmen der Sprechpause minimal angepasst oder ein zu dichter Cue sauber auf zwei aufeinanderfolgende Cues verteilt — geprüft mit `uv run boku lint` (und sofern `work/voice/reviewed` vorliegt, `uv run python -m boku.movie_timing`).
4. **Nahtloser Satzübergang `M120` → `E1008.0`:**
   - Der letzte Cue von `M120` (`91–152`) und `E1008.0` in `day10.txt` **müssen** gemeinsam als ein einziger grammatikalisch perfekter deutscher Satz gelesen werden! (Im Deutschen darauf achten, dass die Verbstellung am Satzende nicht holpert, z. B.: `M120`: *„...eingehuellt in Pflichtgefuehl | und tiefe Einsamkeit, zog er dahin..."* → `E1008.0`: *„...ein Satellit, der lautlos wie im Gleitflug weiterflog."*).

---

## 2. Teil B: Die Code-gesteuerten Sprachclips & 5 Epiloge (`translation/clips.txt`, 46 Einträge)

### Was enthalten ist:
1. **`XCH.34`:** Erzähler-Satz beim Einschlafen in der allerersten Nacht (*„Und so ging der erste Tag jener Sommerferien zu Ende."*).
2. **`XCH.41`–`XCH.45` (Die 5 Epiloge nach dem Abspann!):**
   - Je nach gesammelten Erfahrungs-Sternen hört man einen von 5 großen Lebens-Epilogen des erwachsenen Boku (Schwestern in der Stadt / Boku wird Töpfer / Boku als Programmierer im Großraumbüro / Boku als Schriftsteller in New York kurz vor 2001 / Das Dorf Tsukiyono versinkt 15 Jahre später in einem Staudamm).
   - **KRITISCH — Zeitstempel-Spalte (Feld 4):** Jeder Epilog hat am Zeilenende exakte Sekundenwerte pro Seite (z. B. `5.3 12.2 15.0 18.1 24.2`), wann die jeweilige Seite weiterschaltet — und die **allerletzte Seite MUSS verschwinden, bevor das Bild auf die Sony-Produktionskarte (`OTI`) wechselt!** (`epilogue`-Check im Linter!).
   - Jede Seite muss ≥ 1,5 Sekunden stehen und ≤ 17 Zeichen/Sekunde haben!
3. **`XCH.00`–`XCH.33`, `XCH.35`–`XCH.40` (Käfer-Sumo-Kommentare):**
   - Die Live-Rufe von Guts, Fat und Brille während der Käfer-Sumo-Kämpfe!
   - **Achtung schmalere Box:** Im Käfer-Sumo steht links Bokus Porträt, daher ist die Box hier **42 Pixel schmaler** (`boku.clip_subs.clip_box`) — der Linter misst das automatisch mit!
   - Charakter-Konsistenz wahren: Fat nutzt seinen typischen Ausdruck aus dem Glossar (*„Meine Wenigkeit ist zuerst dran!"*).

---

## 3. Arbeitsschritte für den Agenten

1. Übersetze `translation/movies.txt` komplett ins Deutsche (`ae/oe/ue/ss`, `『 』`-Satzklammern exakt prüfen, `M120` mit `day10.txt` `E1008.0` abgleichen).
2. Übersetze `translation/clips.txt` komplett ins Deutsche, unter Beibehaltung der Seitenanzahl und Zeitstempel bei `XCH.41`–`XCH.45` (oder feinjustiere Seitenbrüche/Sekunden, falls ein deutscher Teilsatz > 17 cps hat, streng innerhalb des Produktionskarten-Limits!).
3. Prüfe alles hart mit dem Linter:
   ```powershell
   uv run boku lint
   ```
   *(Behebe jeden `cue-*`-, Breiten-, CPS- oder Epilog-Timing-Befund bis **0 Fehler**!)*
4. Aktualisiere `translation/status.tsv` für `movies` und `clips`.

---

## 4. Abnahmekriterien (Definition of Done)

- [ ] Alle 43 Cues in `translation/movies.txt` und alle 46 Cues in `translation/clips.txt` sind auf Deutsch übersetzt (`ae/oe/ue/ss`).
- [ ] `M120` → `E1008.0` bildet einen nahtlosen deutschen Satz.
- [ ] Alle 5 Epiloge (`XCH.41`–`XCH.45`) halten das 17-cps-Limit und verschwinden rechtzeitig vor der Produktionskarte (`uv run boku lint` meldet **0 Fehler**).
- [ ] `uv run pytest` läuft komplett grün durch.
- [ ] **Fortschrittsbericht** `plan/progress/07-videos-und-sprachclips.md` wurde erstellt und `plan/README.md` aktualisiert.

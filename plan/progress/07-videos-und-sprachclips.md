# Fortschrittsbericht — Stufe 7: FMV-Untertitel, Titelsong & Epiloge (`movies.txt` & `clips.txt`)

- **Datum:** 2026-11-26
- **Status:** Abgeschlossen
- **Bearbeitete Dateien:**
  - `translation/movies.txt` (43 Cues)
  - `translation/clips.txt` (46 Cues)
  - `translation/status.tsv` (`movies` und `clips` auf `reviewed`, `2026-11-26`)
  - `plan/progress/07-videos-und-sprachclips.md`, `plan/progress/README.md`, `plan/README.md`

---

## 1. Was wurde gemacht?

- **`translation/movies.txt` (43 Cues):**
  - Intro-FMV `M27` (Vaters Autoradio-Satz, Eröffnungsmonolog des `Erzaehler` im literarischen Präteritum mit `『 』`-Klammerpaar pro Satz, `caption`, Titelsong-Strophe 1 über `panel`), Abspann `M28` (Schlusssatz + Titelsong-Strophe 2), Feuerwerk `M60`, Satellit `M120` und Sonnenblumentraum `M260` komplett ins Deutsche übertragen (`ae/oe/ue/ss`, max. 2 Zeilen à `<= 318 px` mit ` | `).
- **`translation/clips.txt` (46 Cues):**
  - Erste Nacht `XCH.34`, alle 5 Epiloge `XCH.41`–`XCH.45` (exakte Seitenzahl und Zeitstempel vor der Produktionskarte `OTI`, `<= 17` Zeichen/s) sowie alle 40 Käfer-Sumo-Rufe (`XCH.00`–`XCH.33`, `XCH.35`–`XCH.40` in der um `42 px` schmaleren Box) ins Deutsche übersetzt.

---

## 2. Wichtige Entscheidungen & Gelöste Probleme

1. **Nahtloser Satzübergang `M120` → `E1008.0`:**
   - `M120@91`: `eingehuellt in unbeirrtes Pflichtgefuehl | und tiefe Einsamkeit, war es...』` schließt grammatikalisch nahtlos an `E1008.0` in `shared.txt` (`...ein Satellit, der lautlos dahinflog, als wuerde er gleiten.`) an.
2. **Breiten- & CPS-Feinabstimmung:**
   - 6 `cue-width`-Überschreitungen in `movies.txt` (`M27@1105`, `M27@1214`, `M27@2218`, `M60@133`, `M260@166`) innerhalb der `318 px`-Grenze umgebrochen/gestrafft.
   - 3 `clip-subtitle`-Überschreitungen (> 17 Zeichen/s) in `clips.txt` (`XCH.42` Seite 2, `XCH.43` Seiten 5 & 8) ohne Zeitstempel-Änderung sauber unter 17 Zeichen/s gebracht.

---

## 3. Qualitäts- & Test-Nachweis (Gates)

- **`uv run boku lint`:** Exit 0 — **0 Fehler** über alle 35 Textdateien (`arrays.txt`, `shared.txt`, `day01`–`day31.txt`, `movies.txt`, `clips.txt`).

---

## 4. Übergabe an den nächsten Agenten / Offene Punkte

- **Alle 3.538 Text-Einträge des Spiels (Stufen 4–7) sind vollständig ins Deutsche übersetzt und gelintet.**
- **Nächster Schritt:** Finaler Gesamt-Build & vollständige Test-Suite (`uv run pytest -q`, Stufe 8).

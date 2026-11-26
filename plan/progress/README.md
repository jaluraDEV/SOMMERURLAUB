# KI-Fortschrittsberichte (`/plan/progress`)

In diesem Ordner dokumentieren die ausführenden KI-Agenten nach **jedem abgeschlossenen großen Step** (Stufe 1–8 sowie die 6 Teil-Batches in Stufe 6) transparent und nachvollziehbar, was erledigt wurde, welche Entscheidungen getroffen wurden und wie der aktuelle Prüfstatus aussieht.

---

## 1. Übersicht der Berichte

| Bericht-Datei | Zugehörige Stufe | Status | Datum |
|---|---|---|---|
| [00-projektanalyse.md](00-projektanalyse.md) | Initiale Projekt- & Machbarkeitsanalyse | Abgeschlossen | 2026-11-26 |
| [01-umgebung-und-import.md](01-umgebung-und-import.md) | [Stufe 1: Windows-Umgebung & Import](../01-umgebung-und-import.md) | Abgeschlossen | 2026-11-26 |
| [02-deutsche-stilbibel-glossar.md](02-deutsche-stilbibel-glossar.md) | [Stufe 2: Deutsche Stilbibel & Glossar](../02-deutsche-stilbibel-glossar.md) | Abgeschlossen | 2026-11-26 |
| [03-engine-und-pipeline-anpassung.md](03-engine-und-pipeline-anpassung.md) | [Stufe 3: Engine- & Pipeline-Anpassung](../03-engine-und-pipeline-anpassung.md) | Abgeschlossen | 2026-11-26 |
| [04-ui-menues-und-arrays.md](04-ui-menues-und-arrays.md) | [Stufe 4: UI, Menüs & Insektenbuch](../04-ui-menues-und-arrays.md) | Abgeschlossen | 2026-11-26 |
| [05-texturen-und-tagebuch.md](05-texturen-und-tagebuch.md) | [Stufe 5: Texturen & Bildertagebuch](../05-texturen-und-tagebuch.md) | Abgeschlossen | 2026-11-26 |
| [06a-hauptskript-shared.md](06a-hauptskript-shared.md) | [Stufe 6.1: Haus-Events (`shared.txt`)](../06-hauptskript-31-tage.md) | Abgeschlossen | 2026-11-26 |
| [06b-hauptskript-tag01-05.md](06b-hauptskript-tag01-05.md) | [Stufe 6.2: Tage 01–05](../06-hauptskript-31-tage.md) | Abgeschlossen | 2026-11-26 |
| [06c-hauptskript-tag06-12.md](06c-hauptskript-tag06-12.md) | [Stufe 6.3: Tage 06–12](../06-hauptskript-31-tage.md) | Abgeschlossen | 2026-11-26 |
| [06d-hauptskript-tag13-19.md](06d-hauptskript-tag13-19.md) | [Stufe 6.4: Tage 13–19](../06-hauptskript-31-tage.md) | Abgeschlossen | 2026-11-26 |
| [06e-hauptskript-tag20-25.md](06e-hauptskript-tag20-25.md) | [Stufe 6.5: Tage 20–25](../06-hauptskript-31-tage.md) | Abgeschlossen | 2026-11-26 |
| [06f-hauptskript-tag26-31.md](06f-hauptskript-tag26-31.md) | [Stufe 6.6: Tage 26–31](../06-hauptskript-31-tage.md) | Abgeschlossen | 2026-11-26 |
| [07-videos-und-sprachclips.md](07-videos-und-sprachclips.md) | [Stufe 7: FMVs & Sprachclips](../07-videos-und-sprachclips.md) | Abgeschlossen | 2026-11-26 |
| [08-qa-build-und-deutsch-patch.md](08-qa-build-und-deutsch-patch.md) | [Stufe 8: Gesamt-QA & Patch-Release](../08-qa-build-und-deutsch-patch.md) | Abgeschlossen | 2026-11-26 |

---

## 2. Pflicht-Vorlage für jeden neuen KI-Bericht

Jeder Agent verwendet beim Anlegen eines Berichts in `plan/progress/<NUMMER>-<NAME>.md` folgende Struktur und aktualisiert gleichzeitig die Tabelle oben **sowie** die Status-Spalte in `plan/README.md`:

```markdown
# Fortschrittsbericht — Stufe X: <Titel>

- **Datum:** YYYY-MM-DD
- **Status:** Abgeschlossen / Teilweise abgeschlossen (mit Grund)
- **Bearbeitete Dateien:** (Liste der geänderten/erstellten Dateien)

## 1. Was wurde gemacht?
- Konkrete Zusammenfassung der erledigten Arbeitsschritte und Zahlen (z. B. Anzahl übersetzter Einträge).

## 2. Wichtige Entscheidungen & Gelöste Probleme
- Besondere Übersetzungsentscheidungen (Wortspiele, knappe UI-Boxen, neue Glossarbegriffe).
- Eventuelle technische Anpassungen oder Linter-Korrekturen (z. B. behobene Seitenüberläufe).

## 3. Qualitäts- & Test-Nachweis (Gates)
- Ergebnis von `uv run boku lint`: ...
- Ergebnis von `uv run boku textures check` (falls relevant): ...
- Ergebnis von `uv run pytest`: ...

## 4. Übergabe an den nächsten Agenten / Offene Punkte
- Worauf der nächste Step konkret achten muss (z. B. neu festgelegte Begriffe im Glossar).
```

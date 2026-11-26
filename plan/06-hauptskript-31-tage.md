# Stufe 6: Hauptskript — Haus-Events & Alle 31 Sommertage (`translation/days/`)

**Ziel:** Übersetzung des gesamten szenischen Dialogskripts (**2.835 Einträge** verteilt auf `shared.txt` mit 750 Zeilen und `day01.txt`–`day31.txt` mit 2.085 Zeilen) in höchster literarischer und charaktertreuer Qualität — gesteuert in **6 überschaubaren Batches** mit jeweils eigenem Zwischenbericht unter `plan/progress/`!

---

## 1. Die Dual-Source-Methode (Warum unsere KI-Übersetzung besser wird als blindes MT)

Für jede Szene (`E0171`, `E0173`, ...) füttern wir den Übersetzungs-Agenten mit **beiden Quellen gleichzeitig**:
1. **Dem japanischen Originalskript + Szenen-Flussgraphen** (generiert via `uv run boku packet --game` unter `work/packets/game/`): Zeigt den exakten japanischen Wortlaut, wer im Raum steht, welche Verzweigungen (`[SEL]`) wohin führen und welche Zeilen dieselbe Sprachaufnahme teilen!
2. **Der geprüften englischen Übersetzung + allen `# NOTE`-Kommentaren** (`work/english-reference/days/`): Dort sind bereits alle versteckten Anspielungen, japanischen Homophone, Kinder-Versprecher, Sprecherwechsel und Zeitbezüge aufgeschlüsselt!

**Goldene Regel beim Übersetzen:**
- Übersetze den **Sinn und Ton des Japanischen** direkt in natürliches, idiomatisches Deutsch (keine wörtlichen Anglizismen aus dem Englischen übernehmen!).
- Prüfe gegen die englische Vorlage + `# NOTE`, dass **keine Nuance, kein Witz und kein Story-Hinweis** verloren geht.

---

## 2. Eiserne Format- & Technikregeln für `dayNN.txt` & `shared.txt`

1. **Zeilenformat:** `ID <TAB> Deutscher_Sprecher <TAB> Deutscher_Text`
   - Jede ID aus der Datei muss exakt einmal vorkommen, in derselben Reihenfolge.
2. **Seitenumbrüche (` // `) sind bei vertonten Zeilen HEILIG:**
   - Vertonte Zeilen schalten ihre Textseiten nach einem festen Frame-Countdown der Audio-Datei um (`page-count`-Regel in `boku/lint.py`).
   - Deshalb **muss** jede vertonte Zeile exakt dieselbe Anzahl an ` // `-Umbrüchen an inhaltlich derselben Stelle des gesprochenen Satzes haben wie das Original!
   - Innerhalb einer Seite wird Fließtext ohne Zeilenumbruch geschrieben (der VWF-Wrapper bricht automatisch auf bis zu 3 Zeilen im Dialogband um).
3. **Auswahlmenüs (`[SEL]`):**
   - Optionen getrennt durch ` | `, exakt gleiche Anzahl und Reihenfolge wie im Original! Wenn vor den Antworten eine Frage in derselben Box steht, ist sie das erste Feld.
   - Keine Option darf breiter als `select-width` sein (eine Auswahlzeile kann nicht umbrechen!).
4. **`(voice only)`-Zeilen:**
   - Zeilen ohne Text auf der Disc bleiben exakt `(voice only)` — **außer** die englische Referenz hat hinter einem weiteren Tabulator bereits den eingesprochenen Untertiteltext (z. B. beim Erzähler am Brunnen): Dann wird dieser Untertitel ins Deutsche übersetzt!
5. **Keine äußeren Anführungszeichen um Dialoge:**
   - Der Renderer setzt `Onkel「...」` bzw. `『...』` (beim `Erzaehler`) automatisch! Gerade `"..."` nur für zitierte Begriffe im Satz (`Es wird "Gedicht" geschrieben und "Shirabe" ausgesprochen.`).
6. **ASCII-Umlaute (`ae`, `oe`, `ue`, `ss`) & Keine japanischen Schriftzeichen:**
   - Auch in `# NOTE`-Kommentaren dürfen keine Kanji/Kana stehen (`test_translation_has_no_japanese.py`), japanische Wörter in Kommentaren immer in Romaji schreiben!
   - Alte englische `# VOICE ...`-Kommentare werden entfernt oder (falls nötig) sauber ersetzt.
7. **Wiederkehrende Sprachaufnahmen konsistent halten:**
   - Manche Zeilen teilen sich exakt dasselbe Audio-Sample (z. B. Onkels Ruf zum Abendessen `E0190.0` und `exe@80029920.0`, oder das Abendessen-Gebet *„Itadakimasu!"* / *„Gochisosama deshita."*). Diese müssen identisch übersetzt werden!

---

## 3. Aufteilung in 6 kontrollierte Batches (mit Zwischenberichten!)

Da Deutsch im Schnitt **ca. 10–15 % länger** als Englisch ist (insbesondere mit `ae/oe/ue/ss`), übersetzen wir niemals blind alle 32 Dateien auf einmal, sondern in **6 chronologischen Batches** mit sofortigem `uv run boku lint`-Check nach jedem Batch:

| Batch | Dateien | Inhalt & Story-Bogen | Einträge | Fortschrittsbericht |
|---|---|---|---|---|
| **Batch 6.1** | `shared.txt` | Alle tagesunabhängigen Haus-Events: 60+ Untersuchungs-Texte im Haus, Bad, Kühlschrank, Bücherregal, Abendessen-Quiz & Antworten, Schlafenszeit | **750** | `progress/06a-hauptskript-shared.md` |
| **Batch 6.2** | `day01.txt` – `day05.txt` | Ankunft bei Familie Sorano, Vorstellungsrunde, erstes Käfernetz, Kennenlernen von Guts & Geheimbasis, Glühwürmchen-Nacht | **425** | `progress/06b-hauptskript-tag01-05.md` |
| **Batch 6.3** | `day06.txt` – `day12.txt` | Käfer-Sumo-Einführung, Feuerwerk (Tag 8 — Achtung Übergang zu Movie `M60`!), Satellit (Tag 10 — Übergang aus Movie `M120` in `E1008.0`!), Brief & Masern-Wortspiel | **399** | `progress/06c-hauptskript-tag06-12.md` |
| **Batch 6.4** | `day13.txt` – `day19.txt` | Halbzeit der Ferien, Gräberbesuch (Obon), Wolfsmädchen-Gerücht, **erstes Treffen mit Saori (`E1861`: „Ich bin Boku" / „Ich bin ich"-Wortspiel!)** | **385** | `progress/06d-hauptskript-tag13-19.md` |
| **Batch 6.5** | `day20.txt` – `day25.txt` | Sternschnuppen, **der historische Schuljungen-Brief aus dem Frühling Showa 17 (`E2303.7`, 13 Seiten!)**, **Onkels Tanka-Gedicht (`E2515.0` mit ` / `-Versbrüchen!)** | **419** | `progress/06e-hauptskript-tag20-25.md` |
| **Batch 6.6** | `day26.txt` – `day31.txt` | Geheimnis um Onii-chan, zweites Tanka (`E2712.0`), Saoris Abreise, Geburt des kleinen Bruders (Tag 29), großer Abschied (Tag 30) & Abreisetag (Tag 31) | **457** | `progress/06f-hauptskript-tag26-31.md` |

---

## 4. Umgang mit Längen-Überläufen (`page-lines` > 3) im Deutschen

Wenn `uv run boku lint` nach einem Batch meldet:
`E0185.0 page 1: 4 lines in dialogue band, which holds 3`
gilt folgende klare Reihenfolge:
1. **Ist die Zeile unvertont (`MSG`)?** → Wir dürfen einen zusätzlichen Seitenumbruch ` // ` einfügen (`page-count-unvoiced` ist nur ein Hinweis, kein Fehler).
2. **Ist die Zeile vertont (`XAMSG`, feste Seitenanzahl)?** → Prüfe, ob eine umständliche deutsche Nebensatzkonstruktion natürlicher und prägnanter formuliert werden kann, **ohne irgendeine Information des Japanischen wegzulassen** (z. B. *„in der Lage sein zu"* → *„koennen"*, Perfekt → Präteritum beim Erzähler, natürliches gesprochenes Kinderdeutsch statt Schachtelsatz). In 99 % der Fälle spart gutes, idiomatisches Deutsch sofort 15–25 Pixel und rutscht sauber von 4 auf 3 Zeilen!

---

## 5. Besondere Schlüssel-Szenen (Pflicht-Augenmerk!)

- **`E1008.0` (Tag 10, Satellit):** Setzt den unvollendeten Satz aus Video `M120` fort! Muss nahtlos an den letzten Untertitel von `M120` in `movies.txt` anschließen (*„...ein Satellit, der lautlos dahinflog..."*).
- **`E1861.3`–`.5` & `.27` (Tag 18, Saori):** Boku sagt *„Ich heisse Boku"* / *„Ich bin Boku"*; im Japanischen klingt *„Boku wa boku da yo"* wie *„Ich bin ich"*, worauf Saori ihn neckisch „Boku-kun" tauft. Im Deutschen den Namen *Boku* beibehalten und in `# NOTE` / Formulierung sicherstellen, dass ihr Missverständnis (*„‚Boku‘ heisst doch einfach ‚ich‘! Na gut, dann nenn ich dich eben Boku-kun!"*) natürlich funktioniert!
- **`E2515.0` & `E2712.0` (Tag 25 & 27, Onkels Tanka):** Beide Vorkommen identisch halten, die 5 Kurzverse mit ` / ` gliedern und die Doppeldeutigkeit (*Herbstwind / Brennofen / verlorener Sohn* + Wortspiel *utsuwa* = Gefäß / menschliche Größe) bewahren!

---

## 6. Abnahmekriterien (Definition of Done)

- [ ] `shared.txt` und alle `day01.txt`–`day31.txt` sind vollständig auf Deutsch übersetzt (`ae/oe/ue/ss`).
- [ ] Alle 6 Teil-Berichte (`06a` bis `06f`) liegen unter `plan/progress/` vor.
- [ ] Unabhängiger **Review-Pass** gegen das japanische Original (`uv run boku packet --like <FILE>`) auf Sinnfehler, vergessene Details oder unnatürliches Deutsch durchgeführt.
- [ ] `uv run boku lint` meldet **0 Fehler** über alle 32 Dateien in `translation/days/`!
- [ ] `translation/status.tsv` ist für `shared` und `day01`–`day31` aktualisiert.
- [ ] `plan/README.md` ist aktualisiert.

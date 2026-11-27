# Deutsche Pruef-Checkliste (`boku-ps1-de`)

Kompakte Endkontrolle fuer alle Uebersetzungs- und Pruef-Laeufe (Stufen 4–7). Diese Liste ergaenzt keine neuen Regeln, sondern fasst die haeufigsten Fehlerquellen aus [style-guide.md](style-guide.md) und [glossary.md](glossary.md) zusammen; im Zweifel gilt stets die Stilbibel bzw. das Glossar. Lizenz: CC BY-SA 4.0 (`LICENSE-translation`).

## Global (Stufen 4–7)

* **Echte Umlaute/`ß` (seit v1.1.0, Stilbibel § 9):** Echte `ä, ö, ü, Ä, Ö, Ü, ß` im Spieltext (Ausnahmen: `title@sjis:188` ohne Umlaute/`ß`, Marker `Erzaehler`); weiterhin null `[„“»«]` im Spieltext.
* **Gerade ASCII-Quotes `"..."` nur im Satzinneren (Stilbibel § 9):** Nie `„..."` oder `»...«`, und **niemals** Anfuehrungszeichen um ganze Dialogzeilen (der Renderer zeichnet `Label「...」` bzw. `『...』`).
* **`Du / Ihr / Sie`-Matrix (Stilbibel § 2):** Familie Sorano und Kinder untereinander = `du / ihr`; Boku -> Moench und anfangs Saori = `Sie`; Saori -> Boku = `du` (`Kleiner`, `Knirps`); Saori -> Erwachsene = `Sie`.
* **Exakte 15 `Deutsche Labels` (Stilbibel § 9):** `Boku, Onkel, Tante, Moe, Shirabe, Guts, Fat, Brille, Vater, Moench, Junge, Frau, Saori, Erzaehler, Alle` (Chor kommagetrennt, sonst `(unlabelled)`).
* **`Erzaehler` im literarischen Praeteritum (Stilbibel § 6):** Immer `"ich"`, `"mein Onkel"`, `"meine Tante"`, `"mein Vater"`, `"meine Mutter"`; keine Verkuerzungen, kein erfundenes *"Damals wusste ich noch nicht..."*.
* **Glossar & verbale Tics wortgetreu (Stilbibel § 4, § 5, § 7, Glossar):** Insekten, Fische, Drachen, Items, Orte, Speisen, `Itadakimasu!`, `Gochisosama deshita.`, `Bye-yoyooon!`, `Ubli-bubli-bon`, `Hicks!`, `Hm-hm`, `Geh-heh-heh` buchstabengenau wie festgelegt.
* **Interjektionen & Lachen (Stilbibel § 7, Glossar § 8):** *un* -> `"Ja"` / `"Mhm"`, *are?* -> `"Huch?"` / `"Moment..."`, *ee?* -> `"Hae?"`, *hee* -> `"Ohh"`; *fufu* -> `"Hm-hm"`, *gehehe* -> `"Geh-heh-heh"`.
* **Nichts dazuerfinden, nichts weglassen (Stilbibel § 0, § 13):** Keine Fuellwoerter (*eigentlich, halt, eben, wirklich*) ohne Originalbasis; kleine Partikeln (*mo* = `auch`, *dake* = `nur`) uebersetzen.
* **Zeichensetzung & Emphase (Stilbibel § 9, § 18):** Kein Gedankenstrich `—` ausser bei echtem Abbruch im Original; `...` immer dreifach; GROSSBUCHSTABEN nur sparsam fuer Schreien; kein `–` (Halbgeviertstrich).
* **Null japanische Schriftzeichen (Stilbibel § 3):** Weder Kanji noch Kana in Spielzeilen oder `# NOTE` / `# UNSURE` — nur Romaji ohne Makrons.

## Stufe 4 (`arrays.txt`)

* **Sonderzeichen & Zaehler erhalten:** `000` am Anfang von `exe@80029AFC.0` (Zellen 1–3) sowie `{G:n}`, `○`, `×`, `↓`, `♂`, `♀` unveraendert lassen.
* **`[SEL]` & Code-Labels:** ` | ` in exakter Optionenzahl; `SN` fuer `exe@code:800377F8`; `{slot}` vor `{day}` in `title@sjis:188` (`<= 64` Bytes Shift-JIS); `title@7A78.0` = `Ja | Nein`.
* **Breiten & Sumo-Sync:** `exe@8003D2E0.23`–`.29@exchange` (`<= 98-px`), `exe@80046214.*` (`<= 115-px`), `exe@8003DA4C.*` (`<= 91-px`, `Forelle`), `exe@8003DA00.*` (`<= 109-px`, `.5 <= 134-px`); `musi@2C.13`–`.31` & `musi@358.0`–`.2` buchstabengenau identisch zu `textures/sumo.txt`.

## Stufe 5 (`textures/*.txt`)

* **`GameFace`-Verbote:** **Keine `"`** und **keine `(` / `)`** in `GameFace`-Texturen (`diary.txt`, `ui.txt`, `signs.txt`, `sumo.txt`, `kite.txt`, `mzkan@*.name`, `tzkan@*.name`, Stein-/Abzeichen-Buttons)!
* **`Bean` / `Sprout` & Umbrueche:** Kein `%` in `Bean` oder `Sprout`; kein ` // ` in einzeiligen bzw. Absatz-Texturen (`diary.txt`, `sumo.txt`, `kite.txt`, `records.txt`, `books.txt`, `T_TITLE`, `OTI`, `M_C15`, `T_CONFIG` ausser `sub_screen`).
* **Box-Grenzen:** `diary.txt` max. 5 Zeilen (`<= 215-px`) in kurzen Drittklaessler-Saetzen; `sumo.txt` Glossen `<= 122-px` fett ohne vertikale Beruehrung, `plate.stamina <= 48-px` (`Energie`), `T_CONFIG.heading <= 50-px` (`Menue`/`Setup`, nicht *Optionen*), `kite@hud.* <= 30 / 38 / 46-px`; `uv run boku textures check --out work/textures-de` mit 0 Fehlern.

## Stufe 6 (`shared.txt`, `day01`–`day31.txt`)

* **` // ` & `(voice only)`:** Seitenumbrueche ` // ` bei vertonten Zeilen (`XAMSG`) in Anzahl und Reihenfolge exakt beibehalten; bei unvertonten (`MSG`) nur ` // ` ergaenzen, falls > 3 Zeilen. `(voice only)` unveraendert lassen (ausser Untertitel hinter zweitem Tab).
* **Kontinuitaet & Wortspiele:** `E1008.0` nahtlos an `movies.txt` `M120` anschliessen; `E2515.0` & `E2712.0` (Tanka ` / `) wortgleich halten; alle 23+1 Wortspiele strikt gemaess `glossary.md` § 9 umsetzen.

## Stufe 7 (`movies.txt`, `clips.txt`)

* **`movies.txt`:** Erzaehler-Untertitel tragen `『 』` direkt im Text (1 Paar pro Satz, keine bei Lied/Vater/Tafel), max. 2 Zeilen x `318-px` (` | `), `<= 17` Zeichen/s, `>= 1,5` s, `M120` geht nahtlos in `E1008.0` ueber.
* **`clips.txt`:** Sumo-Cues (`XCH.00`–`.40`) nutzen das um `42-px` schmalere Feld (`230 / 196-px`); die 5 Epiloge (`XCH.41`–`.45`) bleiben `<= 17` Zeichen/s, und ihre letzte Seite endet vor der `ENDOTI`-Tafel.

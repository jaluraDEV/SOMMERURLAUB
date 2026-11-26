# Stufe 2: Deutsche Stilbibel, Anrede-Regeln & Glossar

**Ziel:** Bevor eine einzige Spielzeile übersetzt wird, definieren wir ein verbindliches deutsches Regelwerk (`translation/style-guide.md` und `translation/glossary.md` angepasst auf Deutsch, plus `translation/checklist.md`), damit alle 31 Tage, alle Texturen und alle Charakterstimmen wie aus einem Guss klingen.

---

## 1. Grundcharter der deutschen Übersetzung

Wir folgen dem bewährten Geist des Projekts (**„Übersetzen, nicht verwestlichen"**):
- Das Spiel spielt im August 1975 im ländlichen Nord-Kanto (Japan), und die japanische Sprachausgabe bleibt hörbar.
- Was das Ohr deutlich hört (Namen, bestimmte Suffixe, *Itadakimasu!*), soll das Auge auf Deutsch nicht widersprechen.
- Gleichzeitig muss das Deutsch **natürlich, warm, lebendig und altersgerecht** klingen — kein steifes „Übersetzungs-Englisch" (keine Anglizismen wie *„Ich sehe"* für *„Ach so"* oder *„Hab eine gute Zeit"*).

---

## 2. Technische Schreib- & Zeichensatzregeln (`ae`, `oe`, `ue`, `ss`)

Da wir bewusst ohne Font-Umbau arbeiten, gelten für **ausnahmslos alle** Spieltexte (Dialoge, Menüs, Texturen, Tagebuch, Filme, Memory Card) folgende Regeln:

| Zeichen | Ersetzung im Spieltext | Beispiele |
|---|---|---|
| `ä` / `Ä` | `ae` / `Ae` | *Kaefer, Raeume, Maedchen, Aehre, spaet* |
| `ö` / `Ö` | `oe` / `Oe` | *schoen, koennen, Kroete, Oel, Loewe* |
| `ü` / `Ü` | `ue` / `Ue` | *fuer, gruen, Tuer, Muetze, Uebung* |
| `ß` | `ss` | *gross, Strasse, heiss, draussen, Spass* |
| `„..."` / `»...«` | `"..."` (gerade ASCII-Quotes) | Nur für zitierte Wörter *innerhalb* eines Satzes (`Es wird "Gedicht" geschrieben`). Niemals um die ganze Sprechzeile! |
| `–` (Gedankenstrich) | `...` oder `-` / `--` | Wie im Original sparsam; Auslassungspunkte immer dreifach `...` |

> **Wichtig:** Achte bei zusammengesetzten Wörtern oder Wortstämmen auf saubere Rechtschreibung vor der Umwandlung (z. B. *Räume → Raeume*, nicht *Raueme*; *Bäume → Baeume*; *läuft → laeuft*). In Stufe 3 bauen wir einen automatischen Linter-Check, der versehentlich stehengebliebene echte Umlaute (`äöüÄÖÜß`) sofort meldet!

---

## 3. Zu klärende & festzulegende Stil-Entscheidungen

### 3.1 Anrede & Du/Sie-System (1975, Familie vs. Fremde)
Im Deutschen haben wir gegenüber dem Englischen einen riesigen Vorteil: **Du vs. Sie** bildet japanische Höflichkeitsstufen viel natürlicher ab!
- **Innerhalb der Familie Sorano:** Alle duzen sich gegenseitig (*du / ihr*).
- **Kinder untereinander** (Boku, Shirabe, Guts, Fat, Specs): Immer *du*.
- **Boku zu fremden Erwachsenen:**
  - Zum Mönch (*O-bō-san*): Höfliches **Sie**!
  - Zu Saori (die er anfangs als fremde Frau im Zelt trifft): Anfangs **Sie** (oder schüchternes Sie, bis sie ihn neckt; sie duzt ihn sofort frech als *"Kleiner"* / *"Knirps"*).
- **Verwandtschaftsanreden & Suffixe (analog zum Hybrid-Ansatz):**
  - *Oji-chan / Oji-san* → **Onkel** (auch wenn Onkel Yusaku gegenüber Boku von sich in der 3. Person als *"der Onkel"* oder *"ich"* spricht — im Deutschen klingt *"Onkel schenkt dir das"* / *"Dein Onkel..."* gegenüber einem 9-Jährigen warm, solange man es nicht unnatürlich übertreibt!).
  - *Oba-chan* → **Tante** (im Sprecher-Label `Tante`, in der Anrede `Tante` oder liebevoll `Tante Kaoru`).
  - *Otō-san / Okā-san* → **Papa / Mama** (wenn der erwachsene Erzähler spricht: *mein Vater / meine Mutter*).
  - *Onee-chan / Moe-neechan / Onii-chan* (als Eigenname genutzt): Bleibt wie gehört **Onee-chan**, **Moe-neechan**, **Onii-chan** (essenziell für den Story-Faden um den verstorbenen Sohn!). Beschreibend (*„die große Schwester des Hauses"*) → normal übersetzt (*große Schwester / großer Bruder*).
  - Suffixe *-kun / -chan / -san*: Bleiben wie gehört (**Boku-kun**, **Boku-chan**, **Shirabe-chan**, **Moe-san**, **Gacchan**).
  - Saoris *Kā-san* für die Tante → **Kaa-san**.

### 3.2 Deutsche Sprecher-Labels (`SPEAKER_LABELS`)
Diese stehen vor der Klammer `「...」` direkt im Dialogfenster auf dem Bildschirm (z. B. `Onkel「...」`). Vorschlag für die 15 Labels:

| Englisch (`style-guide.md` § 9) | Deutsch (`SPEAKER_LABELS`) | Hinweis |
|---|---|---|
| `Boku` | `Boku` | Eigenname bleibt |
| `Uncle` | `Onkel` | Kurz & klar (5 Buchstaben wie `Uncle`!) |
| `Aunt` | `Tante` | 5 Buchstaben |
| `Moe` | `Moe` | Eigenname bleibt |
| `Shirabe` | `Shirabe` | Eigenname bleibt |
| `Guts` | `Guts` | Spitzname (hört man im Japanischen als *Gattsu*!) — bleibt `Guts`! |
| `Fat` | `Fat` | Spitzname (hört man im Japanischen als *Fatto*!) — bleibt `Fat`! |
| `Specs` | `Brille` *(oder `Megane` / `Specs`)* | Im JP *Megane*; `Brille` (6 Buchstaben) passt perfekt ins Deutsche |
| `Father` | `Vater` | 5 Buchstaben (kürzer als `Father`!) |
| `Monk` | `Moench` | Mit `oe` (6 Buchstaben) |
| `Boy` | `Junge` | Bevor Guts seinen Namen nennt |
| `Woman` | `Frau` | Bevor Saori ihren Namen nennt |
| `Saori` | `Saori` | Eigenname bleibt |
| `Narrator` | `Erzaehler` | Wird im Spiel **nicht** gezeichnet (nur `『...』`), dient der Datei-Lesbarkeit |
| `All` | `Alle` | Chor-Zeilen |

*(Hinweis: Vor Ausführung von Stufe 2 kann der User kurz abnicken, ob `Guts / Fat / Brille` oder `Guts / Fat / Megane` bevorzugt wird!)*

### 3.3 Charakter-Register auf Deutsch
- **Boku (9 Jahre):** Höflich, neugierig, ein bisschen trocken/altklug-sachlich, kurze gesprochene Kindersätze (*„Echt?", „Au ja!", „Hm, ach so."*). Im Tagebuch (`diary.txt`): Kurze Hauptsätze eines Drittklässlers.
- **Erwachsener Boku (`Erzaehler`):** Ruhiges, leicht literarisches Präteritum (*„An jenem Tag war es drueckend heiss..."*), vollständige Sätze, lange Vergleiche erhalten, niemals *„Boku"*, sondern *„ich"*, *„mein Onkel"*, *„meine Tante"*.
- **Shirabe (8 Jahre):** Altkluges „feines Fräulein"-Deutsch (*„Wie ueberaus schrecklich!", „Also ehrlich", „Shirabe findet..."*), spricht oft von sich in der 3. Person.
- **Moe (15 Jahre):** Ruhig, vernünftig, große-Schwester-Ton, manchmal leise nachdenklich.
- **Guts / Fat / Brille:** Guts knapp und bestimmend; Fat großspurig (*ore-sama* → *„meine Wenigkeit"* / *„der grosse Fat"*); Brille bücherklug, ganze Sätze (*„weisst du"*).
- **Saori (20 Jahre):** Direkt, burschikos zu Boku (*„Kleiner", „Knirps"*), höflich zu den Erwachsenen.

### 3.4 Fachterminologie im Glossar (`glossary.md`)
Im Glossar werden vorab alle wiederkehrenden Begriffe verbindlich festgelegt, damit `arrays.txt`, `books.txt` und alle Dialoge exakt dieselben Namen nutzen:
- **Alle 57 Insektennamen** (z. B. Schwalbenschwanz, Grosser Schillerfalter, Hirschkaefer-Arten wie *Miyama-Hirschkaefer*, *Riesen-Hirschkaefer*, *Saege-Hirschkaefer*, *Nashornkaefer*, Zikaden bleiben wie im Englischen/Japanischen *Min-min-zemi*, *Higurashi*, *Abura-zemi* etc.) + **6 Kurzformen** für das Tausch-Notizbuch (`@exchange`, max. 102 px!).
- **Alle 3 Fischnamen** (*Iwana*, *Regenbogenforelle*, *Yamame*) & Angelbegriffe (*Koeder*, *Pose*, *Fliege*).
- **Alle 8 Drachennamen** (*Rechteckdrachen*, *Nina-Drachen*, *Zikadendrachen*, ...).
- **Alle 15 Inventar-Items** (max. 115 px Breite im Menü!).
- **Sumo-Techniken** (*Oshidashi*, *Uwatenage* bleiben japanische Fachbegriffe + deutsche Kurz-Glossen unter 122 px für `sumo.txt`).
- **25 Wortspiele** aus `bible.md` § Wordplay: Vorab für jedes der 25 Wortspiele (Kinder-Versprecher vs. japanische Homophone wie *chō* / *ame* / *hana*) die exakte deutsche Lösung festlegen!

---

## 4. Arbeitsschritte für den Agenten

1. Lies `work/english-reference/style-guide.md`, `glossary.md`, `bible.md` und `checklist.md` komplett.
2. Übersetze und adaptiere `translation/style-guide.md` auf die deutschen Regeln (inkl. exaktem Satz in § 9 mit der Kommaliste der deutschen `SPEAKER_LABELS`, falls `test_build.py` diesen parst).
3. Erstelle das vollständige deutsche Glossar in `translation/glossary.md` (alle Figuren, Orte, 57 Insekten + `@exchange`-Kurzformen, Items, Fische, Drachen, Sumo-Moves, Verbale Ticks & Wortspiele — alles bereits mit `ae/oe/ue/ss` geprüft!).
4. Aktualisiere `translation/checklist.md` als kompakte Prüf-Checkliste für die Übersetzungs-Agenten (häufigste Fallen, Umlaut-Regel, Anrede-Matrix, feste Begriffe).

---

## 5. Abnahmekriterien (Definition of Done)

- [ ] `translation/style-guide.md`, `translation/glossary.md` und `translation/checklist.md` sind vollständig für Deutsch ausgearbeitet.
- [ ] Alle Menü-kritischen Glossarbegriffe (Items ≤ 115 px, `@exchange`-Käfer ≤ 102 px) wurden bereits rechnerisch gegen die Pixelbreiten geprüft.
- [ ] Keine echten Umlaute (`äöüß`) in den Spieltext-Spalten des Glossars.
- [ ] **Fortschrittsbericht** `plan/progress/02-deutsche-stilbibel-glossar.md` wurde erstellt und `plan/README.md` aktualisiert.

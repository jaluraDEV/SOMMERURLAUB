# Deutsches Glossar (`boku-ps1-de`)

Jeder wiederkehrende Begriff mit verbindlicher deutscher Schreibweise nach [style-guide.md](style-guide.md) (Stand v1.1.0, 2026-11-27). **Alle Spieltexte nutzen echte deutsche Umlaute/`ß` (Ausnahmen: `title@sjis:188` und interner Marker `Erzaehler`), gerade ASCII-Anführungszeichen `"..."` und enthalten null japanische Schriftzeichen (nur Romaji ohne Makrons).** Wo ein Begriff einer technischen Pixelgrenze unterliegt, wurde er direkt gegen `CellMapEncoder` (`build/vwf/edits.json`), `GameFace`, `Bean` bzw. `Sprout` geprüft (`-px` = Pixelbreite).

---

## 1. Personen, Tiere und Laeden

### Sprecher-Labels (`SPEAKER_LABELS`, Stilbibel § 9)
`Boku, Onkel, Tante, Moe, Shirabe, Guts, Fat, Brille, Vater, Moench, Junge, Frau, Saori, Erzaehler, Alle`

### Figuren, Anreden, Spitznamen, Tiere und Laeden

| Romaji | Deutsch | Vermieden / Hinweis | Fundstelle |
|---|---|---|---|
| Boku | Boku | Eigenname und Label; von sich selbst sagt er "ich" (Stilbibel § 1) | Label, 742 Zeilen |
| Boku-kun | Boku-kun | Familie, Brille, Saori (Stilbibel § 2) | `E0174.1` u. 170 mehr |
| Boku-chan | Boku-chan | Guts, Moench | `E0650.4`, `E1203.8` |
| Kubota | Kubota | Bokus Nachname ("Onkel Kubota", wie Moe seinen Vater gruesst) | `E2904.1` |
| Sorano | Sorano | "Himmelsfeld"; Familienname ("bei Soranos") | `E0175.0`, `E0652.2`, `E8013.0` |
| Yusaku / Yu-chan | Yusaku / Yu-chan | Der Onkel; Koseform seiner Frau | `E0175.0`, `E0502.2` |
| oji (Label) | Onkel | Sprecher-Label | Slot 1 |
| oji-chan / oji-san | Onkel | Nicht *Oji-chan*; Anrede und Selbstbezug zu Boku (unter Erwachsenen/allein "ich") | 83 Stellen |
| Kaoru | Kaoru | Die Tante; juengere Schwester von Bokus Vater | `E0182.0` |
| oba (Label) | Tante | Sprecher-Label | Slot 2 |
| oba-chan | Tante (oder Tante Kaoru) | Nicht *Oba-chan*; Anrede und Selbstbezug zu Boku | 76 Stellen |
| Moe | Moe | Zweisilbig ("Mo-e"); stellt sich in Hiragana vor | `E0177.0` |
| Moe-neechan / onee-chan | Moe-neechan / Onee-chan | Nicht *Grosse Schwester* als Name; Eltern nennen Moe ebenfalls `Onee-chan` | `E0652.7`, `E0402.10` |
| Moe-san | Moe-san | Nur Fat, verliebt schmachtend | `E0652.10` |
| Shirabe | Shirabe | Erklaert ihren Namen woertlich: `Es wird "Gedicht" geschrieben und "Shirabe" ausgesprochen.` | `E0140.7`, `E0177.1` |
| Shirabe-chan | Shirabe-chan | Ihre Mutter, Saori | `E2101.4` |
| chibi-musume | Dreikaesehoch | Ihr verhasster Schul-Spitzname (ein Wort, das sie verbieten kann; bei Beschimpfung `Du. Drei. Kaese. Hoch.`) | `E0402.6`, `E0541.1`, `E3042.3` |
| onii-chan | Onii-chan (als Name) / grosser Bruder (beschreibend) | Der verstorbene Sohn hat keinen anderen Namen; Boku wird an Tag 29 zum "grossen Bruder" | `E0121.5`, `E1101.2`, `E2805.9`, `E2907.2` |
| Yuzuki | Yuzuki | Bokus Mutter; Lesung von Shirabe buchstabiert | `E0445.8`–`.9` |
| chichi (Label) | Vater | Label `Vater`; Boku sagt `Papa`, Erzaehler `mein Vater` | Slot 9 |
| oka-san / kaa-chan | Mama | `Erzaehler`: `meine Mutter` | Dialog |
| obo-san | der Moench (Label `Moench`) | Nicht *Priester* (buddhistisch); von Boku gesiezt | `E1202.0` |
| Saori | Saori | Nach Vorstellung | `E1861.26` |
| josei (Label) | Frau | Saori vor ihrer Vorstellung | `E1861.0`–`.27` |
| okami-musume | Wolfsmaedchen | Name der Familie fuer Saori (als Eigenname gross; Silben: `Wolfs... maedchen.`) | `E1701.7` |
| ofuro no onee-san | die Badedame | Shirabes Name fuer Saori | `E1701.0` |
| kaa-san (Saori) | Kaa-san | Saori zur Tante (sie ist nicht ihre Mutter) | `E2004.2` |
| hen na gaki / kuso-gaki | komischer Knirps / Rotzgoere | Saori zu Boku, neckend-herzlich (auch `Kleiner`) | `E1861.6`, `E2760.0` |
| shonen (Label) / shonen ichigo | Junge / Junge Nummer eins | Guts vor Namensnennung; Saori zu Boku | `E0405.2`, `E1861.2` |
| Gattsu / Gatchan | Guts / Gacchan | Im Japanischen als *Gattsu* hoerbar | `E0551.15`, `E0541.7` |
| Fatto | Fat | Im Japanischen als *Fatto* hoerbar; eigene Erklaerung in `E0650.10`–`.11` | `E0650.10` |
| manmosu debu | Mammut-Fetti | Guts' zweiter Spitzname fuer Fat | `E0650.6` |
| ore-sama | meine Wenigkeit | Fats angeberisches Pronomen (9-mal; nur variieren, wo Grammatik zwingt) | `E0650.10` |
| Megane | Brille | Name und Sprecher-Label `Brille` | `E0650.14` |
| yowamushi Megane / futoccho | der Angsthase Brille / der Dicke | Shirabes Beschreibungen (*yowamushi* = Angsthase) | `E0541.7` |
| moyashikko | Bohnenstange | Altmodische Staenkerei fuer ein duennes Stadtkind (alt. `Milchbubi`) | `E0650.2`, `E2952.0` |
| Ken-bo | Ken-bo | Der alte Hund (Genitiv `Ken-bos`, ohne Apostroph) | `E0471.0`, `E0904.9` |
| Nora | Nora | Die Kuh; "Streunerin" — Erklaerung des Onkels uebersetzen | `E1612.2`–`.6` |
| Nora-jirushi gyunyu | Nora-Milch | Kuehlschrank-Menue | `E4029.1` |
| Janbo-san | Jumbo-san | Shirabes Name fuer den Riesenfisch, "Herr des Teichs" | `E2940.0`, `E0904.3` |
| Nakajima-sensei | Nakajima-sensei | Bokus Klassenlehrkraft (Geschlecht ungenannt) | `E1861.27` |
| kyoto-sense | der Konrektor | Moes Englischlehrer, mutmasslicher Autor des Briefes von 1942 | `E0830.8`, `E2204.6` |
| Yamashita-san | Yamashita | Ein Laden in Sagi-no-sato | `E1102.3` |
| Yahaba-ya / Osho Sushi / Fujiyama-Nenryoten / B-Coop | Yahaba-ya / Osho Sushi ("Turm-Set") / Fujiyama-Brennstoffe / der B-Co-op-Laden | Shogi-Witz bei Osho Sushi (`Osho` = Koenig, `Hisha` = Turm -> "das Turm-Set von Osho Sushi"); B-Co-op spielt auf Japans Agrargenossenschaft A-Coop an | `E1331.1`, `E4028.17`, `E8019.0`, `E0705.2` |

---

## 2. Orte (Stilbibel § 3 & § 15)

Siedlungen bleiben japanisch; rein beschreibende Flurnamen werden uebersetzt.

| Romaji | Deutsch | Vermieden / Hinweis | Fundstelle |
|---|---|---|---|
| Tsukiyono | Tsukiyono | Das Tal mit dem Haus ("Mondnacht-Feld") | `E0210.1`, `E2006.1` |
| Tsukiyono-gama | der Tsukiyono-Brennofen | Name der Werkstatt des Onkels | `E0210.1` |
| Sagi-no-sato (mura) | Sagi-no-sato (Dorf) | Nicht *Reiherdorf*; Dorf am Fuss des Berges | `E0001.0`, `E0502.2` |
| Okuzawa | Okuzawa | Heimat von Guts' Grossvater | `E0551.4` |
| Yukino-gawa | der Yukino-Fluss | Behaelt `Yukino`, weil Shirabe *yuki* = Schnee erklaert | `E0002.1`, `E0442.2`–`.8` |
| Hotaru-zawa | der Gluehwuermchenbach | Nachts verboten | `E0303.0`, `E0502.5` |
| Kaze no Misaki | das Kap der Winde | Tag 14 | `E1304.9` |
| himawari-batake | das Sonnenblumenfeld | | `E1404.1` |
| o-kunugi (san) | die Grosse Eiche | Markanter Baum Richtung Strand; Baumart siehe § 7 | `E1404.16`, `E1205.0` |
| Teppen-yama | der Berg Teppen | Behaelt `Teppen`, weil der Erzaehler mit *teppen* = Gipfel spielt | `E1754.9`, `E2504.1`, `E2505.1` |
| Ryujin-ike | der Drachengott-Teich | Saoris Zeltplatz mit Luftschutzbunker | `E1701.3`, `E2630.0` |
| o-icho | der Grosse Ginkgo | Vorjaehriger Zeltplatz | `E1701.2` |
| himitsu kichi | das Geheimversteck | Unter der Autobahn | `E0254.0`, `E0551.16` |
| himitsu no nukemichi | der Geheimpfad | | `E1754.7` |
| noborigama | der Hangofen | Der Onkel erklaert die Form | `E0210.2`, `E2514.1` |
| kobo | die Werkstatt | | `E0210.1` |
| engawa | die Veranda | Der Onkel fragt Boku, ob er je in einem Haus mit Veranda gelebt hat | `E0112.0` |
| naya / katteguchi / uramon / ima / nikai | der Schuppen / die Kuechentuer / das Hintertor / das Wohnzimmer / oben | | `E0301.3`, `E0210.7` |
| furuido / bokugo | der alte Brunnen / der Luftschutzbunker | | `E0705.2`, `E2630.0` |
| uranai jizo / o-jizo-sama | der Orakel-Jizo / Jizo-sama | Man schlaegt ihm fuer ein Orakel auf den Kopf | `E0443.2`, `E0540.1` |
| umi no ie | die Strandhuette | | `E8059.0` |
| tokai | die Stadt | Boku nennt nie einen Stadtnamen | `E1861.27`, `E0445.2` |

---

## 3. Alltag, Hausregeln und wiederkehrende Wendungen

| Romaji | Deutsch | Hinweis | Fundstelle |
|---|---|---|---|
| itadakimasu / itadakimaasu | Itadakimasu! / Itadakimaasu! | Nicht *Guten Appetit!* (Stilbibel § 4) | `E0006.0`, `E0009.0` |
| gochisosama (deshita) | Gochisosama (deshita). | Nicht *Danke fuer das Essen.* | `E0007.0`, `E0010.0` |
| ...kimasu / ...deshita | ...kimasu / ...deshita | Nur Tag 1: Boku hinkt dem Chor hinterher | `E0103.2`, `E0104.2` |
| osomatsusama deshita | Es war nichts Besonderes. | | `E0406.8` |
| yoroshiku (ne / onegaishimasu) | Je nach Kontext eine von 3 Formen: **"Bitte kuemmern Sie sich gut um ihn."** (Vater uebergibt Kind); **"Freut mich, Sie kennenzulernen."** (Vorstellung bei Fremden); **"Wir verstehen uns schon gut, oder?"** (Bekannte) | Stilbibel § 4; Tag 1 nutzt alle drei | `E0171.1`, `E0177.0`, `E0182.0` |
| gokurosama (deshita) | Je nach Kontext: **"Das war eine lange Reise. Hast du gut gemacht."** (`nagatabi, gokurosama`, Punkt statt Gedankenstrich); sonst **"Gute Arbeit"** / **"Danke fuer deine Muehe"** | Wuerdigt Muehe, nicht Erfolg | `E0174.1` |
| nee (Boku-kun) | He(, Boku-kun) | Aufmerksamkeitsoeffner zu Zeilenbeginn | `E0202.2`, `E0302.2`, `E0541.1`, `E1904.2` |
| kore wa oji-san-chi / oba-chan-chi no kimari nan da kara | Das ist nun mal die Regel bei Onkel zu Hause. / ...bei Tante zu Hause. | **Fester Rahmen**, 4-mal (zuletzt am Schlusstag) | `E0002.1`, `E0185.0`, `E0303.3`, `E3180.0` |
| toban ni kettei! | Hiermit ernenne ich dich zum ...-Kapitaen! | Scherzhaft-behoerdlich: `Prunkwinden-Kapitaen`, `Feldhelfer` | `E0202.5`, `E0302.5` |
| asagao (toban) | Prunkwinde (Kapitaen) | | `E0202.5`, `exe@80046614.10`–`.18` |
| rajio taiso | Radio-Gymnastik | Jeden Morgen, FMV | `E0605.3`, `E2720.1` |
| rajio taiso kado / hanko | Gymnastikkarte / Stempel | Im Inventar `Gymnastikkarte`, im Dialog `Radio-Gymnastikkarte` | `exe@80046214.0`, `E3031.6` |
| enikki | Bildertagebuch | | `E0023.0`, `zukan@32E8` |
| jiyu kenkyu | Sommer-Forschungsprojekt | | `E0114.0` |
| konchu saishu setto | Insektenfang-Set | | `E0107.2` |
| natsuyasumi | Sommerferien | Nie *Sommerpause* | ueberall |
| bangohan atekko / bangohan kuizu | das Abendessen-Ratespiel / das Abendessen-Quiz | | `E0520.0`, `E1502.3` |
| seikai / daiseikai / hazure | Richtig! / Volltreffer! / Daneben | | `E4028.0`–`.6` |
| o-hakamairi / meinichi / butsudan | Grabbesuch / Todestag / Hausaltar | | `E1501.0`, `E1101.2`, `E8011.0` |
| shusen kinenbi | der Gedenktag zum Kriegsende | 15. August | `E1420.2` |
| hanabi taikai / senko hanabi | das Feuerwerksfest / Wunderkerzen (`Senko-hanabi`) | | `E0812.0`, `E1131.0` |
| yukata | Yukata | | `E1104.6` |
| ofuro | das Bad | | `E0020.0` |
| isoro | Kostgaenger (Moe neckend) / zu Gast sein (Boku im Tagebuch) | Nicht *Schnorrer* fuer einen Neunjaehrigen | `E0832.2`, `nikki@NIKKI_001` |
| naze desho? / nan desho? | Warum ist das wohl so? / Was koennte das wohl sein? | **Bokus Tic** (8-mal + Moe-Echo) | `E0832.8`, `E1506.0`, `E1632.13`, `E6000.4` |
| hikku! | Hicks! | Schluckauf bei Schreck | `E0405.1`, `E6004.18` |
| bayoyon! | Bye-yoyooon! | Shirabes Abgangsruf | `E0402.12`, `E1404.16` |
| buibui iwaseru no... Bentsu! | "Ich lass ihn brumm-brumm machen." "Was denn?" "Meinen Benz!" | Shirabes Traum (zweimal) | `E0640.6`–`.8`, `E2401.14`–`.16` |
| ana-ana-bobon | Ubli-bubli-bon | Fantasiewort fuer das Buch & Item 6 (`exe@80046214.6`) | `E1706.1`, `exe@80046214.6` |
| henteko obake | das seltsame Gespenst | | `E2161.0`, `E6005.2` |
| hibiware gata-pon no ki | der rissige Gata-pon-Baum | Bokus Beschreibung fuer eine Eiche | `E0608.0`, `E8063.0` |
| murasaki chu-chu | Lila Zutzler | Shirabes erfundenes Nektarbluemchen | `E0444.8`, `E2940.4` |
| patchin-waku | Patchin-Werk | Shirabes "Patchwork" | `E1705.2` |
| issho no takaramono | ein Schatz fuers Leben | Motiv der Tage 22–28 | `E2204.2`, `E2830.2` |
| ...o te ni ireta / ...o mitsuketa | ...erhalten / ...gefunden | Systemmeldungen | `E0307.0`, `E0670.0` |
| kagi ga kakatte iru | Abgeschlossen. | | `E8026.1` |
| randoseru | Schulranzen | Shirabes roter Ranzen | `E8014.0` |
| jaji | Trainingsanzug | | `E0504.1` |
| kachiku-goya | der Tierstall | Hinter dem Haus | `E0303.0` |
| teiogaku | Regentschaft; Bokus Echo: `...Re-gen-schaft?` | Stilbibel § 8 Typ 1 | `E0640.2`–`.3` |

---

## 4. Spielsysteme: Insekten, Sumo, Angeln, Drachen, Inventar

Klassenbegriffe werden deutsch uebersetzt: `Kaefer`, `Hirschkaefer`, `Nashornkaefer`, `Schmetterling`, `Schwalbenschwanz`, `Libelle`, `Zikade`, `Grille`, `Gluehwuermchen`, `Ameise` (*arinko* -> `Ameisen` / `kleine Ameisen`).

### 4a. Alle 57 Insekten (`exe@8003D2E0.*`, Buch `hhon@5328.*`)

Regel: **Schmetterlinge, Kaefer, Libellen -> deutsch; Zikaden und Singinsekten -> japanischer Name (weil sie nach ihrem Ruf heissen).** Eintraege mit `✎` erklaeren im Insektenbuch den japanischen Namen und nennen dort zusaetzlich den Romaji-Namen (z. B. `Chinesischer Pfauenfalter (Karasu-ageha, "Kraehen-Schwalbenschwanz")`).

**Pixel-Schranken und `@exchange`-Kurzformen:**
* Im Sumo-Tauschnotizbuch (`exe@8003D2E0.<n>@exchange`, `boku/exchange_notebook.py`) betraegt das harte Limit rechts neben dem "BIG!"-Abzeichen **`<= 98-px`** (nicht `102-px`!).
* Alle **9 Kaempferzeilen** (`23`–`30`, `56`) wurden geprueft: Alle 7 `Hirschkaefer` (`23`–`29`) ueberschreiten `98-px` (`101` bis `128-px`) und erhalten deshalb `@exchange`-Kurzformen (`65` bis `92-px`), waehrend `30 Nashornkaefer` (`87-px`) und `56 Gottesanbeterin` (`96-px`) direkt in die `98-px`-Box passen!
* Alle 57 Vollformen passen ins Kaefig-HUD (`<= 213-px`; laengstes `Langschwanz-Schwalbenschwanz` = `204-px`), und alle 9 Kaempfer bleiben `<= 135-px` (Hefterloch).
* In der Insekten-Enzyklopaedie (`mzkan@0..8.name`, `<= 111-px` in `GameFace` bzw. Fallback `Bean`): `#4 Moschusfalter` (`83-px` in `GameFace` / `60-px` in `Bean`) ersetzt *Moschus-Schwalbenschwanz* (`119-px` in `Bean`, waere gescheitert); `#6 Mikado-Schwalbenschwanz` hat `111-px` in `Bean` (passt exakt; Alternative `Mikadofalter` `76-px` `GameFace`).

| # | Romaji | Deutsch (`exe@8003D2E0`) | `@exchange` (`<= 98-px`) | Wissenschaftlich / Hinweis |
|---:|---|---|---|---|
| 0 | agehacho | Schwalbenschwanz | — | *Papilio xuthus* |
| 1 | ki-ageha | Gelber Schwalbenschwanz | — | *Papilio machaon* |
| 2 | onaga-ageha | Langschwanz-Schwalbenschwanz | — | *Papilio macilentus* (`204-px <= 213-px`) |
| 3 | karasu-ageha | Chinesischer Pfauenfalter ✎ | — | *Papilio dehaanii* (erwaehnt "Kraehe") |
| 4 | jako-ageha | Moschusfalter | — | *Byasa alcinous* (`83-px` GameFace, `mzkan@0`) |
| 5 | aosuji-ageha | Blaustreifen-Schwalbenschwanz | — | *Graphium sarpedon* |
| 6 | mikado-ageha | Mikado-Schwalbenschwanz | — | *Graphium doson* (`111-px` Bean, `mzkan@1`) |
| 7 | monshirocho | Kohlweissling | — | *Pieris rapae* |
| 8 | monkicho | Wandergelbling | — | *Colias erate* |
| 9 | aka-tateha | Indischer Admiral | — | *Vanessa indica* |
| 10 | shii-tateha | C-Falter ✎ | — | *Polygonia c-album* (*cho*-Wortspiel) |
| 11 | ruri-tateha | Blauer Admiral | — | *Kaniska canace* (Lapislazuli-Fluegel) |
| 12 | kujakucho | Tagpfauenauge | — | *Aglais io* |
| 13 | o-murasaki | Grosser Schillerfalter | — | *Sasakia charonda* (`92-px` Bean, `mzkan@3`) |
| 14 | o-ichimonji | Grosser Eisvogel | — | *Limenitis populi* |
| 15 | rumisu-shijimi | Loomis-Blaeuling | — | *Arhopala ganesa* (`98-px` GameFace, `mzkan@4`) |
| 16 | midori-shijimi | Gruener Zipfelfalter | — | *Neozephyrus japonicus* |
| 17 | yamato-shijimi | Blasser Grasblaeuling | — | *Zizeeria maha* |
| 18 | tsubame-shijimi | Kurzschwanz-Blaeuling ✎ | — | *Cupido argiades* (Schwalbenschwanz-Motiv) |
| 19 | asagi-madara | Kastanientiger | — | *Parantica sita* |
| 20 | hime-janome | Kleines Waldauge | — | *Mycalesis gotama* |
| 21 | tengucho | Tengu-Falter ✎ | — | *Libythea lepita* (`77-px` GameFace, `mzkan@5`) |
| 22 | aoba-seseri | Gruener Dickkopffalter | — | *Choaspes benjaminii* (`96-px` Bean, `mzkan@6`) |
| 23 / 56 | miyama-kuwagata | Miyama-Hirschkaefer | `Miyama-Kaefer` (`91-px`) | *Lucanus maculifemoratus* (`127-px` voll) |
| 24 / 57 | o-kuwagata | Riesen-Hirschkaefer | `Riesen-Kaefer` (`86-px`) | *Dorcus hopei* (`122-px` voll) |
| 25 | hirata-kuwagata | Flach-Hirschkaefer | `Flach-Kaefer` (`78-px`) | *Dorcus titanus* (`114-px` voll) |
| 26 | ko-kuwagata | Zwerg-Hirschkaefer | `Zwerg-Kaefer` (`85-px`) | *Dorcus rectus* (`121-px` voll) |
| 27 / 58 | nokogiri-kuwagata | Saege-Hirschkaefer | `Saege-Kaefer` (`84-px`) | *Prosopocoilus inclinatus* (`120-px` voll) |
| 28 | aka-ashi-kuwagata | Rotbein-Hirschkaefer | `Rotbein-Kaefer` (`92-px`) | *Dorcus rubrofemoratus* (`128-px` voll) |
| 29 | oni-kuwagata | Oni-Hirschkaefer ✎ | `Oni-Kaefer` (`65-px`) | *Prismognathus angularis* (`101-px` voll) |
| 30 / 59 | kabutomushi | Nashornkaefer | — (`87-px <= 98-px`) | *Trypoxylus dichotomus* |
| 31 | heike-botaru | Heike-Gluehwuermchen | — | *Aquatica lateralis* |
| 32 | kawa-tonbo | Fluss-Prachtlibelle | — | *Mnais* sp. |
| 33 | mukashi-tonbo | Urzeitlibelle ✎ | — | *Epiophlebia superstes* (`63-px` GameFace, `mzkan@7`) |
| 34 | miyama-sanae | Berg-Keiljungfer | — | *Anisogomphus maacki* (`95-px` GameFace, `mzkan@8`) |
| 35 | oniyanma | Oniyanma | — | *Anotogaster sieboldii* |
| 36 | ginyanma | Silber-Koenigslibelle | — | *Anax parthenope* |
| 37 | shiokara-tonbo | Salz-Blaupfeil ✎ | — | *Orthetrum albistylum* (wie mit Salz bestaeubt) |
| 38 | natsu-akane | Sommer-Heidelibelle | — | *Sympetrum darwinianum* |
| 39 | mayutate-akane | Brauen-Heidelibelle ✎ | — | *Sympetrum eroticum* |
| 40 | cho-tonbo | Falterlibelle ✎ | — | *Rhyothemis fuliginosa* (*cho*-Wortspiel) |
| 41 | tonosama-batta | Wanderheuschrecke | — | *Locusta migratoria* |
| 42 | kutsuwamushi | Kutsuwamushi | — | *Mecopoda nipponensis* (`gacha-gacha`) |
| 43 | kusakiri | Kusakiri | — | *Ruspolia lineosa* |
| 44 | hayashi-no-umaoi | Umaoi ✎ | — | *Hexacentrus* sp. ("Pferdetreiber") |
| 45 | kirigirisu | Kirigirisu | — | *Gampsocleis buergeri* (`gii-chon`) |
| 46 | enma-korogi | Enma-Grille ✎ | — | *Teleogryllus emma* (Enma, Hoellenkoenig) |
| 47 | kusahibari | Kusahibari | — | *Svistella bifasciata* ("Graslerche") |
| 48 | suzumushi | Suzumushi ✎ | — | *Meloimorpha japonica* (Namenswechsel 48/49) |
| 49 | matsumushi | Matsumushi ✎ | — | *Xenogryllus marmoratus* |
| 50 | nii-nii-zemi | Nii-nii-zemi | — | *Platypleura kaempferi* |
| 51 | abura-zemi | Abura-zemi ✎ | — | *Graptopsaltria nigrofuscata* (*abura* = Oel) |
| 52 | ezo-zemi | Ezo-zemi | — | *Auritibicen japonicus* |
| 53 | higurashi | Higurashi | — | *Tanna japonensis* (`kana-kana-kana`) |
| 54 | min-min-zemi | Min-min-zemi | — | *Hyalessa maculaticollis* |
| 55 | tsukutsuku-boshi | Tsukutsuku-boshi | — | *Meimuna opalifera* |
| 56 (ID 60) | kamakiri | Gottesanbeterin | — (`96-px <= 98-px`) | *Tenodera* sp. |
| — | aite imasu | Frei | — | `hhon@5328.60` (leeres Kaestchen) |

**11 weitere Kreaturen im Dialog:** `Gluehwuermchen` (*hotaru*) · `Ameisen / Arbeiterameisen / Ameisenkoenigin` (*arinko / hataraki-ari / joo-ari*) · `Bockkaefer` (*kamikiri-mushi*) · `Erdwespe` (*jibachi*) · `Wespennest` (*hachi no su*) · `Kragenbaer` (*tsukinowa-guma*) · `Wildhund` (*yamainu*) · `Japanischer Wolf` (*Nihon-okami*) · `Nipponibis` (*toki*, `E6000.7`) · `Berggorillas / Bergaffen / Wildschwein` (`Bergaffen / Wildschwein` fuer *yamazaru / inoshishi*) · `Nachtigallen-Kot` (*uguisu*, `E0720.1`).

### 4b. Kaefer-Sumo (`musi@*` & `textures/sumo.txt`)

* **Allgemeine Begriffe:** `Kaefer-Sumo` · `Ring` (*dohyo*) · `Energie` (`sumo@plate.stamina`, `44-px <= 48-px` GameFace; *Ausdauer* ist mit `56-px` zu breit!) · `Kaefer-Tausch` (*mushi kokan*) · `King / King-Match` · `Leicht / Stark / King` (`musi@358.0`–`.2` & `sumo@rank.*`, `37/33/27-px <= 50-px` VWF und geprueft innerhalb der Kreide-Ellipsen) · `{G:47}: Kaefer anfeuern` (`musi@348.0`, `116-px <= 212-px`) · `SN` (`exe@code:800377F8`, 2 ASCII-Zeichen fuer `S`/`N`, passend zu `rec@M_S01100.won/lost`) · `Siegeszug` (`sumo@move.heading`, `67-px <= 88-px` fett).
* **Debug-Zustandsnamen (`musi@2C.0`–`.12`, unerreichbar):** `Warten / Ausruhen / Vor / Zurueck / Griff / Beide druecken / 1P drueckt / 2P drueckt / MAX-Schub / Seitwaerts / Technik / Treffer / MAX gedrueckt`.
* **19+3 Siegeszuege & 15 Glossen:** `musi@2C.13`–`.31` muessen **buchstabengenau** mit `sumo@move.1`–`.19` uebereinstimmen; die 15 `GLOSSED`-Zuege erfuellen `r"[A-Z][a-z]+"`; alle Streifen liegen fett in `GameFace` `<= 122-px` ohne vertikale Beruehrung (`LINE = 11`):

| `sumo@move` | Zugname (`arrays` + `sumo`) | Deutsche Glosse (`<= 122-px` fett) | Streifen-Breite |
|---|---|---|---|
| `move.0` | `Oshidashi` | `Hinausstoss vorn` | `115-px` |
| `move.1` | `Buchikamashi` | `Kopf-voran-Sturm` | `118-px` |
| `move.2` | `Tsuppari` | `Offene Stoesse` | `102-px` |
| `move.3` | `Utchari` | `Kippwurf am Rand` | `117-px` |
| `move.4` | `Gaburiyori` | `Federnder Schub` | `112-px` |
| `move.5` | `Kampfgeist` | — | `72-px` |
| `move.6` | `Uwatenage` | `Ueberarmwurf` | `94-px` |
| `move.7` | `Brainbuster` | — | `75-px` |
| `move.8` | `Hikiotoshi` | `Hand-Niederzug` | `106-px` |
| `move.9` | `Susoharai` | `Fussfeger hinten` | `106-px` |
| `move.10` | `Sukuinage` | `Guertelloser Wurf` | `114-px` |
| `move.11` | `Tsuridashi` | `Herausheben vorn` | `120-px` |
| `move.12` | `Ashihiki` | `Beinzug` | `53-px` |
| `move.13` | `Umdreher` | — | `63-px` |
| `move.14` | `Abisetaoshi` | `Rueckwaerts-Fall` | `112-px` |
| `move.15` | `Tsukidashi` | `Frontal-Abstoss` | `105-px` |
| `move.16` | `Sabaori` | `Vorwaerts-Fall` | `97-px` |
| `move.17` | `Harite` | `Offene Ohrfeige` | `103-px` |
| `move.18` | `Mantis-Schere` | — | `93-px` |
| `move.19` | `Mantis-Buster` | — | `91-px` |
| `move.20` | `Unentschieden` | — | `96-px` |
| `move.21` | `Ausdauer-Sieg` | — | `97-px` |

### 4c. Angeln (`exe@8003DA4C.*`, `exe@800462C8`–`6390`)

* **3 Fische:**
  - `Iwana` (`34-px <= 91-px`)
  - `Forelle` (`41-px <= 91-px`) im engen Fangtitel (`exe@8003DA4C.1`), **`Regenbogenforelle`** (`113-px <= 123-px`) im Angelmenue (`exe@80046384.0`), in Rekorden und im Dialog (sofern Stufe 3/4 die `91-px`-Fangtafel nicht verbreitert)
  - `Yamame` (`51-px <= 91-px`)
* **10 Angelbegriffe:** `Tenkara-Fliege` (*tenkara kebari*) · `Fliege` (*kebari*) · `Koeder` (*esa*) · `Pose` (*uki*) · `Biss` (*atari*) · `Anhieb` (*awase*) · `Angelzeug` (*shikake*) · `Sommerfang` (*natsuyasumi no choka*) · `Angelrute / Rute` (*tsurizao / sao*, `E0205.1`) · `Herr des Teichs` (*ike no nushi*).

### 4d. Drachen (`exe@800461CC.0`–`.7`, `tako@440.0`, `textures/kite.txt`)

Alle 8 Drachen passen sowohl ins VWF-Menue (`<= 115-px`) als auch ins Drachenbuch (`GameFace <= 110-px`):

| Romaji | Deutsch | VWF / GameFace | Hinweis |
|---|---|---|---|
| kaku-dako / nakabari kaku-dako | `Rechteckdrachen` | `103 / 102-px` | Im Buchtext `Mittelspann-Rechteckdrachen` moeglich |
| nina-dako | `Nina-Drachen` | `80 / 77-px` | Kinderdrachen von Iki |
| semi-dako | `Zikadendrachen` | `94 / 92-px` | |
| tori-dako | `Vogeldrachen` | `83 / 81-px` | |
| koinobori-dako | `Karpfendrachen` | `94 / 93-px` | |
| hikoki-dako | `Flugzeugdrachen` | `102 / 100-px` | |
| ren-dako | `Drachenkette` | `80 / 79-px` | |
| nigaoe-dako | `Boku-Drachen` | `86 / 84-px` | Traegt Bokus Gesicht |

* Weitere Begriffe: `Drachensteigen` (*takoage*) · `Das froehliche Drachen-Lexikon` (*tanoshii tako hyakka*) · `Abgestuerzt!` (`tako@440.0`, `78-px <= 104-px`) · `Seltsame Insekten-Enzyklopaedie` (`E0022.0`).
* **Drachen-HUD (`kite@hud.*`, `GameFace`):** `Wind` (`25-px <= 30-px`), `Fahrt` (`31-px <= 38-px`; *Tempo* waere `41-px` und zu breit!), `Hoehe` (`37-px <= 46-px`).

### 4e. Inventar (`exe@80046214.*`), Menues, Orakel und Rekorde

* **15 Inventar-Items (`<= 115-px` im Beutel):**
  `0` `Gymnastikkarte` (`94-px`; Vollform im Dialog: `Radio-Gymnastikkarte`) · `1` `Reiscracker-Gruss` (`112-px`; alt. `Souvenir-Cracker` `107-px`; Vollform im Dialog: `Mitbringsel-Reiscracker`) · `2` `Axt` (`22-px`) · `3` `Boellerbuendel` (`87-px`) · `4` `Zuckerwasser` (`85-px`) · `5` `Seltsames Ding` (`93-px`; spaeter `Wal-Ohrknochen`) · `6` `Ubli-bubli-bon` (`83-px`) · `7` `Shirabes Schleife` (`104-px`) · `8` `Sonnenblumen` (`86-px`; Vollform im Dialog: `Sonnenblumenstrauss`, `131-px` fuer die Liste zu lang) · `9` `Ken-bos Fell` (`76-px`) · `10` `Schlangenhaut` (`88-px`) · `11` `Gelbe Blume` (`73-px`, im Beschreibungstext `Trollblume`) · `12` `Maiskolben` (`66-px`) · `13` `Foto` (`29-px`) · `14` `Wal-Ohrknochen` (`97-px`).
* **Status & Auswahlmenues:** `Kescher` (*hochumo*) · `Kaeferkaefig` (*mushikago*) · `Sachen` (*mochimono*) · `Angelzeug` (*tsuri dogu*) · `Insektensammlung` (*konchu hyohon*) · `Freilassen?` · `Behalten / Lieber nicht` · `Diesen aufgeben / Erst mal einstecken` · `Eintragen?` · `Bildertagebuch schreiben und schlafen?`
* **Extras-Menue (`exe@8003DA00.*`, `.0`–`.4 <= 109-px`, `.5 <= 134-px`):** `Bildertagebuch` (`89-px`) · `Sammlung+Kaefig` (`108-px`) · `Drachen` (`49-px`) · `Sachen` (`44-px`) · `Ende` (`30-px`) · `Essens-Quizquote` (`110-px`).
* **Optionen & Erinnerungen (`ui.txt`):** `tex@T_CONFIG.heading` haelt maximal `50-px` in `GameFace` (`Menue` `37-px` oder `Setup` `34-px`; *Optionen* ist `51-px` und wird abgewiesen!). `tex@T_MEMORY.heading`: `Sommer- // Erinnerungen` (`53 / 77-px <= 99-px`).
* **Orakel (`exe@80036750.* <= 104-px`):** `Grosses Pech!` (`87-px`), `Kleines Glueck!` (`90-px`), `Gutes Glueck!` (`82-px`), `Grosses Glueck!` (`97-px`).
* **Rekorde (`records.txt`):** `rec@FS_WAL`: `fish` -> `St.` (`9 <= 14-px`), `size` -> `Groesse` (`33 <= 37-px`), `average` -> `Schnitt` (`29 <= 36-px`), `largest` -> `Rekord` (`28 <= 36-px`). `rec@M_S01100`: `caught` -> `Fang 8/` (`32 <= 56-px`), `won/lost` -> `S` / `N` (`4 <= 12-px`), `value` -> `So viel wert wie` (`66 <= 115-px`), `value_unit` -> `Saege-Kaefer` (`56 <= 69-px`).
* **Memory Card (`exe@8003D5F0.*`):** Offizieller Sony-Begriff **`MEMORY CARD`** in Grossbuchstaben beibehalten (`"MEMORY CARD wird geprueft..."`, `"MEMORY CARD nicht entfernen"`). Speicher-Titel (`title@sjis:188`): `Bokus Ferien {slot} {day}. Aug.` (`49 <= 64` Bytes Shift-JIS).

---

## 5. Essen (`E0221.2`–`.31`, `SELECT_ROW <= 248-px`)

Bekannte japanische Gerichte behalten ihren Namen (Stilbibel § 15); Hausmannskost nach westlicher Art (*yoshoku*) behaelt ihre japanische Bedeutung (`Hamburger Steak` ist eine Frikadelle/Bulette, niemals ein Hamburger im Broetchen!). Alle 47 Abendessen-Quiz-Gerichte bleiben `<= 248-px` (laengstes `Oyakodon mit Lachs und Lachsrogen` = `223-px`):

| Quiz-Tag `d` (`E0221.<d+1>`) | Verbindliches Deutsch |
|---|---|
| d 1, 8, 15, 17, 25, 26, 29 | `Curry-Reis` / `Katsu-Curry` / `Trockencurry` |
| d 2, 28 | `Hayashi-Reis` |
| d 2, 9, 14, 21, 22 | `Hamburger Steak` / `Wuerfelsteak` / `Menchi-Katsu` |
| d 1, 3, 8, 12, 20, 24 | `Haehnchen-Katsu` / `Tonkatsu` / `Katsudon` |
| d 3, 5, 11, 20, 30 | `Karaage` / `Frittierte Sardinen` |
| d 1, 6, 7, 11, 19, 21, 30 | `Lachs Muellerin Art` / `Seebarsch Muellerin Art` / `Frittierter Lachs` / `Frittierte Garnelen` |
| d 5, 11, 23 | `Salzgegrillter Sanma` / `Sanma Kabayaki` / `Gegrillter Hokke` |
| d 8, 21, 27 | `Bastardmakrele nach Nanban-Art` / `Bastardmakrelen-Tataki` |
| d 5, 13, 17, 22, 23 | `Sashimi und Tempura` / `Sushi` / `Inari-zushi` |
| d 3, 4, 10, 19, 29 | `Gebratenes Fleisch mit Gemuese` / `Schwein und Kohl in Austernsosse` (`208-px`) / `Ingwer-Schwein` / `Miso-mariniertes Grill-Schwein` |
| d 4, 10, 16, 26 | `Hiyashi Chuka` / `Hiyamugi` / `Spaghetti` |
| d 4, 9, 13, 14, 15, 19, 20, 24, 27 | `Fruehlingsrollen und Happosai` / `Bratreis und Schwein suess-sauer` (`205-px`) / `Gebratener Reis und Happosai` / `Gyoza` |
| d 6, 7, 10, 12, 15, 17, 18, 25–29 | `Nikujaga` / `Kohlrouladen` / `Korokke` / `Omurice` / `Gratin` |
| d 7, 13, 18, 23–25, 28 | `Haehnchen-Saute` / `Huehnchen in Tomatensosse` / `Gefuellte gruene Paprika` / `Gefuellte frittierte Lotuswurzel` |
| d 14, 16 | `Oyakodon` / `Oyakodon mit Lachs und Lachsrogen` (`223-px`) |
| d 22, 30 | `Jingisukan` (auf der Speisekarte nur dieses Wort; bedeutet gegrilltes Hammelfleisch nach Hokkaido-Art) |

* **Schabeeis (`E0404.3`–`.7`):** `Schabeeis`; `Melone` / `Erdbeere` / `Zitrone` / `Mizore` / `Regenbogen-Spezial`.
* **Sommersnacks (`E0122.0`, `E0213.3`):** `Gerstentee` / `hausgemacht` / `Ajiuri` (kleine suesse Melone, in der Zeile erklaert) / `Mais` / `Wassermelone`.
* **Sushi & Senbei (`E1503.1`, `E2203.4`–`.13`):** `Reiscracker` / `ohne Wasabi` / `Kappa-Maki` / `Hamachi` / `Thunfisch`.
* **Schulspeisung (`E0341`, `E0940`–`E1341`):** `Harusame-Salat` / `Weichnudeln` / `Frittiertes Brot` / `Koppe-Broetchen` / `Frittiertes Walfleisch` / `Gabel-Loeffel` / `Pyramidenpackung` (nicht *Tetra Pak*) / `"Diaetbrot"`.
* **Tante-Emma-Laden (`E1740.0`, `E1940.1`, `E2452.0`, `E1907.0`):** `Tante-Emma-Laden` (*dagashiya*) / `Menko-Karten ("wir nennen sie hier Patchi")` / `Knallerbsen` / `Boeller`.

---

## 6. Zeitgeist 1975: Fernsehen, Buecher, Spielzeug, Zeitgeschichte

* *Tom und Jerry* · Kin-chan · Ultraman · `"die, die sich verwandeln, aber nicht groesser werden"` (Kamen Rider) · Rider-Karten / Rider-Snack / Spinnenmann · Kappa Ebisen · *Heidi* · *Die Abenteuer von Gamba* / Noroi · *Romper Room* · Uri Geller · Freitag der 13. · *Miffy* (*Chiisana Usako-chan* — es geht um den X-Mund) · Doktor Dolittle · *Die Chroniken von Narnia* · *Guri und Gura* · *Satomi Hakkenden* · Tom Sawyer / Huckleberry Finn / Mark Twain · Apollo / Kommandant Armstrong · Beilage der *Kagaku* / Mondauto · Coca-Cola-Jojos / Flummis / Modellflugzeuge (Bambusstreifen, Alurohr) · Silvester-Gesangswettbewerb (*Kohaku*) · Mandarinen am Kotatsu · Benz · Jumbojet · Stewardess · Schwimmkurs · Pruefungsschueler / Oberschule / Schulfest / Konrektor / Schulspeisung (-Kantine) · Otaru / Bezirksamt Suginami / Kanazawa / Sendai-Tanabata / Shikoku · Meiji-Zeit · `Showa 17` (ohne Jahreszahl-Glosse) · Pazifikkrieg · Dorfjugendverein · Neubausiedlung · `"Moratorium"` (`E2532.4`).

---

## 7. Natur und Landschaft

`satoyama` -> *"so weit draussen auf dem Land"* (`E0171.1`), danach *"die Huegel"* · Bach · Tal · Fuss des Berges · Gewitterwolken · Sardinenwolken (*Iwashigumo*, Tag 13 haengt am woertlichen Bild) · einsame Wolke · Sternenstaub (*Nukaboshi*) · Sawtooth-Eiche (*Kunugi*) / Lederhuelsenbaum (*Saikachi*) -> nach Erstnennung *"Eiche"* · Trollblume (*Kinbaiso*) · Kosmee · Sonnenblume · Prunkwinde · Abendrot · Herbstwind · Autobahn.

---

## 8. Interjektionen, Geraeusche und Foto-Stichwort

* `un` -> `Ja` / `Mhm` · `uun / n-n` -> `Noe` / `Nee` · `e? / he?` -> `Hae?` / `Wie?` · `hee` -> `Ohh` / `Aha` · `fu-n` -> `Hmm` · `waai` -> `Juhu!` · `yattaa!` -> `Geschafft!` / `Super!` · `are?` -> `Huch?` / `Moment...` · `aa-a` -> `Ach...` / `(seufz)` · `gee` -> `Igitt` / `Baeh` · `hiee` -> `Iiek!` · `gakkushi` -> `(stoehn)` · `che` -> `Tzz` · `kora / kora-kora` -> `He!` / `Na, na` · `yossha` -> `Alles klar!` · `yoisho` -> `Hauruck!` · `ei` -> `Hopp!` · `fuwaa` -> `(gaehn)` / `*gaeeehn*` · `ii-da / ii-tsu` -> `Baeaeah!` · `wa!` -> `Buh!` · `chu!` -> `*schmatz*`.
* **Foto-Stichwort (`E0445.5`–`.6`, `E0923.6`, `E1606.1`):** Die Tante sagt statt "Bitte laecheln!" immer `"Was mag Papa am liebsten?"` und die Kinder rufen `"Kaese!"`.
* Lachen und Dehnungen: siehe Stilbibel § 7.

---

## 9. Alle 23+1 Wortspiele und sprachabhaengigen Stellen (`bible.md` § 6)

Verbindliche deutsche Loesungen fuer saemtliche Wortspiele nach Stilbibel § 8 (Typ 1: Kind verhaspelt schweres Wort; Typ 2: Lehnwoerter; Typ 3: japanisches Homophon sichtbar halten):

| # | IDs | Typ | Verbindliche deutsche Lösung (v1.1.0 mit echten Umlauten/`ß`) |
|---|---|---|---|
| 1 | `E0177.2` | Typ 1 | `Unser Papa ist cool, oder? // Er ist Ke-ra-mi-ker. Er macht Teller und Reisschalen.` |
| 2 | `E0340.1`–`.2` | Typ 1 | `.1`: `...Was heisst "ungehobelt"?` / `.2`: `Genau das nicht zu wissen, nennt man ungehobelt.` |
| 3 | `E0640.2`–`.3` | Typ 1 | `.2`: `Ich will aus der Welt der Ameisen die Regentschaft erlernen.` / `.3`: `...Re-gen-schaft?` |
| 4 | `E0712.3` | Typ 1 | `.2`: `...gekauft und hierher umgesiedelt.` / `.3`: `Was ist "um-ge-sie-delt"?` |
| 5 | `E0720`, `E0740.1`–`.2` | Typ 3 | `E0720.1`: `Nachtigallen-Kot`; `.2`: `Kacka?`; `E0740.1`: `Kennst du Nachtigallen-Kot?` / `.2`: `Natuerlich weiss ich das. // Das ist doch jemand, der immer an einem dran klebt, nicht wahr? // Shirabe weiss schliesslich alles.` |
| 6 | `E1220.3`–`.6` | Typ 3 | `.3`: `...hattest damals die Mashin...` / `.4`: `Eine Maschine?` / `.5`: `...Nicht ganz.` / `.6`: `Mashin bedeutet Masern.` |
| 7 | `E1820.8`–`.10`, `E2203.0`–`.2` | Typ 2 | `E1820.8`: `Frauen sind ganz schoen deluxe, oder?` / `.9`: `...Meinst du nicht delikat?` (Tag 22 tauscht: `delikat` / `Deluxe!`) |
| 8 | `E1840.0`–`.1` | Typ 3 | `.0`: `...es wird Blut regnen. Ein Blut-Ame.` / `.1`: `Ein Blut-Ame? Blut-Bonbon?` |
| 9 | `E1912.3`–`.4` | Typ 1 | `.2`: `...in der Pubertaet...` / `.3`: `Bupertaet?` / `.4`: `Pubertaet.` |
| 10 | `E1920.2`–`.4` | Typ 3 | `.2`: `Das ist ein Hana-uta...` / `.3`: `Ein Hana-uta? Ein Nasenlied?` / `.4`: `Ein Blumenlied!` |
| 11 | `E2205.3`–`.5` | Typ 3 | `.3`: `...und fuer Papa eine Cho-Krawatte!` / `.4`: `Eine Cho-Krawatte? Eine Billion Krawatten?` / `.5`: `Cho wie Schmetterling. Eine Fliege!` |
| 12 | `E2210.6` | Typ 3 | `Sie hatte wohl eine Katze aufgesetzt, wie man so sagt, und einen Hund, und einen Tanuki, alle moeglichen Tiere...` |
| 13 | `E2430.1` | Typ 1 | `.0`: `...nachtaktiv geworden.` / `.1`: `Nacht-takt-iv?` |
| 14 | `E2532.4`–`.8` | Typ 2, 3 | `.4`: `"Moratorium"` / `.5`: `Fuer mich ist das alles Chinpun-Kanpun...` / `.6`: `...klingt wie ein Pandaname.` / `.7`: `...Moratorium...` / `.8`: `Klingt wie ein Planetarium.` |
| 15 | `E2641.2` | Kultur | `Vielleicht hat es nicht gestimmt, weil es eine Sandale war und kein Geta?` |
| 16 | `E2712.0` | Motiv | `Verstehe... wenn ich so bin, dann bin ich wohl auch noch ein kleines Gefaess...` |
| 17 | `E1503.5` | Typ 3 | `Alles lief wie am Schnuerchen \| Ein See aus Wein, ein Wald aus Fleisch \| Wie ein Albtraum` (`229-px <= 248-px`) |
| 18 | `E4028.17` | Typ 3 | `...das Turm-Set von Osho Sushi in Sagi-no-sato...` |
| 19 | `E1861.3`–`.5`, `.27` | § 1 | `.3`: `Ich bin Boku.` / `.4`: `Wie bitte? Du bist du? Dann bist du ab heute eben Boku-kun.` / `.5`: `Sag ich doch, das stimmt ja auch.` / `.27`: `...in der Klasse von Nakajima-sensei!` |
| 20 | `E1420.0`, `E2320.0` | § 1 | `Bokus Sommerferien` (Spieletitel bleibt *Boku no Natsuyasumi*) |
| 21 | `E1701.7`, `E3042.3` | § 7 | `E1701.7`: `Wolfs... maedchen.` / `E3042.3`: `Du. Drei. Kaese. Hoch.` |
| 22 | `E8060.0` | § 14 | `Da steht: "Taka... ...der... ...von... ...wird... ...en."` |
| 23 | `hhon@5328.10`, `.40`, `.48/.49`, `.3/.18/.21/...` | § 4a | `.10`: `...kein cho-tto bisschen!`; `.40`: `...warum "Cho", Falter? ...und noch dazu cho-mini, super-mini!`; `.48/.49`: `Matsumushi`/`Suzumushi` Namenswechsel; `.3/.18/.21/.29/.33/.37/.39/.44/.46/.51` fuehren den japanischen Namen in `(...)` mit, wo die Zeile ihn erklaert. |
| +1 | `E3042.8` (Bonus) | Typ 3 | `...du bist doch mein Diener, mein Ge-Boku, oder?` |

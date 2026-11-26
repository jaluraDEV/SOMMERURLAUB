<p align="center">
  <img src="docs/logo.png" width="320" alt="Projekt SOMMERURLAUB Logo">
</p>

<h1 align="center">Projekt SOMMERURLAUB</h1>

<p align="center">
  <strong>Vollstaendige deutsche Fan-Uebersetzung von <em>Boku no Natsuyasumi</em> (PS1, SCPS-10088)</strong><br>
  <em>31 Sommertage auf dem Land -- komplett auf Deutsch spielbar (Dialoge, Menues, Texturen, Tagebuch, Lexika & Untertitel).</em>
</p>

<p align="center">
  <a href="../../releases"><strong>Patch herunterladen (Releases)</strong></a> ·
  <a href="#installation--anleitung">Anleitung</a> ·
  <a href="#pruefsummen-sha-1">Pruefsummen</a> ·
  <a href="#lizenzen--credits">Lizenzen &amp; Credits</a>
</p>

---

## Was ist Projekt SOMMERURLAUB?

**Projekt SOMMERURLAUB** ist ein deutscher Fan-Uebersetzungspatch fuer das PlayStation-1-Original von *Boku no Natsuyasumi* (ぼくのなつやすみ, SCEI / Millennium Kitchen, 2000, **SCPS-10088**): Ein neunjaehriger Junge verbringt den August 1975 bei seinem Onkel auf dem Land -- 31 Tage voller Kaeferfang, Kaefer-Sumo, Drachensteigen, Angeln und Bildertagebuch.

- **Alle 2.801 Dialog- & Ereigniszeilen** (`shared.txt` + `day01.txt`–`day31.txt`) im Dual-Source-Verfahren direkt gegen das japanische Originalskript uebersetzt.
- **Alle 314 UI-, Menue-, Item- & Enzyklopaedie-Eintraege** (`arrays.txt`), inkl. aller 57 Insektennamen, Fische, Drachen und Memory-Card-Texte.
- **Alle 300 Textur-Texte** (`textures/`): Titelmenue, Stein-Buttons, Schilder, Rekorde, Kaefer-Sumo-HUD, Drachen-HUD, Insekten- & Drachen-Lexikon sowie alle **93 Seiten von Bokus Bildertagebuch**.
- **Alle 89 Film- & Sprachclip-Untertitel** (`movies.txt` & `clips.txt`): Intro (`M27`), Abspann (`M28`), Titelsong, Zwischensequenzen, Kaefer-Sumo-Rufe und alle **5 End-Epiloge** (`XCH.41`–`XCH.45`). Die japanische Sprachausgabe bleibt bewusst erhalten.
- **Nichts gekuerzt ("Nothing is cut to fit"):** Ueberlange Text-Container werden automatisch reloziert; alle drei Spielfonts (`VWF`, `GameFace`, `Bean`/`Sprout`) nutzen die saubere ASCII-Umlaut-Konvention (`ae`, `oe`, `ue`, `ss`).

---

## Rechtlicher Hinweis

> **Rechtlicher Hinweis:**  
> *Boku no Natsuyasumi* (ぼくのなつやすみ, PS1, `SCPS-10088`, 2000) ist © **Sony Interactive Entertainment** (ursprünglich Sony Computer Entertainment Inc.) und entwickelt von **Millennium Kitchen**.  
> **Projekt SOMMERURLAUB** ist ein unkommerzielles Fan-Übersetzungsprojekt und steht in keiner Verbindung zu Sony Interactive Entertainment oder Millennium Kitchen.  
> Dieses Repository und die Releases enthalten **keinerlei Original-Spieldateien**. Zur Nutzung wird eine eigene Kopie (Dump) der japanischen Original-CD benötigt.

---

## Installation & Anleitung

1. **Eigenen Dump der japanischen Original-CD (`SCPS-10088`) bereitstellen** (`.bin` / `.img` + `.cue`). Falls ein `.chd` vorliegt, vorher mit `chdman` entpacken.
2. **SHA-1-Pruefsumme pruefen:** Der unmodifizierte Original-Dump muss exakt den Redump-SHA-1 `5959bf7d9835d0a60aeb0143e2d0fc564bfea9fa` haben.
3. **Patch anwenden:**
   - **Mit `xdelta3` / MultiPatch (empfohlen):** Die `.xdelta`-Datei aus den [Releases](../../releases) auf dein Original-Image anwenden:
     ```bash
     xdelta3 -d -s "Boku no Natsuyasumi (Japan).bin" "Boku no Natsuyasumi (Japan) [T-De SOMMERURLAUB v1.0.0].xdelta" image.img
     ```
   - **Mit DuckStation (PPF-On-the-Fly):** Alternativ die `.ppf`-Datei aus den Releases in DuckStation als Patch hinterlegen oder fest patchen.
4. **Spielen:** Die beiliegende `image.cue` (zusammen mit der gepatchten `image.img`) in **DuckStation** oder **RetroArch (Beetle PSX)** laden.

---

## Pruefsummen (SHA-1)

| Version | Original-Dump (vorher) | Gepatchtes Image (nachher) |
|---|---|---|
| Original (`SCPS-10088`) | `5959bf7d9835d0a60aeb0143e2d0fc564bfea9fa` | `5959bf7d9835d0a60aeb0143e2d0fc564bfea9fa` |
| **SOMMERURLAUB v1.0.0** | `5959bf7d9835d0a60aeb0143e2d0fc564bfea9fa` | `eaddd03ef086c2af85c627c8af81b3edbe5a65f3` |

---

## Lizenzen & Credits

Dieses Projekt basiert auf dem englischen Uebersetzungsprojekt **[jeapostrophe/boku-ps1](https://github.com/jeapostrophe/boku-ps1)** von **Jay McCarthy** (inkl. der dort dokumentierten Vorarbeiten und Credits an `pleonex`, `HilltopWorks`, `GriffithVIII`, `psyouloveme`, `KendritPy` und `snake7594`, siehe [research/related-projects.md](research/related-projects.md)). Fuer **Projekt SOMMERURLAUB** wurden die gesamte Uebersetzung, das Glossar, die Stilbibel, Teile der Linter-/Pipeline-Regeln sowie die Texturen komplett ins Deutsche uebertragen und angepasst.

Es gilt die **Dual-Lizenz** des Basis-Projekts:
- **Code, Build-Tools, Skripte & Assembly-Patches:** [MIT-Lizenz](LICENSE) ([opensource.org/licenses/MIT](https://opensource.org/licenses/MIT))
- **Uebersetzungsskript & Kontext-Notizen (`translation/`):** [CC BY-SA 4.0](LICENSE-translation) ([creativecommons.org/licenses/by-sa/4.0/](https://creativecommons.org/licenses/by-sa/4.0/))

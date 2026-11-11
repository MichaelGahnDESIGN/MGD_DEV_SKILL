---
name: mgd-design-check
description: >-
  Prüft das Design einer Webseite oder Oberfläche mit Hallmark (Anti-KI-Look) und dessen
  Linter im echten Browser, und baut auf Wunsch neue Seiten mit Hallmark. Für /mgd-design-check.
  Installiert fehlende Voraussetzungen (puppeteer-core global, Hallmark nach Rückfrage) selbst.
  Ändert bestehende Dateien nur auf ausdrücklichen Wunsch (polish).
---

# /mgd-design-check

Kurzbefehl für [Hallmark](https://github.com/Nutlope/hallmark) (Nutlope, MIT).
Aufruf-Formen:

| Aufruf | Was passiert | Ändert Dateien? |
|---|---|---|
| `/mgd-design-check <Pfad oder URL>` | **Prüfbericht** (Hallmark `audit` + Linter im Browser) | nein |
| `/mgd-design-check neu <Beschreibung>` | **Neue Seite** bauen mit `/hallmark` | ja, nur neue Dateien |
| `/mgd-design-check polish <Pfad>` | Nur die gefundenen KI-Merkmale beheben (`redesign`, Inhalt und Layout bleiben) | ja, nur auf diesen Befehl |

Ohne Angabe: den vom Projekt gebauten Frontend-Ordner bzw. die lokale Dev-URL
nehmen, die im Projekt dokumentiert ist. Nichts erfinden; unklar → einmal kurz nachfragen.

## Schritt 0: Voraussetzungen prüfen und selbst herstellen

1. **Node 18+:** `node -v`. Fehlt Node: melden und stoppen (Nutzer installiert Node).
2. **puppeteer-core (global):** `npm ls -g puppeteer-core --depth=0`.
   Fehlt es: **direkt** `npm i -g puppeteer-core` ausführen, ohne extra Rückfrage
   (vom Nutzer dauerhaft erlaubt, harmlos, nur Browser-Steuerung). Danach erneut prüfen.
3. **Chrome/Chromium:** Hallmark findet `/Applications/Google Chrome.app` o. Ä. selbst
   oder über `CHROME_PATH`. Ist keins da: den Nutzer bitten, Chrome zu installieren;
   bis dahin nur statische Prüfungen (ohne `--render`) und das im Bericht sagen.
4. **Hallmark:** Ordner `~/.claude/skills/hallmark` oder `~/.agents/skills/hallmark`
   suchen. Fehlt er: **erst fragen** (Code von Dritten), bei „ja“
   `npx skills add nutlope/hallmark -g --agent claude-code`. Danach Hinweis, dass
   ein Neustart der Sitzung nötig sein kann; die Skripte unter `<skill-dir>/scripts/`
   lassen sich trotzdem sofort mit `node` starten.

## Schritt 1: Prüfen (Standard und `polish`)

1. Projektregeln lesen. Gibt es `design.md` / `DESIGN.md` (gesperrtes Designsystem):
   hat Vorrang, im Bericht nennen.
2. Linter: `node <hallmark-dir>/scripts/sloplint.mjs <Ziel> --render`
   (bei laufender Seite zusätzlich `--url <lokale-URL>`). Nur lokale Adressen
   (`localhost`, `127.0.0.1`) oder die vom Nutzer genannte URL öffnen.
3. Hallmark `audit <Ziel>` ausführen (laut `references/redesign.md` von Hallmark).
   Das ist ein reiner Bericht.
4. Schweregrade so wiedergeben, wie Hallmark sie nennt: **Floor/FAIL** (muss weg),
   **Reflex** (Standardfehler, mit Grund erlaubt), **Finish** (Feinschliff).

## Schritt 2: Bericht (einfach, für Laien)

- Ergebnis in einem Satz (grün / Probleme gefunden).
- Liste: Problem in einfachen Worten → Datei/Zeile → Vorschlag zur Behebung.
- Was geprüft wurde (Breiten, Browser) und was **nicht** geprüft werden konnte.
- Bei `polish` zusätzlich: vorher/nachher, und `sloplint --kept` bestanden
  (Links, Felder, Überschriften sind noch da).
- Screenshots und Berichte bleiben **lokal** (Lokal-only-Regel von `/dev`), wenn sie Kundendaten zeigen.

## Regeln

- Bestehende Dateien nur bei `polish` ändern, davor Git-Stand sichern (Commit oder Stash-freier Rückfallpunkt).
- Keine Secrets, Logins oder echten Formular-Absendungen im Browser-Test.
- Fotos/Inhalte nie erfinden (Hallmark-Floor 8).
- Dieser Skill gibt keine Freigabe für Deploy, Push oder Löschen.
- Passt zu `/dev` und `/fast-dev`: dort kann dieser Check nach UI-Änderungen laufen.

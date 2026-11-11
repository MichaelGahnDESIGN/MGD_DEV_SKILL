# /mgd-design-check

Nutze den installierten Skill `mgd-design-check` (Quelle: `mgd-design-check/SKILL.md`
in diesem Repository). Er prüft das Design mit Hallmark und dessen Linter im Browser.

Aufruf: `/mgd-design-check <Pfad oder URL>` (Bericht), `/mgd-design-check neu <Beschreibung>`
(neue Seite) oder `/mgd-design-check polish <Pfad>` (nur KI-Merkmale beheben).

Fehlt `puppeteer-core`, global installieren (`npm i -g puppeteer-core`). Fehlt Hallmark,
vorher fragen. Keine Freigabe für Deploy, Push oder Löschen.

In Codex den Skill mit `$mgd-design-check` aufrufen.

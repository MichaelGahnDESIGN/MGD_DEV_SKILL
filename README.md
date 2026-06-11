# DEV-Skill

Der **DEV-Skill** ist eine wiederverwendbare Arbeitsanweisung für AI-Agenten wie
Claude Code, ChatGPT Codex und andere agentische Entwicklungsumgebungen.

Er hilft dabei, ein Softwareprojekt kontrolliert in einen sauberen,
nachvollziehbaren Arbeitsstand zu bringen: lokal, in Git/GitHub, auf
Entwicklungszweigen, in Dev/Staging, auf Live-Systemen, in Backups, in Tests,
in Browser-Smokes und in der begleitenden Projektdokumentation.

Der Skill ist bewusst projektneutral. Er enthält keine festen Projektnamen,
keine privaten Serverpfade und keine kundenspezifischen Annahmen. Stattdessen
weist er den Agenten an, die Regeln, Testbefehle, Deployment-Ziele,
Dokumentationsorte und Sicherheitsanforderungen immer aus dem jeweiligen
Repository abzuleiten.

## Wofür ist dieser Skill gedacht?

Der DEV-Skill ist für Situationen gedacht, in denen ein Agent nicht nur eine
einzelne Datei ändern soll, sondern den Zustand eines Projekts als Ganzes
prüfen muss.

Typische Aufgaben sind:

- offene Änderungen, Branches, Remotes und Tags prüfen;
- lokale Arbeit mit GitHub abgleichen;
- Dev-, Staging- und Live-Stände vergleichen;
- Tests, Builds und Smoke-Checks passend zum Projekt ausführen;
- Browser- und Playwright-Smokes für Weboberflächen durchführen;
- vor Deployments Backups und Rückfallwege berücksichtigen;
- alte Backups, Build-Artefakte und Cache-Dateien vorsichtig einordnen;
- Projektdokumentation und Wissensdatenbanken aktualisieren;
- Risiken, offene Punkte und nächste Schritte verständlich dokumentieren.

Kurz gesagt: Der Skill ist für die Momente gedacht, in denen ein Projekt
geordnet, sicher und nachvollziehbar weitergegeben, veröffentlicht oder
aufgeräumt werden soll.

## Was der Skill nicht tut

Der DEV-Skill ist kein automatisches Deployment-Skript. Er ersetzt keine
menschliche Freigabe, keinen echten Restore-Test und kein Security-Audit.

Er soll Agenten dabei helfen, vorsichtig zu arbeiten. Besonders bei Live-Systemen,
Datenbanken, Uploads, Admin-Bereichen, Zahlungsfunktionen oder personenbezogenen
Daten bleibt eine bewusste menschliche Entscheidung wichtig.

## Sicherheitsprinzipien

Sicherheit und Datenschutz stehen im Mittelpunkt des Skills. Der Agent wird
angewiesen, sensible Daten nicht unnötig zu lesen, zu speichern, zu loggen oder
weiterzugeben.

Der Skill betont unter anderem:

- keine Secrets, Tokens, Passwörter oder `.env*`-Dateien in Git schreiben;
- keine personenbezogenen Daten in Logs, Screenshots oder Abschlussberichte
  übernehmen;
- Zahlungsdaten nicht selbst speichern oder ungeschützt verarbeiten;
- Webhooks und Zahlungsanbieter nur mit offiziellen Prüfverfahren absichern;
- Live-Änderungen nur mit Backup, Restore-Pfad und Tests angehen;
- keine destruktiven Git-, Datenbank- oder Serverbefehle ohne klare Absicherung;
- Backups erst löschen, wenn neue vollständige Backups geprüft wurden;
- mindestens die letzten drei vollständigen Backups je Backup-Familie behalten.

Diese Regeln sind absichtlich streng. Bei Release-, Backup-, Deployment- und
Cleanup-Arbeiten ist ein vorsichtiger Agent deutlich wertvoller als ein schneller
Agent.

## Repository-Struktur

```text
DEV-Skill/
├── README.md
└── dev/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

### `dev/SKILL.md`

Das ist die eigentliche Skill-Datei. Sie enthält das Frontmatter für die
Skill-Erkennung und danach die vollständige Arbeitsanweisung.

### `dev/agents/openai.yaml`

Diese Datei enthält zusätzliche Metadaten für Umgebungen, die eine kurze
Interface-Beschreibung auslesen. Der Skill funktioniert auch dann, wenn ein
Agent nur `SKILL.md` nutzt.

## Installation in ChatGPT Codex oder Codex Desktop

Je nach Codex-Installation können Skill-Ordner unterschiedlich liegen. In vielen
lokalen Setups werden persönliche Skills in einem Codex-Skill-Ordner abgelegt.

Beispiel:

```bash
mkdir -p ~/.codex/skills
cp -R dev ~/.codex/skills/dev
```

Manche Setups verwenden stattdessen einen allgemeinen Agenten-Skill-Ordner:

```bash
mkdir -p ~/.agents/skills
cp -R dev ~/.agents/skills/dev
```

Wenn deine Codex-Version einen anderen Installationspfad dokumentiert, folge
dieser lokalen Dokumentation.

## Installation in Claude Code

In vielen Claude-Code-Setups liegen persönliche Skills in einem Claude-Skill-Ordner.

Beispiel:

```bash
mkdir -p ~/.claude/skills
cp -R dev ~/.claude/skills/dev
```

Danach kann Claude Code den Skill über das Frontmatter in `SKILL.md` finden,
wenn eine Aufgabe zum beschriebenen Einsatzbereich passt.

## Nutzung mit anderen AI-Agenten

Andere AI-Agenten können den Skill ebenfalls verwenden, wenn sie Markdown-Regeln
oder Skill-Dateien laden können.

Allgemeines Vorgehen:

1. Kopiere den Ordner `dev/` in den Skill-, Rules- oder Instructions-Bereich des
   jeweiligen Agents.
2. Stelle sicher, dass der Agent das Frontmatter in `SKILL.md` lesen kann.
3. Hinterlege bei Bedarf einen Trigger wie `/dev`, `dev`, `release workflow`,
   `project sync`, `backup cleanup` oder `deployment readiness`.
4. Prüfe mit einer harmlosen Testaufgabe, ob der Agent den Skill wirklich lädt.

Wenn ein Agent kein eigenes Skill-System besitzt, kann der Inhalt von
`dev/SKILL.md` auch als Projektregel oder wiederverwendbare Arbeitsanweisung
genutzt werden.

## Empfohlene Testaufgaben

Nach der Installation sollte der Skill zuerst mit ungefährlichen Aufgaben
getestet werden.

Beispiele:

```text
/dev prüfe dieses Projekt nur lesend und erstelle einen Zustandsbericht.
```

```text
Nutze den DEV-Skill, aber führe keine Deployments und keine Löschungen aus.
Prüfe nur Git, Tests und Dokumentation.
```

```text
Bereite einen Release-Check vor. Keine Live-Änderungen ohne Rückfrage.
```

```text
/dev prüfe die GitHub-Seite und die README im Browser mit Playwright,
aber ändere keine Einstellungen und lade keine privaten Dateien hoch.
```

Ein korrekt arbeitender Agent sollte zuerst Projektregeln und Dokumentation
lesen, dann Git- und Projektstände prüfen, Tests vorschlagen oder ausführen und
Risiken klar benennen. Er sollte nicht sofort deployen, löschen oder produktive
Systeme verändern.

## Ablauf des Skills

Der Skill führt den Agenten durch neun Bereiche:

1. Projektkontext und Regeln laden.
2. Lokale, entfernte und veröffentlichte Stände vergleichen.
3. Git, GitHub und Branches einordnen.
4. Tests, Builds und allgemeine Smoke-Checks ausführen.
5. Browser- und Playwright-Smokes sicher prüfen.
6. Deployments auf Dev/Staging und Live nur abgesichert angehen.
7. Cleanup und Backup-Retention vorsichtig behandeln.
8. Projektwissen und Wissensdokumentation aktualisieren.
9. Einen kurzen, nachvollziehbaren Abschlussbericht schreiben.

Die Reihenfolge ist wichtig. Sie verhindert, dass ein Agent zu früh löscht,
deployed oder Git-Stände überschreibt.

## Browser- und Playwright-Smokes

Der Skill enthält einen eigenen Workflow für browserbasierte Prüfungen. Er ist
für Webapps, Admin-Panels, Dokumentationsseiten, GitHub-Seiten, Logins,
Checkouts, Uploads und andere nutzernahe Browserpfade gedacht.

Der Agent soll zuerst prüfen, ob es im Projekt bereits Playwright-, Cypress- oder
E2E-Tests gibt. Vorhandene Tests sind besser als neu erfundene Klickpfade.

Wenn ein manueller Browser-Smoke sinnvoller ist, soll der Agent konkrete
sichtbare Erfolgssignale prüfen, zum Beispiel:

- lädt die Startseite ohne sichtbaren Fehler?
- funktioniert die zentrale Navigation?
- sind Dashboard, Listenansicht oder Kernmodul erreichbar?
- zeigt ein Formular erwartete Validierung, ohne echte Daten abzusenden?
- wird die README oder eine Release-Seite korrekt angezeigt?
- gibt es relevante Konsolen- oder Netzwerkfehler?

Wichtig: Screenshots, Logs und Browser-Ausgaben dürfen keine personenbezogenen
Daten, Sessiondaten, Tokens, Zahlungsdaten oder internen Admin-Details enthalten.
Produktive Zahlungen, Löschungen, E-Mail-Versandaktionen, Rechteänderungen oder
andere externe Nebenwirkungen brauchen eine klare Freigabe.

## Anpassung an eigene Projekte

Der Skill bleibt bewusst allgemein. Projektspezifische Details gehören deshalb
in das jeweilige Projekt, nicht in diesen Skill.

Gute Orte dafür sind zum Beispiel:

- `AGENTS.md`
- `CLAUDE.md`
- `GEMINI.md`
- `README.md`
- `docs/`
- Deployment-Runbooks
- Sicherheits- und Backup-Dokumentation

So kann derselbe DEV-Skill in sehr unterschiedlichen Projekten funktionieren,
während jedes Projekt seine eigenen Pfade, Testbefehle, Server, Risiken und
Freigaberegeln sauber dokumentiert.

## Hinweise für Forks und Beiträge

Wenn du den Skill anpasst, achte bitte darauf, dass er projektneutral bleibt.

Bitte vermeide:

- feste Projektnamen;
- private Servernamen oder interne Pfade;
- echte Tokens, Zugangsdaten oder interne URLs;
- projektspezifische Testbefehle als allgemeine Pflicht;
- harte Löschbefehle;
- Live-Deployments ohne Backup- und Rückfalllogik.

Gute Erweiterungen sind zum Beispiel:

- klarere Sicherheitsregeln;
- bessere Hinweise für verschiedene Tech-Stacks;
- zusätzliche vorsichtige Prüfschritte;
- bessere Abschlussberichte;
- kompatible Metadaten für weitere Agenten;
- Übersetzungen, solange die Sicherheitslogik erhalten bleibt.

## Datenschutz und sensible Daten

Dieser Skill ist für reale Projekte gedacht. Dadurch kann er in Umgebungen
auftauchen, in denen personenbezogene Daten, Zahlungsdaten, Authentifizierung,
Uploads, Logs oder Admin-Funktionen eine Rolle spielen.

Der Skill soll Agenten dazu bringen, solche Daten nicht unnötig zu lesen, nicht
in Ausgaben zu kopieren und nicht in Git oder externe Tools zu schreiben.

Trotzdem gilt: Wer diesen Skill nutzt, bleibt für die eigene Umgebung
verantwortlich. Besonders bei Kundendaten, Zahlungsdaten, medizinischen Daten,
rechtlich relevanten Logs oder Produktivdatenbanken sollten zusätzliche
Schutzmaßnahmen und menschliche Freigaben Pflicht sein.

## Lizenz

Dieses Projekt steht unter der MIT-Lizenz.

Du kannst den Skill frei nutzen, kopieren, verändern und weitergeben, auch in
kommerziellen Projekten. Bitte lass dabei den Copyright- und Lizenzhinweis
erhalten.

Der vollständige Lizenztext steht in [`LICENSE`](LICENSE).

## Impressum

Angaben gemäß § 5 DDG:

- Anbieter: Michael Gahn DESIGN
- Inhaber: Michael Gahn
- Anschrift: Dr.-Theodor-Brugsch Str. 12, 08529 Plauen, Sachsen, Deutschland
- Telefon: +49 (0) 176 557 647 48
- E-Mail: Anfrage@Michael-Gahn.de

Umsatzsteuer-Identifikationsnummer gemäß § 27a Umsatzsteuergesetz: DE288143343

Steuernummer: 223/222/02451

Quelle und aktuelle Angaben:
[https://Michael-Gahn.de/Impressum](https://Michael-Gahn.de/Impressum)

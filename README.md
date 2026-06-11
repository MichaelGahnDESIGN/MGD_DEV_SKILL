# DEV-Skill

`DEV-Skill` ist ein projektneutraler Skill fuer AI-Agenten wie Claude Code,
ChatGPT Codex und andere agentische Entwicklungsumgebungen. Er hilft dabei,
ein Softwareprojekt kontrolliert in einen geprueften Arbeitsstand zu bringen:
lokal, in Git/GitHub, auf Entwicklungszweigen, in Dev/Staging, auf Live-Systemen,
in Backups, in Tests und in der begleitenden Wissensdokumentation.

Der Skill ist bewusst nicht an ein bestimmtes Produkt, Framework oder Projekt
gebunden. Er leitet Projektname, Stack, Testbefehle, Deployment-Ziele,
Backup-Orte und Dokumentationsstruktur aus dem jeweiligen Repository und dessen
Regeln ab.

## Wofuer ist dieser Skill gedacht?

Der Skill ist fuer Situationen gedacht, in denen ein AI-Agent nicht nur einzelne
Dateien bearbeiten, sondern den Gesamtzustand eines Projekts bewusst pruefen,
aufräumen und dokumentieren soll.

Typische Einsaetze:

- ein Projekt nach einer Arbeitsphase sauber abschliessen;
- lokale Aenderungen mit Git und GitHub abgleichen;
- offene Branches, Remotes, Tags und Worktrees pruefen;
- Dev-, Staging- und Live-Staende vergleichen;
- Tests, Builds und Smoke-Checks passend zum Projekt ausfuehren;
- vor Deployments Backups und Rueckfallstrategien beruecksichtigen;
- alte Backups, Build-Artefakte und Cache-Dateien vorsichtig inventarisieren;
- Wissensdokumentation, Wikis, `docs/`-Ordner oder vergleichbare Wissensorte aktualisieren;
- Risiken, offene Punkte und naechste Schritte nachvollziehbar dokumentieren.

Der Skill ist besonders nuetzlich fuer Projekte, bei denen mehrere Ebenen
zusammenpassen muessen: Code, GitHub, Deployment, Dokumentation, Backups,
Sicherheit und Betrieb.

## Was der Skill nicht ist

Der Skill ist kein automatisches Deployment-Skript und keine Garantie, dass ein
Projekt gefahrlos live geschaltet werden kann. Er ist eine Arbeitsanweisung fuer
AI-Agenten. Der Agent soll dadurch sorgfaeltiger pruefen, dokumentieren und
kritische Aktionen nicht blind ausfuehren.

Der Skill ersetzt nicht:

- menschliche Freigaben fuer Live-Aenderungen;
- echte Backup- und Restore-Tests;
- rechtliche Pruefung bei Datenschutz, Impressum, Lizenzen oder Zahlungsdaten;
- Sicherheits-Audits durch qualifizierte Personen;
- projektspezifische Deployment-Runbooks.

## Sicherheitsprinzipien

Sicherheit und Datenschutz sind zentrale Bestandteile des Skills. Der Agent wird
angewiesen, bei sensiblen Daten besonders vorsichtig zu arbeiten.

Der Skill betont unter anderem:

- keine Secrets, Tokens, Passwoerter oder `.env*`-Dateien in Git schreiben;
- keine personenbezogenen Daten in Logs, Screenshots oder Abschlussberichte
  uebernehmen;
- Zahlungsdaten niemals selbst speichern oder ungeschuetzt verarbeiten;
- Webhooks und Zahlungsanbieter nur mit offiziellen Verfahren pruefen;
- Live-Aenderungen nur mit Backup, Restore-Pfad und Tests angehen;
- keine destruktiven Git-, Datenbank- oder Serverbefehle ohne klare Absicherung;
- Backups erst loeschen, wenn neue vollstaendige Backups geprueft wurden;
- mindestens die letzten drei vollstaendigen Backups je Backup-Familie behalten.

Diese Regeln sind bewusst streng. Ein AI-Agent soll bei Release-, Backup-,
Deployment- und Cleanup-Arbeiten lieber einmal mehr pruefen als einmal zu viel
loeschen.

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

Das ist die eigentliche Skill-Datei. Sie enthaelt Frontmatter fuer die
Skill-Erkennung und danach die vollstaendige deutschsprachige Arbeitsanweisung.

### `dev/agents/openai.yaml`

Diese Datei enthaelt eine einfache Agenten-Metabeschreibung fuer Umgebungen, die
zusaetzliche Interface-Informationen auslesen. Der Skill funktioniert auch dann,
wenn ein Agent nur `SKILL.md` nutzt.

## Installation in ChatGPT Codex oder Codex Desktop

Je nach Codex-Installation koennen Skill-Verzeichnisse unterschiedlich liegen.
In vielen lokalen Codex-Setups liegt der persoenliche Skill-Ordner hier:

```bash
~/.codex/skills/
```

Installation:

```bash
mkdir -p ~/.codex/skills
cp -R dev ~/.codex/skills/dev
```

Danach sollte der Skill als `dev` verfuegbar sein und bei passenden Anfragen
oder beim Prompt `/dev` geladen werden.

Falls deine Codex-Installation stattdessen `~/.agents/skills/` verwendet, kopiere
den Ordner dorthin:

```bash
mkdir -p ~/.agents/skills
cp -R dev ~/.agents/skills/dev
```

Wichtig: Die genaue Skill-Erkennung haengt von der jeweiligen Codex-Version und
Konfiguration ab. Wenn dein Codex eine andere Skill-Struktur dokumentiert, nutze
diese lokale Dokumentation als fuehrende Quelle.

## Installation in Claude Code

Fuer Claude Code werden persoenliche Skills haeufig unter folgendem Pfad
abgelegt:

```bash
~/.claude/skills/
```

Installation:

```bash
mkdir -p ~/.claude/skills
cp -R dev ~/.claude/skills/dev
```

Danach kann Claude Code den Skill anhand des Frontmatters in `SKILL.md` finden,
wenn eine Aufgabe zum beschriebenen Einsatzbereich passt.

Auch hier gilt: Wenn deine Claude-Code-Version einen anderen offiziellen
Installationspfad oder ein anderes Skill-Format vorgibt, folge der lokalen oder
offiziellen Dokumentation deiner Installation.

## Nutzung mit anderen AI-Agenten

Andere AI-Agenten koennen den Skill ebenfalls verwenden, wenn sie Markdown-Regeln
oder Skill-Dateien laden koennen.

Allgemeines Vorgehen:

1. Kopiere den Ordner `dev/` in den Skill-, Rules- oder Instructions-Ordner des
   jeweiligen Agents.
2. Stelle sicher, dass der Agent das Frontmatter in `SKILL.md` lesen kann.
3. Hinterlege bei Bedarf einen Trigger wie `/dev`, `dev`, `release workflow`,
   `project sync`, `backup cleanup` oder `deployment readiness`.
4. Pruefe mit einer Testaufgabe, ob der Agent den Skill wirklich laedt.

Wenn ein Agent kein Skill-System besitzt, kann der Inhalt von `dev/SKILL.md` auch
als Projektregel, Systemhinweis oder wiederverwendbare Arbeitsanweisung genutzt
werden.

## Empfohlene Testaufgaben

Nach der Installation sollte der Skill mit harmlosen Aufgaben getestet werden.

Beispiele:

```text
/dev pruefe dieses Projekt nur lesend und erstelle einen Zustandsbericht.
```

```text
Nutze den DEV-Skill, aber fuehre keine Deployments und keine Loeschungen aus.
Pruefe nur Git, Tests und Dokumentation.
```

```text
Bereite einen Release-Check vor. Keine Live-Aenderungen ohne Rueckfrage.
```

Ein korrekt arbeitender Agent sollte zuerst Projektregeln und Dokumentation
lesen, dann Git- und Projektstaende pruefen, Tests vorschlagen oder ausfuehren
und Risiken klar benennen. Er sollte nicht sofort Deployments, Loeschungen oder
destruktive Befehle ausfuehren.

## Arbeitslogik des Skills

Der Skill fuehrt den Agenten durch acht grosse Bereiche:

1. Projektkontext und Regeln laden.
2. Lokale, remote und deployte Staende vergleichen.
3. Git, GitHub und Branches vereinheitlichen.
4. Tests, Builds und Smoke-Checks ausfuehren.
5. Deployments auf Dev/Staging und Live nur abgesichert angehen.
6. Cleanup und Backup-Retention vorsichtig behandeln.
7. Projektwissen, Wissensdokumentation oder vergleichbare Wissensorte aktualisieren.
8. Einen kurzen, nachvollziehbaren Abschlussbericht schreiben.

Die Reihenfolge ist wichtig, weil sie verhindert, dass ein Agent zu frueh
loescht, deployt oder Git-Staende ueberschreibt.

## Anpassung an eigene Projekte

Der Skill ist projektneutral. Du solltest projektspezifische Details deshalb
nicht direkt in `dev/SKILL.md` einbauen, sondern im jeweiligen Projekt
dokumentieren.

Gute Orte fuer projektspezifische Regeln:

- `AGENTS.md`
- `CLAUDE.md`
- `GEMINI.md`
- `README.md`
- `docs/`
- `DOKUMENTATION/`
- Deployment-Runbooks
- Sicherheits- und Backup-Dokumentation

So bleibt der DEV-Skill allgemein nutzbar, waehrend jedes Projekt seine eigenen
Pfade, Server, Testbefehle, Backup-Regeln und Risiken sauber beschreibt.

## Was bei Forks und Anpassungen wichtig ist

Wenn du den Skill veraenderst, achte darauf, dass er weiterhin projektneutral
bleibt.

Bitte vermeide:

- feste Projektnamen;
- feste Servernamen oder private Pfade;
- echte Tokens, Zugangsdaten oder interne URLs;
- projektspezifische Testbefehle als allgemeine Pflicht;
- harte Loeschbefehle;
- Live-Deployments ohne Backup- und Rueckfalllogik.

Gute Erweiterungen sind dagegen:

- klarere Sicherheitsregeln;
- bessere Hinweise fuer verschiedene Tech-Stacks;
- zusaetzliche vorsichtige Pruefschritte;
- bessere Abschlussberichte;
- kompatible Metadaten fuer weitere Agenten;
- Uebersetzungen, solange die Sicherheitslogik erhalten bleibt.

## Datenschutz und sensible Daten

Dieser Skill ist bewusst fuer reale Projekte gedacht. Dadurch kann er in
Umgebungen auftauchen, in denen personenbezogene Daten, Zahlungsdaten,
Authentifizierung, Uploads, Logs oder Admin-Funktionen eine Rolle spielen.

Der Skill soll Agenten dazu bringen, solche Daten nicht unnoetig zu lesen,
nicht in Ausgaben zu kopieren und nicht in Git oder externe Tools zu schreiben.

Trotzdem gilt: Wer diesen Skill nutzt, bleibt fuer die eigene Umgebung
verantwortlich. Besonders bei Kundendaten, Zahlungsdaten, medizinischen Daten,
rechtlich relevanten Logs oder Produktivdatenbanken sollten zusaetzliche
Schutzmassnahmen und menschliche Freigaben Pflicht sein.

## Lizenz

Dieses Repository enthaelt derzeit keine ausdrueckliche Open-Source-Lizenz. Ohne
Lizenz gelten normale Urheberrechte. Wenn der Skill oeffentlich frei
weiterverwendet werden soll, sollte bewusst eine passende Lizenzdatei ergaenzt
werden, zum Beispiel MIT, Apache-2.0, CC BY 4.0 oder eine eigene Regelung.

Diese README trifft keine Rechtsberatung und ersetzt keine juristische Pruefung.

## Impressum

Angaben gemaess Impressum des Herausgebers:

[https://Michael-Gahn.de/Impressum](https://Michael-Gahn.de/Impressum)

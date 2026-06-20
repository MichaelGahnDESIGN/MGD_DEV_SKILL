# DEV-Skill

Ich nutze AI-Agenten nicht nur zum Schreiben einzelner Dateien, sondern auch für
die wichtigen Projektaufgaben am Rand: Stände prüfen, GitHub
abgleichen, Backups im Blick behalten, Deployments vorbereiten, Browser-Smokes
machen und am Ende sauber dokumentieren, was wirklich passiert ist.

Aus genau diesem Alltag heraus ist der **DEV-Skill** entstanden.

Der Skill ist eine wiederverwendbare Arbeitsanweisung für Claude Code, ChatGPT
Codex und andere AI-Agenten. Er soll einem Agenten helfen, ein Softwareprojekt
nicht hektisch, sondern kontrolliert in einen nachvollziehbaren Arbeitsstand zu
bringen.

Wichtig: Der Skill ist projektneutral. Er enthält keine festen Projektnamen,
keine privaten Serverpfade und keine kundenspezifischen Annahmen. Der Agent soll
immer aus dem jeweiligen Repository ableiten, welche Regeln, Testbefehle,
Deployment-Ziele, Backup-Orte und Dokumentationsstrukturen gelten.

## Wofür ich den Skill gebaut habe

Ich wollte einen wiederverwendbaren Ablauf für typische Projekt-Situationen, in
denen ein Agent mehr tun muss als nur Code ändern.

Zum Beispiel:

- offene Änderungen, Branches, Remotes und Tags prüfen;
- lokale Arbeit mit GitHub abgleichen;
- Dev-, Staging- und Live-Stände vergleichen;
- Tests, Builds und Smoke-Checks ausführen;
- Weboberflächen mit Playwright oder einem Browser-Tool prüfen;
- Backups und Rückfallwege vor Deployments berücksichtigen;
- Changelog-Dateien pflegen, damit Änderungen später in Updatern, Menüs oder
  Notificationcentern nutzbar werden;
- alte Backups, Build-Artefakte und Cache-Dateien vorsichtig einordnen;
- Projektwissen und Dokumentation aktualisieren;
- am Ende klar berichten, was geprüft wurde und was offen bleibt.

Der Skill ist besonders dann hilfreich, wenn ein Projekt übergeben,
veröffentlicht, aufgeräumt oder für den nächsten Arbeitsschritt vorbereitet
werden soll.

## Was dieser Skill nicht ersetzt

Der DEV-Skill ist kein Autopilot für Live-Deployments. Er ersetzt keine
menschliche Freigabe, keinen Restore-Test, kein Security-Audit und keine
rechtliche Prüfung.

Er ist bewusst vorsichtig formuliert. Wenn es um Produktivsysteme, Datenbanken,
Uploads, Admin-Bereiche, Zahlungen oder personenbezogene Daten geht, soll der
Agent lieber einmal mehr nachweisen, was er tut, als einmal zu schnell handeln.

## Grundprinzipien

Der Skill folgt ein paar einfachen Prinzipien:

- Erst verstehen, dann ändern.
- Erst sichern, dann deployen.
- Erst prüfen, dann behaupten.
- Keine Secrets in Git, Logs, Screenshots oder Abschlussberichte.
- Keine produktiven Löschungen oder Zahlungen ohne klare Freigabe.
- Keine privaten Pfade oder Zugangsdaten in öffentliche Dokumentation.
- Abweichungen und Risiken lieber klar benennen als schönreden.

Diese Haltung ist mir wichtig, weil AI-Agenten sehr schnell sehr viel bewegen
können. Geschwindigkeit ist gut, Nachvollziehbarkeit ist wichtiger.

## Repository-Struktur

```text
DEV-Skill/
├── LICENSE
├── README.md
├── .gitignore
├── .github/
│   └── ISSUE_TEMPLATE/
├── .claude/
│   └── commands/
│       ├── dev.md
│       └── dev-changelog.md
├── .codex/
│   └── commands/
│       ├── dev.md
│       └── dev-changelog.md
└── dev/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

`dev/SKILL.md` ist die eigentliche Skill-Datei. Dort steht die vollständige
Arbeitsanweisung für den Agenten.

`dev/agents/openai.yaml` enthält Metadaten für Agenten-Umgebungen, die ein
kurzes Anzeigeprofil oder einen Standard-Prompt erwarten (z. B. OpenAI-basierte
Tool-Registries). Die Datei ist optional und hat keinen Einfluss auf Claude Code
oder Codex.

`.claude/commands/dev.md`, `.codex/commands/dev.md`,
`.claude/commands/dev-changelog.md` und `.codex/commands/dev-changelog.md` sind
Slash-Command-Vorlagen. Sie sorgen dafür, dass `/dev` und `/dev-changelog` in
Claude Code und ChatGPT Codex als direkte Befehle erkannt werden.

## Installation in ChatGPT Codex oder Codex Desktop

Klone das Repository und lege den `dev/`-Ordner in deinen Codex-Skill-Pfad:

```bash
git clone https://github.com/MichaelGahnDESIGN/MGD-DEV-Skill.git ~/.codex/skills/MGD-DEV-Skill
cp -R ~/.codex/skills/MGD-DEV-Skill/dev ~/.codex/skills/dev
mkdir -p ~/.codex/commands
cp ~/.codex/skills/MGD-DEV-Skill/.codex/commands/*.md ~/.codex/commands/
```

Manche Installationen nutzen stattdessen einen allgemeinen Agenten-Skill-Ordner:

```bash
mkdir -p ~/.agents/skills
cp -R ~/.codex/skills/MGD-DEV-Skill/dev ~/.agents/skills/dev
```

**Updates:** Da das Repository geklont wurde, kannst du später einfach updaten:

```bash
cd ~/.codex/skills/MGD-DEV-Skill && git pull && cp -R dev ~/.codex/skills/dev && mkdir -p ~/.codex/commands && cp .codex/commands/*.md ~/.codex/commands/
```

## Installation in Claude Code

Klone das Repository und lege den `dev/`-Ordner in deinen Claude-Skill-Pfad:

```bash
git clone https://github.com/MichaelGahnDESIGN/MGD-DEV-Skill.git ~/.claude/skills/MGD-DEV-Skill
cp -R ~/.claude/skills/MGD-DEV-Skill/dev ~/.claude/skills/dev
mkdir -p ~/.claude/commands
cp ~/.claude/skills/MGD-DEV-Skill/.claude/commands/*.md ~/.claude/commands/
```

Danach kann Claude Code den Skill über das Frontmatter in `dev/SKILL.md`
erkennen.

**Updates:**

```bash
cd ~/.claude/skills/MGD-DEV-Skill && git pull && cp -R dev ~/.claude/skills/dev && mkdir -p ~/.claude/commands && cp .claude/commands/*.md ~/.claude/commands/
```

## Nutzung mit anderen AI-Agenten

Du kannst den Skill auch mit anderen Agenten nutzen, wenn sie Markdown-Regeln
oder Skill-Dateien laden können.

Allgemein reicht meistens:

1. Den Ordner `dev/` in den Skill-, Rules- oder Instructions-Bereich des Agents
   kopieren.
2. Prüfen, ob der Agent das Frontmatter in `SKILL.md` erkennt.
3. Einen Trigger wie `/dev`, `dev`, `release workflow`, `project sync`,
   `backup cleanup` oder `deployment readiness` verwenden.
4. Mit einer ungefährlichen Aufgabe testen, ob der Agent den Skill wirklich
   nutzt.

Wenn ein Agent kein eigenes Skill-System hat, kannst du den Inhalt von
`dev/SKILL.md` auch als Projektregel oder wiederverwendbare Arbeitsanweisung
einsetzen.

## Gute erste Testaufgaben

Ich würde den Skill zuerst mit lesenden oder risikoarmen Aufgaben testen.

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

```text
/dev-changelog führe die CHANGELOG.md für die aktuellen Änderungen.
Nutze Git-Diff und Commits als Quelle, aber schreibe keine Secrets,
internen Serverpfade oder personenbezogenen Daten hinein.
```

Ein gut arbeitender Agent sollte dabei zuerst Projektregeln und Dokumentation
lesen, dann Git- und Projektstände prüfen, Tests vorschlagen oder ausführen und
Risiken klar benennen. Er sollte nicht sofort deployen, löschen oder produktive
Systeme verändern.

Bei `/dev-changelog` sollte der Agent fokussiert bleiben: Er sucht oder erstellt
eine `CHANGELOG.md`, hält das bestehende Format ein und schreibt Änderungen so,
dass Menschen sie verstehen und spätere Tools sie zuverlässig auslesen können.
Gute Kategorien sind zum Beispiel `Neu`, `Geändert`, `Behoben`, `Sicherheit`,
`Technisch` und `Dokumentation`.

## Ablauf im Skill

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

Der Zusatzbefehl `/dev-changelog` nutzt denselben Sicherheitsrahmen, startet
aber nur den Changelog-Assistenten. Er ist sinnvoll, wenn du nach einer Änderung
oder vor einem Release die sichtbaren Änderungen dokumentieren möchtest, ohne
gleich den vollständigen Release-, Backup- oder Deployment-Ablauf zu starten.

Die Reihenfolge ist wichtig. Sie soll verhindern, dass ein Agent zu früh löscht,
deployed oder Git-Stände überschreibt.

## Browser- und Playwright-Smokes

Browser-Smokes sind ein eigener Teil des Skills, weil viele Probleme erst im
sichtbaren Produkt auffallen: kaputte Navigation, falsche README, nicht geladene
Assets, Login-Probleme, Konsolenfehler oder nicht erreichbare Admin-Bereiche.

Der Agent soll zuerst prüfen, ob es im Projekt bereits Playwright-, Cypress- oder
E2E-Tests gibt. Vorhandene Tests sind besser als neu erfundene Klickpfade.

Wenn ein manueller Browser-Smoke sinnvoller ist, soll der Agent sichtbare
Erfolgssignale prüfen:

- lädt die Startseite ohne sichtbaren Fehler?
- funktioniert die zentrale Navigation?
- sind Dashboard, Listenansicht oder Kernmodul erreichbar?
- zeigt ein Formular erwartete Validierung, ohne echte Daten abzusenden?
- wird die README oder eine Release-Seite korrekt angezeigt?
- gibt es relevante Konsolen- oder Netzwerkfehler?

Screenshots, Logs und Browser-Ausgaben dürfen keine personenbezogenen Daten,
Sessiondaten, Tokens, Zahlungsdaten oder internen Admin-Details enthalten.
Produktive Zahlungen, Löschungen, E-Mail-Versandaktionen, Rechteänderungen oder
andere externe Nebenwirkungen brauchen eine klare Freigabe.

## Anpassung an eigene Projekte

Der Skill selbst soll allgemein bleiben. Projektspezifische Details gehören in
das jeweilige Projekt.

Gute Orte dafür sind zum Beispiel:

- `AGENTS.md`
- `CLAUDE.md`
- `GEMINI.md`
- `README.md`
- `docs/`
- Deployment-Runbooks
- Sicherheits- und Backup-Dokumentation

So kann derselbe DEV-Skill in unterschiedlichen Projekten funktionieren, während
jedes Projekt seine eigenen Pfade, Testbefehle, Server, Risiken und Freigaben
sauber dokumentiert.

## Weitere Dokumentation

Im [Wiki](https://github.com/MichaelGahnDESIGN/MGD-DEV-Skill/wiki) findest du
zusätzliche Erklärungen und konkrete Workflows, zum Beispiel für
Backup-Verwaltung, Speicherplatz sparen, Release-Checks, Browser-Smokes und
Changelog-Pflege.

## Verwandte Projekte Von Michael Gahn DESIGN

Der DEV-Skill gehört zu einer kleinen Werkzeugfamilie für KI-gestützte
Projektarbeit.

- [AI-Basic-Projektordner](https://github.com/MichaelGahnDESIGN/AI-Basic-Projektordner)  
  Eine saubere Projektvorlage mit Regeln, Dokumentation, Agentenstruktur und
  Sicherheitsgrenzen. Sinnvoll als Basis für neue Projekte.

- [AI Project Updater Skill](https://github.com/MichaelGahnDESIGN/AI-Project-Updater-Skill)  
  Ein geführter Assistent für lokale Staging-Umgebungen, Docker-Planung,
  Update-Vorbereitung und sichere Staging-zu-Live-Abläufe. Das Repository ist
  während der Entwicklung zunächst privat.

- [ProjectClean-Skill](https://github.com/MichaelGahnDESIGN/ProjectClean-Skill)  
  Ein Abschluss- und Aufräum-Skill für Versionen, Tests, Commits, Backups,
  Dokumentation und vorsichtiges Cleanup.

- [AI-PlayTest-Skill](https://github.com/MichaelGahnDESIGN/AI-PlayTest-Skill)  
  Ein Skill für Play-Tests aus Sicht echter Nutzerrollen, lokal, auf Staging
  oder vorsichtig auf Live.

- [Claude-Codex-MCP](https://github.com/MichaelGahnDESIGN/Claude-Codex-MCP)  
  Ein lokales MCP-System für Aufgaben, Chat und Übergaben zwischen Claude,
  Codex und weiteren KI-Agenten.

## Beiträge und Forks

Wenn du den Skill anpasst oder forkst, achte bitte darauf, dass er
projektneutral bleibt.

Bitte vermeide:

- feste Projektnamen;
- private Servernamen oder interne Pfade;
- echte Tokens, Zugangsdaten oder interne URLs;
- projektspezifische Testbefehle als allgemeine Pflicht;
- harte Löschbefehle;
- Live-Deployments ohne Backup- und Rückfalllogik.

Gute Erweiterungen sind willkommen, zum Beispiel:

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

## 🔒 Lokal-only — Playtests, Backups & sensible Daten

Diese Daten dürfen **niemals** die lokale Maschine verlassen — weder nach GitHub noch nach Live/Deploy:

- **Playtests:** Play-Test-Branches (`PlayTest*`) und -Artefakte (`PlayTest/`, Protokolle, Screenshots) bleiben lokal.
- **Backups:** DB-Dumps, `*.sql`, `*.sql.gz`, `BACKUPS/` bleiben lokal — nie nach GitHub, nie in den Webroot/Live.
- **Sensible Daten:** `.env*` (außer `.env.example`), Tokens, API-Keys, Passwörter, `*.pem`, `*.key`, Zugangsdaten — niemals committen/pushen/deployen.
- **Push-Disziplin:** Nur den Hauptbranch (`main`) pushen, **niemals** `git push --all`/`--mirror`. `PlayTest*`-Branches werden nie gepusht.

Alle genannten Muster gehören in `.gitignore`. Technische Absicherung: der Pre-Push-Hook aus dem [MGD-DEV-Skill](https://github.com/MichaelGahnDESIGN/MGD-DEV-Skill) (`dev/hooks/pre-push`) blockiert solche Pushes hart — empfohlen, am besten global via `git config --global core.hooksPath ~/.git-hooks`.

---

## Verwandte MGD Projekte

| Projekt | Beschreibung |
|---------|-------------|
| [MGD-AI-Basic-Projektordner](https://github.com/MichaelGahnDESIGN/MGD-AI-Basic-Projektordner) | Projektvorlage für KI-Agenten |
| [MGD-App-Updater-Skill](https://github.com/MichaelGahnDESIGN/MGD-App-Updater-Skill) | Software-Update-Systeme planen und implementieren |
| [MGD-Bugreport-Skill](https://github.com/MichaelGahnDESIGN/MGD-Bugreport-Skill) | Feedback-Hub: Bug-Meldung, Ideen und Support |
| [MGD-ToDo-SKILL](https://github.com/MichaelGahnDESIGN/MGD-ToDo-SKILL) | Aufgabenmanagement direkt im Projekt-Repo |
| [MGD-ProjectClean-Skill](https://github.com/MichaelGahnDESIGN/MGD-ProjectClean-Skill) | Abschluss- und Aufräum-Workflow |
| [MGD-AI-Project-Updater-Skill](https://github.com/MichaelGahnDESIGN/MGD-AI-Project-Updater-Skill) | Geführter Projekt-Assistent für Staging und Updates |

→ Alle öffentlichen Projekte: [github.com/MichaelGahnDESIGN](https://github.com/MichaelGahnDESIGN)

---

## Impressum

Angaben gemäß § 5 DDG — Siehe [`IMPRESSUM.md`](IMPRESSUM.md).

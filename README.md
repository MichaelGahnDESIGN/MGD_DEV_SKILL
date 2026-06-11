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
└── dev/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

`dev/SKILL.md` ist die eigentliche Skill-Datei. Dort steht die vollständige
Arbeitsanweisung für den Agenten.

`dev/agents/openai.yaml` enthält zusätzliche Metadaten für Umgebungen, die eine
kurze Beschreibung oder einen Standard-Prompt anzeigen.

## Installation in ChatGPT Codex oder Codex Desktop

Je nach Codex-Installation können persönliche Skills an unterschiedlichen Orten
liegen. In vielen Setups funktioniert dieser Weg:

```bash
mkdir -p ~/.codex/skills
cp -R dev ~/.codex/skills/dev
```

Manche Installationen nutzen stattdessen einen allgemeinen Agenten-Skill-Ordner:

```bash
mkdir -p ~/.agents/skills
cp -R dev ~/.agents/skills/dev
```

Wenn deine Codex-Version einen anderen Pfad vorgibt, nimm bitte den Pfad aus
deiner lokalen Dokumentation.

## Installation in Claude Code

Für Claude Code werden persönliche Skills häufig in einem Claude-Skill-Ordner
abgelegt.

Beispiel:

```bash
mkdir -p ~/.claude/skills
cp -R dev ~/.claude/skills/dev
```

Danach kann Claude Code den Skill über das Frontmatter in `dev/SKILL.md`
erkennen.

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

Ein gut arbeitender Agent sollte dabei zuerst Projektregeln und Dokumentation
lesen, dann Git- und Projektstände prüfen, Tests vorschlagen oder ausführen und
Risiken klar benennen. Er sollte nicht sofort deployen, löschen oder produktive
Systeme verändern.

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

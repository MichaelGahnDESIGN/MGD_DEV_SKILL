<!-- MGD-HEADER -->
<p align="center"><a href="https://Michael-Gahn.de"><img src="assets/mgd-logo.png" alt="Michael Gahn DESIGN" width="48"></a></p>

<p align="center"><img src="assets/banner.svg" alt="MGD DEV" width="100%"></p>

<p align="center">
  <img alt="Lizenz" src="https://img.shields.io/github/license/MichaelGahnDESIGN/MGD_DEV_SKILL?label=Lizenz">
  <a href="https://github.com/MichaelGahnDESIGN/MGD_DEV_SKILL/releases/latest"><img alt="Release" src="https://img.shields.io/github/v/release/MichaelGahnDESIGN/MGD_DEV_SKILL?label=Release"></a>
  <img alt="Sprache" src="https://img.shields.io/badge/Sprache-Shell-2f6fed">
  <a href="https://Michael-Gahn.de"><img alt="by Michael Gahn DESIGN" src="https://img.shields.io/badge/by-Michael%20Gahn%20DESIGN-cd1616"></a>
</p>
<!-- /MGD-HEADER -->

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

## Empfohlene Begleit-Skills

Der DEV-Skill spielt bewusst mit drei weiteren Skills von Michael Gahn DESIGN
zusammen, die im selben Projekt oft sinnvoll sind:

- **[Fragenkatalog-Skill](https://github.com/MichaelGahnDESIGN/Fragenkatalog-Skill)**
  — interaktiver Design-Fragenkatalog mit KI-Antworten aus wählbarer
  Experten-Perspektive, inklusive Rechts-Kategorie.
- **[MGD_Todo_SKILL](https://github.com/MichaelGahnDESIGN/MGD_Todo_SKILL)**
  — selbst-gehostete `TODO.html` mit Bearbeiten-Funktion und
  Dokument-Verknüpfung.
- **[MGD_Living-Documentation](https://github.com/MichaelGahnDESIGN/MGD_Living-Documentation)**
  — lebendige Projektdokumentation (Entscheidungen, offene Punkte, Risiken,
  Testnachweise) als HTML+Markdown.

Keiner davon ist Voraussetzung für den DEV-Skill — er funktioniert auch ganz
allein. Wo sie aber vorhanden sind, ergänzen sie sich: der DEV-Skill prüft
Stände, Tests und Deployments, das Todo hält offene Befunde fest, die
Living-Documentation dokumentiert Entscheidungen und Risiken dauerhaft, und
der Fragenkatalog klärt offene Design- und Projektfragen, bevor sie zu
stillschweigenden Annahmen werden.

Beim **allerersten** `/dev`-, `/dev-fast`- oder `/dev-changelog`-Lauf in
einem Projekt prüft der Skill aktiv, welche dieser Begleit-Skills bereits
installiert sind, und fragt bei fehlenden nach, ob sie mitinstalliert werden
sollen — siehe `dev/SKILL.md`, Abschnitt „Companion-Skill-Check". Bei jedem
weiteren Lauf im selben Projekt wird nicht erneut gefragt.

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
│       ├── dev-changelog.md
│       └── dev-fast.md
├── .codex/
│   └── commands/
│       ├── dev.md
│       ├── dev-changelog.md
│       └── dev-fast.md
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
`.claude/commands/dev-changelog.md`, `.codex/commands/dev-changelog.md`,
`.claude/commands/dev-fast.md` und `.codex/commands/dev-fast.md` sind
Slash-Command-Vorlagen. Sie sorgen dafür, dass `/dev`, `/dev-changelog` und
`/dev-fast` in Claude Code und ChatGPT Codex als direkte Befehle erkannt
werden.

## Installation in ChatGPT Codex oder Codex Desktop

Klone das Repository und lege den `dev/`-Ordner in deinen Codex-Skill-Pfad:

```bash
git clone https://github.com/MichaelGahnDESIGN/MGD_DEV_SKILL.git ~/.codex/skills/MGD-DEV-Skill
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
git clone https://github.com/MichaelGahnDESIGN/MGD_DEV_SKILL.git ~/.claude/skills/MGD-DEV-Skill
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

```text
/dev-fast mir geht bald das Kontextfenster aus. Zerlege die Aufgabe in
den kleinsten deploybaren Teilschritt, prüfe nur das Nötigste und geh
sofort live, statt am Ende alles auf einmal zu sammeln.
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

Der Zusatzbefehl `/dev-fast` nutzt denselben Sicherheitsrahmen, ist aber auf
Geschwindigkeit statt Gründlichkeit getrimmt: kleinste deploybare Teilschritte,
minimale Prüfung, sofortiges Commit + Deploy je Schritt. Sinnvoll, wenn nur
noch wenig Kontextfenster oder Nutzungslimit übrig ist und trotzdem etwas
Fertiges live gehen soll — nutze stattdessen `/dev`, wenn genug Budget für
einen vollständig geprüften Release da ist.

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

Im [Wiki](https://github.com/MichaelGahnDESIGN/MGD_DEV_SKILL/wiki) findest du
zusätzliche Erklärungen und konkrete Workflows, zum Beispiel für
Backup-Verwaltung, Speicherplatz sparen, Release-Checks, Browser-Smokes und
Changelog-Pflege.

## Verwandte Projekte Von Michael Gahn DESIGN

Der DEV-Skill gehört zu einer kleinen Werkzeugfamilie für KI-gestützte
Projektarbeit. Die vollständige Liste mit Beschreibung und Zusammenspiel
steht weiter unten im Abschnitt „Verwandte MGD Projekte".

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

Alle genannten Muster gehören in `.gitignore`. Technische Absicherung: der Pre-Push-Hook aus dem [MGD_DEV_SKILL](https://github.com/MichaelGahnDESIGN/MGD_DEV_SKILL) (`dev/hooks/pre-push`) blockiert solche Pushes hart — empfohlen, am besten global via `git config --global core.hooksPath ~/.git-hooks`.

---

## Verwandte MGD Projekte

Direkte Begleit-Skills (siehe auch „Empfohlene Begleit-Skills" oben):

| Projekt | Beschreibung | Warum gut mit DEV_SKILL |
|---------|-------------|--------------------------|
| [Fragenkatalog-Skill](https://github.com/MichaelGahnDESIGN/Fragenkatalog-Skill) | Interaktiver Design-Fragenkatalog mit KI-Antworten aus wählbarer Experten-Perspektive, inkl. Rechts-Kategorie | Offene Design- und Projektfragen vor einem Release klären, statt sie stillschweigend anzunehmen |
| [MGD_Todo_SKILL](https://github.com/MichaelGahnDESIGN/MGD_Todo_SKILL) | Selbst-gehostete `TODO.html` mit Bearbeiten-Funktion und Dokument-Verknüpfung | Vor jedem Release `/todo` prüfen — Befunde aus dem DEV-Lauf, die über die Session hinaus wichtig bleiben, landen hier |
| [MGD_Living-Documentation](https://github.com/MichaelGahnDESIGN/MGD_Living-Documentation) | Lebendige Projektdokumentation (Entscheidungen, offene Punkte, Risiken, Testnachweise) als HTML+Markdown | Vor jedem Release den Living-Documentation-Stand prüfen — Schritt 8 des DEV-Skills (Projektwissen aktualisieren) findet hier einen vorbereiteten Zielort |

Weitere Projekte aus derselben Werkzeugfamilie:

| Projekt | Beschreibung |
|---------|-------------|
| [MGD_AI-Basic-Projektordner_TOOL](https://github.com/MichaelGahnDESIGN/MGD_AI-Basic-Projektordner_TOOL) | Projektvorlage für KI-Agenten mit Regeln, Dokumentation, Agentenstruktur und Sicherheitsgrenzen |
| [MGD_Software-Updater_SKILL](https://github.com/MichaelGahnDESIGN/MGD_Software-Updater_SKILL) | Software-Update-Systeme planen und implementieren |
| [MGD_BugReport_SKILL](https://github.com/MichaelGahnDESIGN/MGD_BugReport_SKILL) | Feedback-Hub: Bug-Meldung, Ideen und Support |
| [MGD_ProjectClean_SKILL](https://github.com/MichaelGahnDESIGN/MGD_ProjectClean_SKILL) | Abschluss- und Aufräum-Workflow für Versionen, Tests, Commits, Backups und Dokumentation |
| [MGD_AI-Project-Updater_SKILL](https://github.com/MichaelGahnDESIGN/MGD_AI-Project-Updater_SKILL) | Geführter Projekt-Assistent für lokale Staging-Umgebungen, Docker-Planung und Updates (Repository während der Entwicklung zunächst privat) |
| [MGD_AI-PlayTest_SKILL](https://github.com/MichaelGahnDESIGN/MGD_AI-PlayTest_SKILL) | Play-Tests aus Sicht echter Nutzerrollen, lokal, auf Staging oder vorsichtig auf Live |
| [MGD_Claude-Codex_MCP](https://github.com/MichaelGahnDESIGN/MGD_Claude-Codex_MCP) | Lokales MCP-System für Aufgaben, Chat und Übergaben zwischen Claude, Codex und weiteren KI-Agenten |

→ Alle öffentlichen Projekte: [github.com/MichaelGahnDESIGN](https://github.com/MichaelGahnDESIGN)

---

## Impressum

Angaben gemäß § 5 DDG — Siehe [`IMPRESSUM.md`](IMPRESSUM.md).

<!-- MGD-LEGAL -->
---

## Lizenz

Dieses Projekt steht unter der [MIT-Lizenz](https://opensource.org/license/mit). Den vollständigen Text enthält die Datei [LICENSE](LICENSE).

## Impressum

**Angaben gemäß § 5 DDG (Digitale-Dienste-Gesetz)**

Michael Gahn DESIGN  
Michael Gahn  
Dr.-Theodor-Brugsch Str. 12  
08529 Plauen  
Sachsen  
Deutschland

Tel.: +49 (0) 151 59156639  
E-Mail: Anfrage@Michael-Gahn.de

Umsatzsteuer-Identifikationsnummer gemäß § 27 a Umsatzsteuergesetz:  
Steuernummer: 223/222/02451  
Ust-ID: DE288143343

Wir sind zur Teilnahme an einem Streitbeilegungsverfahren vor einer Verbraucherschlichtungsstelle weder verpflichtet noch bereit.

**Redaktionell verantwortlich:**

Michael Gahn DESIGN  
Michael Gahn  
Dr.-Theodor-Brugsch Str. 12  
08529 Plauen  
Sachsen  
Deutschland

Tel.: +49 (0) 151 59156639  
E-Mail: Anfrage@Michael-Gahn.de
<!-- /MGD-LEGAL -->

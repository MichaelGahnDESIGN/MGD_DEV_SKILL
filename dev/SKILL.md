---
name: dev
description: Use when the user invokes /dev or asks to synchronize any software project across local worktree, GitHub, main/dev branches, staging/live deployments, backups, cleanup, browser/Playwright smoke tests, and project knowledge documentation.
---

# Dev

## Ziel

Dieser Skill bringt ein Projekt in einen einheitlichen, geprueften Arbeitsstand: lokal, Git/GitHub, Hauptbranch, Entwicklungszweige, Dev/Staging, Live, Backups, Tests und Wissensdokumentation. Er ist fuer Abschluss-, Aufraeum-, Release-, Deploy- und Weiterarbeitsstaende in jedem Projekt gedacht.

Der Skill ist projektneutral. Projektname, Stack, Live-/Staging-Ziele, Backup-Pfade, Testbefehle und Dokumentationsorte werden immer aus dem aktuellen Repository, den Projektregeln und der vorhandenen Dokumentation abgeleitet.

## Harte Sicherheitsregeln

- Niemals Secrets, Tokens, Passwoerter, `.env*`, private Serverpfade mit Zugangsdaten, echte E-Mail-Zugangsdaten, Zahlungsdaten oder personenbezogene Daten in Git, Logs, Screenshots, Wissensdokumentation oder Abschlussberichte schreiben.
- Niemals `git reset --hard`, `git clean -fd`, Backup-Loeschung, Server-Loeschung, Datenbankoperationen, Migrationen oder Live-Aenderungen ohne vorheriges geprueftes Backup ausfuehren.
- Live gilt nur als Wahrheit, wenn GitHub, lokaler Commit, dokumentierte Version, API-/Frontend-/Admin-Builds und Smoke-Tests plausibel zusammenpassen. Bei Widerspruch zuerst Befund dokumentieren.
- Backups erst loeschen, nachdem ein neues vollstaendiges Backup erstellt und per SHA-256 oder gleichwertigem Hashmanifest geprueft wurde. Danach nur aeltere Backups entfernen, sodass mindestens die letzten 3 vollstaendigen Backups je Backup-Familie erhalten bleiben.
- `.trash`, generierte Build-Artefakte, App-Bundles, alte Archive und Cache-Verzeichnisse nur loeschen, wenn sie eindeutig reproduzierbar sind und nicht mehr als Restore- oder Referenzstand gebraucht werden.
- Bei Zahlungs-, Auth-, Profil-, Upload-, Rechnungs-, Admin-, Logging- und personenbezogenen Daten besonders streng nach Datenminimierung, Zugriffsbeschraenkung, Verschluesselung/Hashing, sicherer Token-Ablage und DSGVO-Naehe arbeiten.

## Ablauf

### 1. Projektkontext und Regeln laden

Lies vor Aenderungen die vorhandenen Regeln und Betriebsdokumente. Typische Kandidaten sind:

- `AGENTS.md`, `CLAUDE.md`, `GEMINI.md` oder vergleichbare Agentenregeln;
- `GRUNDREGELN.md`, Projektregeln, Architektur- und Sicherheitsdokumente;
- `README.md`, `docs/`, `AI/`, `PROJEKT/`, `DOKUMENTATION/` und vorhandene `SKILL.md`-Dateien;
- Betriebsdokumentation zu Backups, Deployment, Versionen, Staging, Live, Monitoring und Restore;
- Paket- und Stack-Hinweise wie `package.json`, `composer.json`, `pubspec.yaml`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `Dockerfile` und CI-Workflows.

Wenn erwartete Dokumente fehlen, dokumentiere das als offenen Punkt und leite vorsichtig aus der Repo-Struktur ab, statt projektspezifische Annahmen zu erfinden.

Pruefe danach:

- `git status --short --branch`;
- aktuelle Branches, Remotes, Tags und offene Worktrees;
- Projektname, Hauptbranch und aktive Arbeitsbranch;
- lokale Version aus App-/API-/Package-Dateien;
- dokumentierte oder erreichbare Dev-/Staging-/Live-Versionen, falls vorhanden.

### 2. Staende vergleichen

Vergleiche:

- lokaler `HEAD`, Hauptbranch, aktive Branch und Remote-Hauptbranch;
- GitHub-Remote mit `git fetch --all --prune --tags`;
- lokale offene Aenderungen und untracked Dateien;
- dokumentierte Versionen, Tags, Changelog und Deploy-Metadaten;
- Dev-/Staging-/Live-Versionen ueber vorhandene APIs, HTML-Metadaten, Healthchecks, Admin-Anzeigen oder Deployment-Logs;
- lokale Builds gegen deployte Builds, wenn Artefakte oder Build-IDs vorhanden sind.

Wenn ein Stand abweicht, entscheide konservativ:

- lokale ungesicherte Arbeit sichern, committen oder branchieren;
- nur Fast-Forward-Merges nutzen, wenn moeglich;
- Konflikte nicht blind loesen;
- Live nicht ueberschreiben, bevor Backup, Restore-Pfad und Tests geklaert sind;
- bewusst abweichende Staende dokumentieren.

### 3. Git, GitHub und Vereinheitlichung

Zielzustand:

- relevante Arbeit ist auf dem vorgesehenen Hauptbranch oder sauber in einer dokumentierten Feature-Branch;
- der Remote-Stand ist aktuell und nachvollziehbar;
- lokale Arbeitskopie ist sauber oder bewusst mit offenen Punkten dokumentiert;
- nicht mehr benoetigte lokale Feature-Branches sind geloescht oder als weiterhin relevant dokumentiert;
- Dev/Staging und Live laufen auf demselben freigegebenen Stand oder ihre bewusste Abweichung ist dokumentiert.

Nutze bevorzugt:

- `git merge --ff-only`, wenn moeglich;
- normale Merge-Commits nur nach Pruefung;
- Pull Requests fuer nachvollziehbare Integration, wenn das Projekt so arbeitet;
- keine Rewrites auf geteilten Branches ohne ausdrueckliche Freigabe.

### 4. Tests, Checks und Smokes

Fuehre passend zum Projekt aus, was die Dokumentation, CI oder der Stack nahelegt:

- JavaScript/TypeScript/Web: Lint, Typecheck, Unit-/Integrationstests, Build, Playwright/Cypress-Smokes.
- PHP/Symfony/Laravel/WordPress: `php -l`, PHPUnit, Framework-Checks, relevante Console-/WP-CLI-Kommandos.
- Flutter/Dart: `flutter analyze`, relevante Tests, Web-/App-Builds.
- Python: Lint/Format-Check, Typecheck, Pytest, Migrations-/Management-Checks.
- Datenbank: Migrationen nur nach Backup pruefen; Schema- und Seed-Kommandos dokumentieren.
- Browser: Playwright oder Browser-Plugin fuer Login, zentrale Module, Admin-Bereiche und Live-Smokes.
- Betrieb: vorhandene Healthcheck-, Stability-, Deploy- oder Monitoring-Skripte nutzen.

Wenn ein erwartetes Tool nicht verfuegbar ist, dokumentiere den Grund und nutze den besten sicheren Ersatz, zum Beispiel Browser-, Curl- oder API-Smokes.

### 5. Browser- und Playwright-Smokes

Nutze Playwright, ein Browser-Plugin oder ein vergleichbares Browser-Automationswerkzeug, wenn das Projekt eine Weboberflaeche, ein Admin-Panel, eine Dokumentationsseite, eine GitHub-Seite, eine Login-Strecke, einen Checkout, Uploads oder andere nutzernahe Browserpfade hat.

Arbeitsweise:

- pruefe zuerst, ob es bereits projektinterne Playwright-, Cypress- oder E2E-Tests gibt, und bevorzuge diese gegenueber neu erfundenen Klickpfaden;
- starte lokale Apps nur ueber dokumentierte Befehle und notiere URL, Branch, Commit und Umgebung;
- teste Dev/Staging vor Live, wenn beide erreichbar sind;
- lade Seiten nach Builds oder Deployments bewusst neu und pruefe eine konkrete sichtbare Erfolgsaussage, nicht nur den HTTP-Status;
- erfasse Browser-Konsole, Netzwerkfehler oder sichtbare Fehlermeldungen nur soweit sie fuer die Diagnose gebraucht werden;
- erstelle Screenshots nur, wenn sie fuer Nachvollziehbarkeit, Vergleich oder Fehlerdiagnose nuetzlich sind;
- speichere oder veroeffentliche keine Screenshots mit personenbezogenen Daten, Tokens, E-Mail-Adressen, Zahlungsdaten, Sessiondaten, Kundendaten oder internen Admin-Details;
- gib niemals Passwoerter, Einmalcodes, API-Keys, Zahlungsdaten oder andere Secrets in Browserseiten ein, ausser die Aufgabe, Umgebung und Freigabe sind eindeutig dokumentiert;
- verwende fuer Logins nach Moeglichkeit Testkonten, Seed-Daten oder bereits dokumentierte sichere Testablaeufe;
- bestaetige keine produktiven Zahlungen, Loeschungen, E-Mail-Versandaktionen, Rechteaenderungen oder externen Nebenwirkungen ohne ausdrueckliche Freigabe.

Typische Smoke-Pfade:

- Startseite oder zentrale App-Shell laedt ohne sichtbaren Fehler;
- Login- oder Auth-Status wird korrekt angezeigt, soweit sicher testbar;
- Hauptnavigation, Dashboard, Listenansicht oder Kernmodul ist erreichbar;
- Formularvalidierung zeigt erwartete Hinweise ohne echte Daten zu senden;
- Admin- oder Profilbereiche geben keine sensiblen Informationen unnoetig preis;
- Checkout- oder Zahlungsstrecken werden nur im Test-/Sandbox-Modus geprueft;
- GitHub-, Dokumentations- oder Release-Seiten zeigen aktuellen Commit, README, Changelog oder Artefakte.

Berichte Browser-Ergebnisse knapp mit:

- getesteter URL und Umgebung;
- Tool oder vorhandener Testbefehl;
- geprueften Nutzerpfaden;
- Ergebnis je Pfad;
- relevanten Konsolen-/Netzwerkfehlern ohne Secrets;
- Screenshot-Pfad oder bewusster Verzicht auf Screenshots;
- offenen Risiken, zum Beispiel fehlender Login, privates Repository, nicht erreichbares Staging oder fehlende Testdaten.

### 6. Deploy auf Dev/Staging und Live

Vor jedem Deploy:

- vollstaendiges Backup erstellen;
- Datenbankdump einschliessen, wenn eine Datenbank betroffen ist;
- Uploads/Medien/Speicherorte einschliessen, wenn sie fuer Restore gebraucht werden;
- Hashmanifest erzeugen und pruefen;
- Restore-Pfad und Backup-Ort im Bericht nennen;
- Secrets nicht anzeigen oder speichern.

Deploy-Reihenfolge:

1. Dev/Staging aktualisieren und smoke-testen.
2. Live erst aktualisieren, wenn Backup, Tests und Rueckfallstrategie klar sind.
3. Migrationen/Schema-Kommandos nur nach Backup und mit dokumentierter Reihenfolge ausfuehren.
4. Live-Versionen, Healthchecks und zentrale Nutzerpfade pruefen.
5. Browser-Smoke mit Playwright, Browser-Plugin oder dokumentiertem Ersatz durchfuehren.

### 7. Cleanup und Backup-Retention

Erstelle zuerst eine Inventarliste:

- lokale Backups;
- Server-Backups;
- Staging-/Dev-Backups;
- Datenbankdumps;
- Build-Artefakte;
- alte Worktrees;
- lokale Branches;
- Cache-/Temp-Verzeichnisse;
- bekannte Archiv- oder Restore-Staende.

Loesche nur:

- eindeutig generierte, reproduzierbare Artefakte;
- alte Backups oberhalb der letzten 3 vollstaendigen, geprueften Backups je Backup-Familie;
- zusammengefuehrte lokale Branches/Worktrees, die keine einzigartige Arbeit enthalten;
- Cache-/Temp-Dateien, die keine Projekt- oder Restore-Information enthalten.

Nicht loeschen:

- letzte 3 vollstaendige Backups je Backup-Familie;
- Backups, die in Versionen, Deployment-Dokumentation oder Abschlussberichten als Restore-Punkt referenziert sind;
- ungepruefte Datenbankdumps;
- unbekannte Dateien mit moeglichen Secrets;
- Nutzeruploads, Medien, Rechnungsdaten, Logs mit rechtlicher Relevanz oder Auditdaten ohne klare Freigabe.

### 8. Projektwissen aktualisieren

Aktualisiere, wenn vorhanden und erreichbar, den im Projekt dokumentierten Wissensort. Das kann zum Beispiel `Wissensdokumentation`, ein `docs/`-Bereich, eine interne Wissensdatenbank, ein Wiki, ein Obsidian-Vault oder eine andere projektbezogene Dokumentationsstruktur sein.

Leite Speicherort, Namensschema und erlaubte Inhalte immer aus den Projektregeln, der vorhandenen Dokumentation und der lokalen Struktur ab. Erfinde keine privaten Pfade und dokumentiere keine internen Serverdetails, wenn sie nicht ausdruecklich fuer Dokumentation vorgesehen sind.

Arbeitsweise:

- keine versteckten Obsidian-/App-Systemdaten bearbeiten;
- `.trash`, alte Build-Bundles, Caches und sensible Dateien ueberspringen;
- vorhandene Projektseiten lesen und den passenden Projektordner oder Wissensbereich ermitteln;
- Wissen aus App, Admin, API, Datenbank, Betrieb, Backups, Staging, Live, Tests, Deployments und offenen Punkten ergaenzen;
- neue `.md`-Dateien nur an passenden Stellen anlegen;
- `index.html`, `INDEX.md` oder vergleichbare Uebersichten nur aktualisieren, wenn das Projekt diese Struktur nutzt;
- keine Secrets, Zugangsdaten, personenbezogenen Daten oder privaten Serverdetails dokumentieren.

Typische Zielbereiche:

- projektspezifische Dokumentationsordner wie `docs/`, `DOKUMENTATION/` oder `AI/`;
- ein projektbezogener Bereich in einer Wissensdatenbank;
- ein Team-Wiki oder ein Obsidian-/Markdown-Vault;
- fachliche Wissensbereiche, wenn das Projekt dort bereits verlinkt ist oder die Projektregeln es vorsehen.

Wenn kein passender Zielordner existiert, lege nur dann einen neuen Projektordner an, wenn Projektname, Zweck und gewuenschter Dokumentationsort eindeutig sind. Andernfalls dokumentiere lokal im Projekt und nenne den offenen Wissensdokumentations-Punkt im Abschlussbericht.

### 9. Abschlussbericht

Berichte knapp:

- Projektname, aktueller Commit und Branch;
- GitHub-/Remote-Stand;
- Dev-/Staging-/Live-Version oder Grund, warum sie nicht pruefbar war;
- ausgefuehrte Tests, Browser-Smokes und getestete Funktionen;
- Backup-Pfad, Umfang und Hashpruefung;
- Deploy- oder Cleanup-Aktionen;
- aktualisierte Projekt- und Wissensdokumentations-Dateien;
- bekannte Restrisiken oder bewusst offene Punkte.

Wenn die jeweilige Agentenumgebung spezielle Abschlussmarker oder Git-Direktiven erwartet, nutze sie nur fuer tatsaechlich erfolgreiche Aktionen. In allen anderen Umgebungen reicht ein normaler, klarer Abschlussbericht.

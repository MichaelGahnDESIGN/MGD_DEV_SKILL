---
name: dev
description: Use when the user invokes /dev, /dev-changelog, or asks to synchronize a software project across local worktree, GitHub, main/dev branches, staging/live deployments, backups, cleanup, browser/Playwright smoke tests, changelog maintenance, and project knowledge documentation.
---

# Dev

## Ziel

Dieser Skill bringt ein Projekt in einen einheitlichen, geprüften Arbeitsstand: lokal, Git/GitHub, Hauptbranch, Entwicklungszweige, Dev/Staging, Live, Backups, Tests und Wissensdokumentation. Er ist für Abschluss-, Aufräum-, Release-, Deploy- und Weiterarbeitsstände in jedem Projekt gedacht.

Der Skill ist projektneutral. Projektname, Stack, Live-/Staging-Ziele, Backup-Pfade, Testbefehle und Dokumentationsorte werden immer aus dem aktuellen Repository, den Projektregeln und der vorhandenen Dokumentation abgeleitet.

## Sonderbefehl `/dev-changelog`

Wenn der Nutzer `/dev-changelog` aufruft oder ausdrücklich einen Changelog-Assistenten möchte, starte einen fokussierten Changelog-Workflow statt des vollständigen `/dev`-Ablaufs.

Ziel: Eine menschlich lesbare und später maschinell gut auswertbare Changelog-Datei führen, aus der später ein Updater, ein Menüpunkt „Änderungen“, ein Notificationcenter oder eine Release-Ansicht gespeist werden kann.

Arbeitsweise:

1. Projektregeln, vorhandene Dokumentation und vorhandene Changelog-Dateien lesen.
2. Bevorzugte Datei ableiten: zuerst vorhandene `CHANGELOG.md`, sonst dokumentierter Projektpfad, sonst `CHANGELOG.md` im Repository-Stamm vorschlagen oder anlegen.
3. Vorhandene Änderungen nur aus nachvollziehbaren Quellen ableiten: Git-Diff, Commits, Issues/PRs, Release-Notizen, Aufgabenbeschreibung und Projektdokumentation.
4. Neue Einträge unter `Unreleased` oder der vom Nutzer genannten Version sammeln.
5. Einträge klar, kurz und nutzerverständlich schreiben. Jede Änderung soll erklären, was sich für Nutzer, Betreiber oder Entwickler praktisch ändert.
6. Struktur stabil halten, damit sie später geparst werden kann.
7. Keine Secrets, Tokens, personenbezogenen Daten, internen Serverpfade, Kundendaten, Zahlungsdaten oder privaten Admin-Details in den Changelog schreiben.
8. Am Ende berichten, welche Datei geändert wurde, welche Quellen genutzt wurden und welche Punkte unsicher oder offen sind.

Empfohlenes Markdown-Format:

```markdown
# Changelog

## Unreleased

### Neu
- ...

### Geändert
- ...

### Behoben
- ...

### Sicherheit
- ...

### Technisch
- ...

### Dokumentation
- ...

## 1.2.3 - 2026-06-18

### Neu
- ...
```

Wenn ein Projekt bereits ein anderes Changelog-Format nutzt, dieses Format beibehalten und nur vorsichtig ergänzen.

## Harte Sicherheitsregeln

- Niemals Secrets, Tokens, Passwörter, `.env*`, private Serverpfade mit Zugangsdaten, echte E-Mail-Zugangsdaten, Zahlungsdaten oder personenbezogene Daten in Git, Logs, Screenshots, Wissensdokumentation oder Abschlussberichte schreiben.
- Niemals `git reset --hard`, `git clean -fd`, Backup-Löschung, Server-Löschung, Datenbankoperationen, Migrationen oder Live-Änderungen ohne vorheriges geprüftes Backup ausführen.
- Live gilt nur als Wahrheit, wenn GitHub, lokaler Commit, dokumentierte Version, API-/Frontend-/Admin-Builds und Smoke-Tests plausibel zusammenpassen. Bei Widerspruch zuerst Befund dokumentieren.
- Backups erst löschen, nachdem ein neues vollständiges Backup erstellt und per SHA-256 oder gleichwertigem Hashmanifest geprüft wurde. Danach nur ältere Backups entfernen, sodass mindestens die letzten 3 vollständigen Backups je Backup-Familie erhalten bleiben.
- `.trash`, generierte Build-Artefakte, App-Bundles, alte Archive und Cache-Verzeichnisse nur löschen, wenn sie eindeutig reproduzierbar sind und nicht mehr als Restore- oder Referenzstand gebraucht werden.
- Bei Zahlungs-, Auth-, Profil-, Upload-, Rechnungs-, Admin-, Logging- und personenbezogenen Daten besonders streng nach Datenminimierung, Zugriffsbeschränkung, Verschlüsselung/Hashing, sicherer Token-Ablage und DSGVO-Nähe arbeiten.

### Lokal-only — Playtests, Backups und sensible Daten verlassen NIE die lokale Maschine

Diese Regel ist nicht verhandelbar und hat Vorrang vor jedem Aufräum-, Release- oder Sync-Schritt:

- **Niemals nach GitHub und niemals nach Live** gelangen: Play-Test-Branches und -Artefakte (`PLAYTEST/`, `PlayTest/`, Protokolle, Screenshots), Backups (DB-Dumps, `*.sql`, `*.sql.gz`, `*.dump`, `BACKUPS/`/`BACKUP*`) sowie sensible Daten (`.env*` außer `.env.example`, Tokens, API-Keys, Passwörter, `*.pem`, `*.key`, `id_rsa*`, Dateien mit Zugangsdaten/`server_access`). Diese bleiben **ausschließlich lokal**.
- **Push-Disziplin:** Nur den vereinbarten Hauptbranch (i. d. R. `main`) pushen. **Niemals** `git push --all` oder `git push --mirror`. Branches, deren Name `playtest` enthält (z. B. `PlayTest*`), werden **nie** gepusht — sie sind reine Lokal-Branches.
- **Vor jedem Push prüfen:** zu pushende Branchnamen gegen das `playtest`-Muster und `git diff --cached --name-only` bzw. den Push-Bereich gegen die obigen Datei-/Pfadmuster. Bei einem Treffer **abbrechen** und den Befund melden, statt zu pushen.
- **Vor jedem Deploy prüfen:** Die Deploy-Quelle (rsync-Quelle, Build-Verzeichnis, Archiv) enthält keine Backups, keine `PLAYTEST/`-Inhalte und keine Secrets. Niemals Backups oder Test-Artefakte in den Webroot/Live-Stand spielen.
- Alle genannten Muster gehören in `.gitignore`; fehlt ein Eintrag, zuerst `.gitignore` ergänzen, dann weiterarbeiten.
- **Technische Absicherung:** Installiere im Projekt den mitgelieferten Pre-Push-Hook `dev/hooks/pre-push` (siehe dort), der Push-Versuche von Playtest-Branches, Backups und Secrets hart blockiert — Belt-and-Suspenders zusätzlich zu dieser Regel.

## Ablauf

### 1. Projektkontext und Regeln laden

Lies vor Änderungen die vorhandenen Regeln und Betriebsdokumente. Typische Kandidaten sind:

- `AGENTS.md`, `CLAUDE.md`, `GEMINI.md` oder vergleichbare Agentenregeln;
- `GRUNDREGELN.md`, Projektregeln, Architektur- und Sicherheitsdokumente;
- `README.md`, `docs/`, `AI/`, `PROJEKT/`, `DOKUMENTATION/` und vorhandene `SKILL.md`-Dateien;
- Betriebsdokumentation zu Backups, Deployment, Versionen, Staging, Live, Monitoring und Restore;
- Paket- und Stack-Hinweise wie `package.json`, `composer.json`, `pubspec.yaml`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `Dockerfile` und CI-Workflows.

Wenn erwartete Dokumente fehlen, dokumentiere das als offenen Punkt und leite vorsichtig aus der Repo-Struktur ab, statt projektspezifische Annahmen zu erfinden.

Prüfe danach:

- `git status --short --branch`;
- aktuelle Branches, Remotes, Tags und offene Worktrees;
- Projektname, Hauptbranch und aktive Arbeitsbranch;
- lokale Version aus App-/API-/Package-Dateien;
- dokumentierte oder erreichbare Dev-/Staging-/Live-Versionen, falls vorhanden.

### 2. Stände vergleichen

Vergleiche:

- lokaler `HEAD`, Hauptbranch, aktive Branch und Remote-Hauptbranch;
- GitHub-Remote mit `git fetch --all --prune --tags`;
- lokale offene Änderungen und untracked Dateien;
- dokumentierte Versionen, Tags, Changelog und Deploy-Metadaten;
- Dev-/Staging-/Live-Versionen über vorhandene APIs, HTML-Metadaten, Healthchecks, Admin-Anzeigen oder Deployment-Logs;
- lokale Builds gegen deployte Builds, wenn Artefakte oder Build-IDs vorhanden sind.

Wenn ein Stand abweicht, entscheide konservativ:

- lokale ungesicherte Arbeit sichern, committen oder branchieren;
- nur Fast-Forward-Merges nutzen, wenn möglich;
- Konflikte nicht blind lösen;
- Live nicht überschreiben, bevor Backup, Restore-Pfad und Tests geklärt sind;
- bewusst abweichende Stände dokumentieren.

### 3. Git, GitHub und Vereinheitlichung

Zielzustand:

- relevante Arbeit ist auf dem vorgesehenen Hauptbranch oder sauber in einer dokumentierten Feature-Branch;
- der Remote-Stand ist aktuell und nachvollziehbar;
- lokale Arbeitskopie ist sauber oder bewusst mit offenen Punkten dokumentiert;
- nicht mehr benötigte lokale Feature-Branches sind gelöscht oder als weiterhin relevant dokumentiert;
- Dev/Staging und Live laufen auf demselben freigegebenen Stand oder ihre bewusste Abweichung ist dokumentiert.

Nutze bevorzugt:

- `git merge --ff-only`, wenn möglich;
- normale Merge-Commits nur nach Prüfung;
- Pull Requests für nachvollziehbare Integration, wenn das Projekt so arbeitet;
- keine Rewrites auf geteilten Branches ohne ausdrückliche Freigabe.

### 4. Tests, Checks und Smokes

Führe passend zum Projekt aus, was die Dokumentation, CI oder der Stack nahelegt:

- JavaScript/TypeScript/Web: Lint, Typecheck, Unit-/Integrationstests, Build, Playwright/Cypress-Smokes.
- PHP/Symfony/Laravel/WordPress: `php -l`, PHPUnit, Framework-Checks, relevante Console-/WP-CLI-Kommandos.
- Flutter/Dart: `flutter analyze`, relevante Tests, Web-/App-Builds.
- Python: Lint/Format-Check, Typecheck, Pytest, Migrations-/Management-Checks.
- Datenbank: Migrationen nur nach Backup prüfen; Schema- und Seed-Kommandos dokumentieren.
- Browser: Playwright oder Browser-Plugin für Login, zentrale Module, Admin-Bereiche und Live-Smokes.
- Betrieb: vorhandene Healthcheck-, Stability-, Deploy- oder Monitoring-Skripte nutzen.

Wenn ein erwartetes Tool nicht verfügbar ist, dokumentiere den Grund und nutze den besten sicheren Ersatz, zum Beispiel Browser-, Curl- oder API-Smokes.

### 5. Browser- und Playwright-Smokes

Nutze Playwright, ein Browser-Plugin oder ein vergleichbares Browser-Automationswerkzeug, wenn das Projekt eine Weboberfläche, ein Admin-Panel, eine Dokumentationsseite, eine GitHub-Seite, eine Login-Strecke, einen Checkout, Uploads oder andere nutzernahe Browserpfade hat.

Arbeitsweise:

- prüfe zuerst, ob es bereits projektinterne Playwright-, Cypress- oder E2E-Tests gibt, und bevorzuge diese gegenüber neu erfundenen Klickpfaden;
- starte lokale Apps nur über dokumentierte Befehle und notiere URL, Branch, Commit und Umgebung;
- teste Dev/Staging vor Live, wenn beide erreichbar sind;
- lade Seiten nach Builds oder Deployments bewusst neu und prüfe eine konkrete sichtbare Erfolgsaussage, nicht nur den HTTP-Status;
- erfasse Browser-Konsole, Netzwerkfehler oder sichtbare Fehlermeldungen nur soweit sie für die Diagnose gebraucht werden;
- erstelle Screenshots nur, wenn sie für Nachvollziehbarkeit, Vergleich oder Fehlerdiagnose nützlich sind;
- speichere oder veröffentliche keine Screenshots mit personenbezogenen Daten, Tokens, E-Mail-Adressen, Zahlungsdaten, Sessiondaten, Kundendaten oder internen Admin-Details;
- gib niemals Passwörter, Einmalcodes, API-Keys, Zahlungsdaten oder andere Secrets in Browserseiten ein, außer die Aufgabe, Umgebung und Freigabe sind eindeutig dokumentiert;
- verwende für Logins nach Möglichkeit Testkonten, Seed-Daten oder bereits dokumentierte sichere Testabläufe;
- bestätige keine produktiven Zahlungen, Löschungen, E-Mail-Versandaktionen, Rechteänderungen oder externen Nebenwirkungen ohne ausdrückliche Freigabe.

Typische Smoke-Pfade:

- Startseite oder zentrale App-Shell lädt ohne sichtbaren Fehler;
- Login- oder Auth-Status wird korrekt angezeigt, soweit sicher testbar;
- Hauptnavigation, Dashboard, Listenansicht oder Kernmodul ist erreichbar;
- Formularvalidierung zeigt erwartete Hinweise ohne echte Daten zu senden;
- Admin- oder Profilbereiche geben keine sensiblen Informationen unnötig preis;
- Checkout- oder Zahlungsstrecken werden nur im Test-/Sandbox-Modus geprüft;
- GitHub-, Dokumentations- oder Release-Seiten zeigen aktuellen Commit, README, Changelog oder Artefakte.

Berichte Browser-Ergebnisse knapp mit:

- getesteter URL und Umgebung;
- Tool oder vorhandener Testbefehl;
- geprüften Nutzerpfaden;
- Ergebnis je Pfad;
- relevanten Konsolen-/Netzwerkfehlern ohne Secrets;
- Screenshot-Pfad oder bewusster Verzicht auf Screenshots;
- offenen Risiken, zum Beispiel fehlender Login, privates Repository, nicht erreichbares Staging oder fehlende Testdaten.

### 6. Deploy auf Dev/Staging und Live

Vor jedem Deploy:

- vollständiges Backup erstellen;
- Datenbankdump einschließen, wenn eine Datenbank betroffen ist;
- Uploads/Medien/Speicherorte einschließen, wenn sie für Restore gebraucht werden;
- Hashmanifest erzeugen und prüfen;
- Restore-Pfad und Backup-Ort im Bericht nennen;
- Secrets nicht anzeigen oder speichern.

Deploy-Reihenfolge:

1. Dev/Staging aktualisieren und smoke-testen.
2. Live erst aktualisieren, wenn Backup, Tests und Rückfallstrategie klar sind.
3. Migrationen/Schema-Kommandos nur nach Backup und mit dokumentierter Reihenfolge ausführen.
4. Live-Versionen, Healthchecks und zentrale Nutzerpfade prüfen.
5. Browser-Smoke mit Playwright, Browser-Plugin oder dokumentiertem Ersatz durchführen.

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
- bekannte Archiv- oder Restore-Stände.

Lösche nur:

- eindeutig generierte, reproduzierbare Artefakte;
- alte Backups oberhalb der letzten 3 vollständigen, geprüften Backups je Backup-Familie;
- zusammengeführte lokale Branches/Worktrees, die keine einzigartige Arbeit enthalten;
- Cache-/Temp-Dateien, die keine Projekt- oder Restore-Information enthalten.

Nicht löschen:

- letzte 3 vollständige Backups je Backup-Familie;
- Backups, die in Versionen, Deployment-Dokumentation oder Abschlussberichten als Restore-Punkt referenziert sind;
- ungeprüfte Datenbankdumps;
- unbekannte Dateien mit möglichen Secrets;
- Nutzeruploads, Medien, Rechnungsdaten, Logs mit rechtlicher Relevanz oder Auditdaten ohne klare Freigabe.

### 8. Projektwissen aktualisieren

Aktualisiere, wenn vorhanden und erreichbar, den im Projekt dokumentierten Wissensort. Das kann zum Beispiel ein `docs/`-Bereich, eine interne Wissensdatenbank, ein Wiki, ein Obsidian-Vault oder eine andere projektbezogene Dokumentationsstruktur sein.

Leite Speicherort, Namensschema und erlaubte Inhalte immer aus den Projektregeln, der vorhandenen Dokumentation und der lokalen Struktur ab. Erfinde keine privaten Pfade und dokumentiere keine internen Serverdetails, wenn sie nicht ausdrücklich für Dokumentation vorgesehen sind.

Arbeitsweise:

- keine versteckten Obsidian-/App-Systemdaten bearbeiten;
- `.trash`, alte Build-Bundles, Caches und sensible Dateien überspringen;
- vorhandene Projektseiten lesen und den passenden Projektordner oder Wissensbereich ermitteln;
- Wissen aus App, Admin, API, Datenbank, Betrieb, Backups, Staging, Live, Tests, Deployments und offenen Punkten ergänzen;
- neue `.md`-Dateien nur an passenden Stellen anlegen;
- `index.html`, `INDEX.md` oder vergleichbare Übersichten nur aktualisieren, wenn das Projekt diese Struktur nutzt;
- keine Secrets, Zugangsdaten, personenbezogenen Daten oder privaten Serverdetails dokumentieren.

Typische Zielbereiche:

- projektspezifische Dokumentationsordner wie `docs/`, `DOKUMENTATION/` oder `AI/`;
- ein projektbezogener Bereich in einer Wissensdatenbank;
- ein Team-Wiki oder ein Obsidian-/Markdown-Vault;
- fachliche Wissensbereiche, wenn das Projekt dort bereits verlinkt ist oder die Projektregeln es vorsehen.

Wenn kein passender Zielordner existiert, lege nur dann einen neuen Projektordner an, wenn Projektname, Zweck und gewünschter Dokumentationsort eindeutig sind. Andernfalls dokumentiere lokal im Projekt und nenne den offenen Wissensdokumentations-Punkt im Abschlussbericht.

### 9. Abschlussbericht

Berichte knapp:

- Projektname, aktueller Commit und Branch;
- GitHub-/Remote-Stand;
- Dev-/Staging-/Live-Version oder Grund, warum sie nicht prüfbar war;
- ausgeführte Tests, Browser-Smokes und getestete Funktionen;
- Backup-Pfad, Umfang und Hashprüfung;
- Deploy- oder Cleanup-Aktionen;
- aktualisierte Projekt- und Wissensdokumentations-Dateien;
- bekannte Restrisiken oder bewusst offene Punkte.

Wenn die jeweilige Agentenumgebung spezielle Abschlussmarker oder Git-Direktiven erwartet, nutze sie nur für tatsächlich erfolgreiche Aktionen. In allen anderen Umgebungen reicht ein normaler, klarer Abschlussbericht.

# /dev

Starte den DEV-Skill für dieses Projekt.

## Verhalten

Nutze `dev/SKILL.md` als Arbeitsgrundlage und führe den Ablauf in dieser Reihenfolge durch:

1. Projektkontext und Regeln laden (`AGENTS.md`, `CLAUDE.md`, `README.md`, `docs/` usw.)
2. Lokale, GitHub- und veröffentlichte Stände vergleichen (`git status`, `git fetch`)
3. Git, Branches und Remotes einordnen
4. Tests, Builds und allgemeine Checks ausführen
5. Browser- und Playwright-Smokes sicher prüfen
6. Deploy auf Dev/Staging und Live nur mit Backup und Rückfallplan
7. Cleanup und Backup-Retention vorsichtig behandeln
8. Projektwissen und Dokumentation aktualisieren
9. Abschlussbericht schreiben

## Sicherheitsregeln

- Keine Secrets, Tokens oder Passwörter in Git, Logs oder Berichte schreiben.
- Keine `git reset --hard`, Backup-Löschung oder Live-Änderungen ohne vorheriges geprüftes Backup.
- Live nicht überschreiben, bevor Backup, Tests und Rückfallstrategie klar sind.
- Keine produktiven Zahlungen, Löschungen oder E-Mail-Versandaktionen ohne ausdrückliche Freigabe.

## Ergebnis

Am Ende kurz berichten:

- Projektname, aktueller Commit und Branch
- GitHub-/Remote-Stand
- ausgeführte Tests und Browser-Smokes
- Backup-Pfad und Hashprüfung
- Deploy- oder Cleanup-Aktionen
- bekannte Restrisiken oder bewusst offene Punkte

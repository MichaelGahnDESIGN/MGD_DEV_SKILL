# Changelog

Alle wichtigen Änderungen an diesem Repository werden hier dokumentiert.

## 1.2.0 - 2026-09-19

### Neu

- `/dev-fast` als tokensparenden Sonderbefehl ergänzt: zerlegt anstehende Arbeit in kleinste, unabhängig deploybare Teilschritte und geht nach minimaler Prüfung sofort live — statt am Ende eines knappen Kontextfensters oder Nutzungslimits eine große, unfertige Änderung zu riskieren.
- `/dev` und `/dev-fast` weisen jetzt kurz auf [MGD_Todo_SKILL](https://github.com/MichaelGahnDESIGN/MGD_Todo_SKILL) hin, falls `/todo` im Projekt nicht installiert ist (unverbindlicher Hinweis, keine Abhängigkeit).
- Slash-Command-Vorlagen `dev-fast.md` für Claude Code und Codex hinzugefügt.

### Dokumentation

- README um `/dev-fast` in Befehlsübersicht, Struktur und Nutzungsbeispielen ergänzt.

## 1.1.1 - 2026-06-23

### Neu

- Standard-GitHub-Dokumentation ergänzt: `.github/CONTRIBUTING.md`, `.github/SECURITY.md`, `.github/CODE_OF_CONDUCT.md`, Issue-Vorlage für Security-Reports.

## 1.1.0 - 2026-06-18

### Neu

- `/dev-changelog` als fokussierten Changelog-Assistenten ergänzt.
- Slash-Command-Vorlagen für Codex und Claude Code hinzugefügt.
- README und Wiki um Changelog-Beispiele und Nutzungshinweise erweitert.

### Sicherheit

- Changelog-Regeln schließen Secrets, personenbezogene Daten, Kundendaten, Zahlungsdaten und interne Serverdetails ausdrücklich aus.

## 1.0.1 - 2026-06-14

### Geändert

- Lokal-only-Regel für Playtests, Backups und sensible Daten ergänzt.

## 1.0.0 - 2026-06-14

### Neu

- Erste veröffentlichte Version des DEV-Skills mit Slash-Command-Vorlagen.

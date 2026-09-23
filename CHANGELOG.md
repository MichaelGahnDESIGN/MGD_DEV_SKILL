# Changelog

Alle wichtigen Änderungen an diesem Repository werden hier dokumentiert.

## 1.3.0 - 2026-09-23

### Neu

- Companion-Skill-Check ergänzt: Beim allerersten `/dev`-, `/dev-fast`- oder `/dev-changelog`-Lauf in einem Projekt prüft der Skill aktiv, ob Fragenkatalog-Skill, MGD_Todo_SKILL und MGD_Living-Documentation im Projekt oder global installiert sind, fragt bei fehlenden Begleit-Skills nach und installiert sie auf Zustimmung. Eine Marker-Datei (`.dev-skill/companion-check.md`) sorgt dafür, dass der Check nicht bei jedem weiteren Lauf erneut auftaucht.
- README um Abschnitt „Empfohlene Begleit-Skills" ergänzt, der das Zusammenspiel der vier Skills (DEV_SKILL, Fragenkatalog-Skill, MGD_Todo_SKILL, MGD_Living-Documentation) kurz erklärt.

### Dokumentation

- Die beiden bisher redundanten Abschnitte „Verwandte Projekte Von Michael Gahn DESIGN" und „Verwandte MGD Projekte" in der README zu einer vollständigen, deduplizierten Tabelle zusammengeführt und um Fragenkatalog-Skill sowie MGD_Living-Documentation ergänzt, jeweils mit einem Satz zum Zusammenspiel mit DEV_SKILL.
- `dev/SKILL.md`, Abschnitt „Zusammenspiel mit anderen Skills", um Zeilen für Fragenkatalog-Skill und MGD_Living-Documentation ergänzt.

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

# /dev-changelog

Starte den DEV-Changelog-Assistenten für dieses Projekt.

## Verhalten

Nutze `dev/SKILL.md` als Arbeitsgrundlage und führe den fokussierten `/dev-changelog`-Workflow durch:

1. Projektregeln und vorhandene Changelog-/Release-Dokumentation lesen.
2. Vorhandene `CHANGELOG.md` oder den dokumentierten Changelog-Pfad finden.
3. Falls keine Changelog-Datei existiert, `CHANGELOG.md` im Repository-Stamm vorschlagen oder anlegen.
4. Änderungen aus nachvollziehbaren Quellen ableiten: Git-Diff, Commits, Issues/PRs, Release-Notizen, Aufgabenbeschreibung und Projektdokumentation.
5. Einträge unter `Unreleased` oder der genannten Version ergänzen.
6. Eine stabile Struktur verwenden, die später für Updater, Menüpunkt „Änderungen“, Notificationcenter oder Release-Ansichten geparst werden kann.
7. Abschlussbericht schreiben.

## Sicherheitsregeln

- Keine Secrets, Tokens, Passwörter, internen Serverpfade, personenbezogenen Daten, Kundendaten, Zahlungsdaten oder privaten Admin-Details in den Changelog schreiben.
- Unsichere oder nicht belegte Änderungen nicht erfinden, sondern als offene Frage melden.
- Bestehendes Changelog-Format beibehalten, wenn das Projekt bereits eines nutzt.

## Ergebnis

Am Ende kurz berichten:

- geänderte Changelog-Datei;
- verwendete Quellen;
- neue oder aktualisierte Version/Section;
- unsichere oder offene Punkte.

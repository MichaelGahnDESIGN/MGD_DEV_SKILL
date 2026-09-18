# /dev-fast

Starte den DEV-Fast-Assistenten für dieses Projekt: schnelle, tokensparende
Entwicklung mit häufigem Zwischen-Deploy statt eines vollständigen `/dev`-Laufs.

Gedacht für die Situation, dass nur noch wenig Kontextfenster oder wenig
Nutzungslimit übrig ist und trotzdem etwas Fertiges live gehen soll, bevor die
Session oder das Limit endet.

## Verhalten

Nutze `dev/SKILL.md` als Arbeitsgrundlage und führe den fokussierten
`/dev-fast`-Workflow durch:

1. Die anstehende Arbeit in die kleinste sinnvolle, für sich alleine deploybare
   Einheit zerlegen — nicht die ganze Funktion, sondern der erste Teilschritt,
   der allein funktioniert und live gehen kann.
2. Nur gezielt lesen, was für genau diesen Teilschritt und seinen Deploy-Weg
   nötig ist. Keine zusätzliche Erkundung, keine Doppelarbeit.
3. Minimal prüfen: das Nötigste, um keinen kaputten Stand zu deployen — kein
   vollständiges Test-/Lint-Programm wie bei `/dev`.
4. Committen und nach Projekt-Konvention deployen — sofort, nicht erst am Ende
   der gesamten Aufgabe.
5. Falls im Projekt bereits `/todo` installiert ist, die Zerlegung optional dort
   als Todos anlegen bzw. erledigte Teilschritte abhaken. Ist `/todo` nicht
   installiert, kurz auf [MGD_Todo_SKILL](https://github.com/MichaelGahnDESIGN/MGD_Todo_SKILL)
   hinweisen, ohne die Aufgabe davon abhängig zu machen.
6. Nach jedem Teilschritt kurz berichten und, solange Aufgabe und Budget es
   hergeben, direkt mit dem nächsten Teilschritt weitermachen.

## Unterschied zu `/dev`

`/dev-fast` ist schneller und günstiger, aber bewusst weniger gründlich als
`/dev`. Es ersetzt `/dev` nicht — bei ausreichend Kontext/Budget bleibt `/dev`
die richtige Wahl für einen sauberen, vollständig geprüften Release.

## Sicherheitsregeln

Dieselben wie bei `/dev` — unverändert und ohne Ausnahme:

- **Lokal-only (Vorrang):** Play-Test-Branches/-Artefakte (`PLAYTEST/`, `PlayTest*`), Backups (`*.sql`, `*.sql.gz`, `BACKUPS/`) und sensible Daten (`.env*` außer `.env.example`, Tokens, Keys, Zugangsdaten) NIE zu GitHub pushen und NIE deployen. Nur `main` pushen, niemals `git push --all`. Vor Push/Deploy gegen diese Muster prüfen; siehe `dev/SKILL.md` und den Pre-Push-Hook `dev/hooks/pre-push`.
- Keine Secrets, Tokens oder Passwörter in Git, Logs oder Berichte schreiben.
- Keine `git reset --hard`, Backup-Löschung oder Live-Änderungen ohne vorheriges geprüftes Backup.
- Keine produktiven Zahlungen, Löschungen oder E-Mail-Versandaktionen ohne ausdrückliche Freigabe.

## Ergebnis

Nach jedem Teilschritt kurz berichten:

- Teilschritt und Begründung für die Wahl als kleinste Einheit;
- was geprüft wurde (bewusst reduziert);
- Commit und Deploy-Ziel;
- nächster geplanter Teilschritt, falls die Aufgabe noch offen ist.

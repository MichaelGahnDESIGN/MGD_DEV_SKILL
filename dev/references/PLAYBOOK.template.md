# Playbook · <Auftrag>

> In die vorhandene Projektdokumentation übernehmen und Platzhalter ersetzen.
> Bei kurzem Auftrag genügt je Abschnitt eine Zeile. Vor dem ersten Eingriff planen;
> anschließend dieses Dokument fortschreiben, nicht für jeden Aufruf neu beginnen.

## Ziel und Grenzen

- Ergebnis: <konkreter Nutzen und messbarer Gesamtabschluss>
- Umfang / Freigaben: <was beauftragt ist; keine Freigabe aus dieser Vorlage ableiten>
- Geschützt: <was unverändert bleibt>
- Vorhandene Todo-/Doku-Verweise: <IDs und Pfade, keine zweite Aufgabenliste>

## Grundlinie

- Datum, Repository, Branch und Ausgangscommit: <belegter Stand>
- Betroffene Funktion / Tests: <Befehl, Ergebnis und bekannte Altfehler>
- Lokal / GitHub / Release / Live: <je eigener Stand oder ausdrücklich unbekannt>
- Rückfallpunkt: <Git-Referenz oder freigegebener Sicherungsnachweis; keine Secrets>

## Ausführung in Reihenfolge

| ID | Schritt und betroffene Dateien | Voraussetzung | Erfolgskriterium und Prüfung | Rückfall | Status | Beleg |
| --- | --- | --- | --- | --- | --- | --- |
| P1 | <kleine nutzbare Einheit> | <keine oder IDs> | <vorab festgelegter sichtbarer Erfolg und gezielter Test> | <Rückweg> | geplant | — |
| P2 | <nächste Einheit> | P1 geprüft | <eigenes Kriterium> | <Rückweg> | geplant | — |

Status: `geplant` → `in Arbeit` → `geprüft`. Bei Fehlern `blockiert` mit Grund,
bei bewusstem Wegfall `entfallen` mit Begründung. Unbekannt ist nicht geprüft.
Ein Eintrag wird erst nach Prüfung gegen sein ursprüngliches Kriterium und die
Grundlinie abgeschlossen. Unabhängige Schritte nur nach erlaubter Delegation
parallel bearbeiten; denselben Dateibereich nicht gleichzeitig verändern.

## Planänderungen

| Datum | Betroffene IDs | Neuer Weg und Grund | Auswirkung auf Kriterien, Reihenfolge und Freigaben |
| --- | --- | --- | --- |
| — | — | Noch keine | — |

Planänderungen vor der Umsetzung festhalten. Ein fehlender Beleg oder eine rote
Prüfung ist kein Grund, das Kriterium nachträglich abzuschwächen.

## Fortsetzung und Abschluss

- Aktueller Schritt / nächster ausführbarer Schritt: <ID und Voraussetzung>
- Abgleich: <Git-Diff und Zielstand passen noch zur Grundlinie? Was hat sich geändert?>
- Lokal geprüft: <konkreter Beleg oder offen>
- GitHub / Release / Live: <je konkreter Beleg oder offen; nicht gleichsetzen>
- Restpunkte / Blockaden: <ID, Ursache und nötige Entscheidung; keine Scheinerledigung>
- Gesamtergebnis: <erreicht, wenn alle Kriterien passend belegt sind; sonst offen>

Nur bereinigte Nachweise hier verlinken. Keine Zugangsdaten, personenbezogenen
Protokolle, privaten Serverdetails, Sicherungen oder Playtest-Artefakte veröffentlichen.

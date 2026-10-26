# Playbook · Verbindlicher Ablauf für Dev und Fast-dev

Stand: 26.10.2026 · Grundlinie: `2f7a0f1` auf `main`.

## Ziel und Grenzen

Jeder Aufruf plant vor der Umsetzung ein dauerhaftes Playbook und gleicht die
Arbeit Schritt für Schritt damit ab. `/dev`, `/fast-dev` und `/dev-fast` nutzen
denselben Vertrag. Die schnelle Variante hält den Umfang klein, nicht die
Sicherheitsgrenzen. Kein Eingriff in MythRush, Live-Dienste oder fremde Dateien.

Vorhanden: zwei portable Skills, Command-Vorlagen, README, Changelog und öffentliches
Wiki. Kein Installer, keine Paketbau-Automation, kein vorhandener CI-Testlauf.
Die installierten Kopien entsprechen noch dem älteren Stand `cf17a09`.
Die unbekannte unversionierte Datei `SKILL.md` im Quellrepo bleibt erhalten.

## Reihenfolge und Nachweise

| ID | Schritt / Dateien | Voraussetzung | Erfolg und Beleg | Status |
| --- | --- | --- | --- | --- |
| P1 | Iststand und Regeln lesen | keine | Remote, lokale Kopien und fremde Änderungen eingeordnet | geprüft |
| P2 | Vertrag und portable Vorlage in `dev/` und `fast-dev/` ergänzen; Commands, README, Changelog nachziehen | P1 | Vorlage ist aus beiden installierbaren Skills erreichbar; Alias widerspruchsfrei | geprüft |
| P3 | Diff, interne Links und Paketumfang prüfen | P2 | 11 relative Links gültig; 18 Produktdateien, CRC-/Entpackprüfung und identische Vorlagen im ZIP | geprüft |
| P4 | Nur passende lokale Installationen synchronisieren | P3 | 11 Dateien hashgleich synchronisiert; unbekannte Root-Skilldatei unverändert | geprüft |
| P5 | Geprüfte Quellen auf GitHub integrieren und vorhandenes Wiki ergänzen | P3 | Quellcommit `9d27b1f`, Wiki `bf417a1`; Inhalte aus GitHub zurückgelesen | geprüft |
| P6 | Ergebnisse und Grenzen festhalten | P4, P5 | Prüf- und Veröffentlichungsnachweise unten; Release-/Live-Grenzen benannt | geprüft |

## Rückfall und Abschluss

Quellenrückfall ist der Git-Ausgangsstand. Installierte Kopien nur ersetzen, wenn
sie noch den zuvor geprüften Hash tragen; andernfalls den Konflikt melden. Keine
Produktivdaten betroffen, daher keine neue Datenbanksicherung. Ein neues getaggtes
Release ist in diesem begrenzten Skill-Update nicht beauftragt; ein lokaler
Pakettest ist kein veröffentlichter Release.

Bei fehlendem GitHub-Zugriff oder fremden Änderungen nur den betroffenen Schritt
blockieren und unabhängige Arbeit fortsetzen. Keine stillen Reihenfolgewechsel.

## Prüfung der Vertragsfälle

Manuelle Inhaltsprüfung der Anweisungen, keine Messung eines autonomen Agentenlaufs:

- Neuer Kurzauftrag: Ziel, Grundlinie und Schrittfolge müssen vor dem ersten Eingriff stehen.
- Fortsetzung nach Kontextwechsel: Playbook, Git und Zielzustand werden erneut verglichen; keine blinde Wiederholung bereits belegter Schritte.
- Roter Teilschritt: abhängige Schritte bleiben blockiert; ein neuer Weg wird vor der Ausführung begründet, Kriterien werden nicht passend abgeschwächt.

Paketprüfung: 18 positiv ausgewählte Dateien, CRC und getrennte Ordnerinstallation
bestanden. SHA256 des temporären Prüfpakets:
`3065c1cfabbb2fcb428c1a4681a8b20dd59ccc1aa507afbdea8cfbc717278e4e`.
Das Prüfpaket wurde nicht als Release veröffentlicht. Keine CI vorhanden, kein
Live-System geändert; Markdown- und Paketprüfung sind keine Browser-/Engine-Abnahme.

## Veröffentlichung und Abgleich

- Quelle auf `main`: `9d27b1f` mit Playbook-Vertrag, Vorlagen, Commands, README und Changelog. Dev-/Fast-dev-Inhalte und beide Vorlagen aus GitHubs Contents-API zurückgelesen und bytegleich verglichen.
- Öffentliches Wiki: `bf417a1` auf `master`, neue Seite `Workflow-Playbook`, vorhandene Fast-dev-Seiten und Navigation abgestimmt. Remote-Fassung der neuen Seite bytegleich zurückgelesen.
- Lokal: elf Skill-/Command-Dateien nach Prüfung gegen bekannte Ausgangsfassungen synchronisiert und Hashgleichheit belegt. Unbekannte unversionierte Root-`SKILL.md` unverändert erhalten; sie ist nicht Teil dieses Pakets.
- Kein neues getaggtes Release und kein Website-/Spieldeployment aus diesem Teilauftrag. Das Quellupdate steht unter `Unreleased`; das bisherige Downloadrelease bleibt unverändert.

Gesamtergebnis dieses Teilauftrags: erreicht. Die Playbook-Regeln sind Anweisungen
für Agenten; sie erzwingen ohne zusätzliche, nicht beauftragte Laufzeit-Hooks
keine Ausführungsreihenfolge auf Betriebssystemebene.

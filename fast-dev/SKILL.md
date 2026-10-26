---
name: fast-dev
description: >-
  Setzt freigegebene Entwicklungsaufgaben zügig in kleine nutzbare Live-Schritte um.
  Für /fast-dev und ausdrücklich gewünschte schnelle Umsetzung mit kurzen Playbooks
  und gezielten Prüfungen. Überspringt keine Sicherheits- oder Zugriffsschranken.
---

# /fast-dev

Ziel: ein sichtbares, funktionierendes Ergebnis in kleinen, gezielt geprüften Schritten.
Die geltenden Projektregeln und der tatsächliche Auftrag bestimmen den Umfang.

## Verbindliches Playbook

Bei **jedem Aufruf vor der ersten Umsetzung** ein vorhandenes Playbook lesen und
fortschreiben oder aus [der Vorlage](references/PLAYBOOK.template.md) anlegen.
Zielort aus dem Projekt ableiten; ohne Vorgabe
`docs/playbooks/<Datum>-<Auftrag>.md` nutzen und den Pfad kurz nennen. Bei einem
ausdrücklich rein lesenden Auftrag das Playbook im Bericht führen, ohne Dateischreibzugriff.

Das Playbook enthält Ziel und Grenzen, Commit und Grundlinie sowie geordnete
Schritte mit stabilen IDs, Voraussetzungen, betroffenen Dateien, Erfolgskriterium,
Prüfung, Beleg, Status und Rückfallweg. Vor jedem Schritt abgleichen, nach ihm den
Beleg eintragen. Status: `geplant`, `in Arbeit`, `geprüft`, `blockiert`, `entfallen`.
Nur mit bestandener Prüfung als `geprüft` markieren; entfallene Schritte begründen.
Abhängige Schritte bei Fehlern sperren, nur die betroffene Ursache korrigieren.
Planänderungen vor ihrer Ausführung mit Datum, Grund und Auswirkung eintragen;
Kriterien nicht nachträglich abschwächen. Bei Fortsetzung zuerst Playbook, Git-
und Zielstand vergleichen. Bestehende Todo-IDs verlinken, keine zweite Aufgabenliste.
Vor Abschluss alle Einträge abgleichen; lokal, GitHub, Release und Live getrennt
belegen. Keine zusätzliche Freigabe und keine Secrets durch das Playbook.

## Ablauf

1. Lies Regeln, Git-Status, betroffene Fach-Doku und den vorhandenen Deployment-Weg.
   Nutze den Projektgraph gezielt, falls vorgeschrieben. Nicht das ganze Projekt prüfen.
2. Plane beziehungsweise aktualisiere das Playbook oben. Wähle den nächsten
   ausführbaren kleinen Schritt mit erfüllten Voraussetzungen; vorhandene Todos
   nur verlinken.
3. Nutze vorhandene Komponenten, native Plattformfunktionen und lokale Assets.
   Löse Routineentscheidungen selbst. Unabhängige Aufgaben nur delegieren, wenn
   der Nutzer oder geltende Regeln dies erlauben.
4. Prüfe pro Schritt Syntax und genau die geänderte Hauptfunktion. Bei UI eine
   echte Sichtprüfung in den benötigten breiten und schmalen Ansichten; bei
   Berechtigungen und Datenspeicherung gezielt die betroffene Schutzgrenze.
   Keine vollständigen Testläufe oder wiederholten Smokes ohne konkreten Anlass.
5. Sichere einen nachvollziehbaren Rückfallpunkt. Deploye nur positiv ausgewählte
   Produktdateien, keine Projektwurzel, Secrets, privaten Sicherungen oder Testdaten.
   Bestehende Freigaben und Sicherheitsmodi bleiben verbindlich.
6. Sobald ein Schritt geprüft und nutzbar ist: nachvollziehbar committen und nach
   autorisiertem Projektverfahren veröffentlichen. Mit dem nächsten Schritt direkt
   weitermachen, bis der Auftrag erledigt ist. Ein Teilergebnis beendet den Auftrag nicht.
7. Umfasst der Auftrag einen Release, Version und Changelog abstimmen, den
   geprüften Commit taggen und den GitHub-Release samt vorgesehenem Paket wirklich
   veröffentlichen. Tag, Commit und heruntergeladenes Paket prüfen. Falls `/dev`
   installiert ist, dessen Release-Ablauf verwenden; ein Commit allein ist kein Release.
8. Playbook vollständig abgleichen; Doku, Todo, Version und ggf. lokalen Graph
   synchronisieren. Kurz berichten:
   sichtbar geändert, gezielt geprüft, Commit/Deployment, Rückfallpunkt, echte Restpunkte.

Bei einem Fehler nur die betroffene Ursache bearbeiten und die passende Prüfung
wiederholen. Keine Umgehung von Login, PIN, Wartung, Verschlüsselung oder fehlender
Freigabe. „Nicht geprüft“ bleibt ausdrücklich nicht geprüft. Dieser Skill erteilt
keine pauschale Freigabe für Zahlungen, Löschungen oder Änderungen fremder Systeme.

Alias im Dev-Workflow: `/dev-fast`; kanonischer Aufruf dieses Skills: `/fast-dev`.

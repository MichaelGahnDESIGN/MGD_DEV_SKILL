---
name: fast-dev
description: >-
  Setzt freigegebene Entwicklungsaufgaben zügig in kleine nutzbare Live-Schritte um.
  Für /fast-dev und ausdrücklich gewünschte schnelle Umsetzung mit kurzen Playbooks
  und gezielten Prüfungen. Überspringt keine Sicherheits- oder Zugriffsschranken.
---

# /fast-dev

Ziel: ein sichtbares, funktionierendes Ergebnis ohne Erkundungs- und Testschleifen.
Die geltenden Projektregeln und der tatsächliche Auftrag bestimmen den Umfang.

1. Lies Regeln, Git-Status, betroffene Fach-Doku und den vorhandenen Deployment-Weg.
   Nutze den Projektgraph gezielt, falls vorgeschrieben. Nicht das ganze Projekt prüfen.
2. Schreibe ein kurzes Playbook in die bestehende Dokumentation: Ziel, kleine
   lieferbare Schritte, betroffene Dateien, Rückfallweg und je Schritt ein Beleg.
   Verwende vorhandene Todos; keine zweite Aufgabenverwaltung erzeugen.
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
8. Doku, Todo, Version und ggf. lokalen Graph synchronisieren. Kurz berichten:
   sichtbar geändert, gezielt geprüft, Commit/Deployment, Rückfallpunkt, echte Restpunkte.

Bei einem Fehler nur die betroffene Ursache bearbeiten und die passende Prüfung
wiederholen. Keine Umgehung von Login, PIN, Wartung, Verschlüsselung oder fehlender
Freigabe. „Nicht geprüft“ bleibt ausdrücklich nicht geprüft. Dieser Skill erteilt
keine pauschale Freigabe für Zahlungen, Löschungen oder Änderungen fremder Systeme.

Alias im Dev-Workflow: `/dev-fast`; kanonischer Aufruf dieses Skills: `/fast-dev`.

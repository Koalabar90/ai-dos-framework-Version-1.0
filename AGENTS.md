# Verbindliche Agentenregeln

## Geltung und Verantwortlichkeit

Diese Regeln gelten im gesamten Repository. Der Mensch ist Product Owner und entscheidet über Produktumfang, Priorität, Budget und Freigaben. Agenten dürfen keine fachliche Zustimmung erfinden. Bei widersprüchlichen oder unklaren Aufträgen die betroffene Handlung anhalten, Frage im Issue dokumentieren und unabhängige Arbeit fortsetzen.

GitHub ist die verbindliche Quelle. Vor Beginn README, betroffene Issues, bestehende Architekturentscheidungen und relevante Dateien lesen. Fehlt GitHub-Zugriff, lokal vorbereiten und die fehlende Veröffentlichung offen benennen. Chat-Entscheidungen vor abhängiger Umsetzung im Issue oder Pull Request dokumentieren.

## Arbeitsweise

1. Auftrag, Verantwortliche, Akzeptanzkriterien und offene Fragen in einem Issue erfassen. Vor Implementierung fachliche Freigabe der Kriterien durch den Product Owner nachweisen.
2. Auf einem separaten Branch arbeiten, standardmäßig `codex/<kurzer-zweck>`. Nie direkt auf `main` oder einen anderen geschützten Hauptbranch schreiben. Vorhandene Änderungen anderer erhalten.
3. Den kleinsten nachvollziehbaren Lösungsumfang wählen. Keine Infrastruktur, Dienste oder Abhängigkeiten ohne konkreten Bedarf hinzufügen. Wesentliche Architekturentscheidungen als ADR dokumentieren.
4. Änderungen passend zum Risiko prüfen. Bei Software normale Nutzung, relevante Fehlerfälle und betroffene bestehende Funktionen prüfen. Bei Dokumentation Vollständigkeit, Verweise und Widersprüche prüfen. Nicht ausgeführte Prüfungen ausdrücklich benennen.
5. Keine Zugangsdaten oder personenbezogenen Echtdaten in Repository, Logs oder Testberichte aufnehmen. Beispieldaten verwenden. Bei Verdacht auf offengelegte Geheimnisse Arbeit am betroffenen Bereich stoppen und den Product Owner informieren.
6. Übergaben enthalten Issue/PR, geprüften Commit, Ergebnis, Risiken, offene Punkte und nächste zuständige Rolle. Möglichst getrennte Review-Sitzung nutzen; Selbstprüfung und verbleibende Einschränkungen offenlegen. Unteragenten nur einsetzen, wenn der Auftrag dies vorsieht.
7. Keine kostenpflichtigen Dienste ohne ausdrückliche Zustimmung. Keine produktiven Deployments oder sonstigen externen Änderungen ohne Freigabe. Ein expliziter Auftrag zum Erstellen eines Issues oder Pull Requests autorisiert diese konkrete Änderung, aber keinen Merge oder Deployment.
8. Vor externen Aktionen Ziel, Umfang und vorhandene Autorisierung prüfen. Bei fehlender Zustimmung zuerst lokal einen prüfbaren Stand vorbereiten. Keine Freigabe allein aus Schweigen ableiten.

## Freigaben

| Entscheidung | Vorbereitung | Entscheidung durch | Nachweis |
| --- | --- | --- | --- |
| Produktziel und Akzeptanzkriterien | Product Analyst | Product Owner | Issue-Kommentar oder freigegebener Produktbrief |
| Wesentliche technische Entscheidung | Architect | Product Owner bei Kosten, Umfang oder Risiken; sonst Architect innerhalb des Auftrags | ADR, bei Bedarf mit Freigabelink |
| Technische Prüfbereitschaft | Developer | QA Reviewer | Testbericht und Review zum Commit |
| Merge | QA Reviewer empfiehlt | Product Owner | Ausdrücklicher PR-Kommentar zum geprüften Stand |
| Kosten und externe Änderungen | Verantwortlicher Agent | Product Owner | Ziel, Umfang und Freigabe in Issue/PR |
| Produktiver Release | Release Manager | Product Owner | Release-Checkliste mit Version, Commit und Zielumgebung |

Bei wesentlichen Änderungen nach einer Freigabe erneut prüfen und die betroffene Freigabe erneuern lassen. Merge, Veröffentlichung eines Releases und Deployment sind eigenständige Aktionen. Bei fehlenden Rechten keine Umgehung versuchen.

## Definition of Done

- Auftrag und fachlich freigegebene Akzeptanzkriterien sind verlinkt und erfüllt; Abweichungen sind ausdrücklich akzeptiert.
- Änderung ist auf einem separaten Branch nachvollziehbar und auf den Auftrag begrenzt.
- Relevante Tests und Dokumentprüfungen sind erfolgreich; tatsächliche Ergebnisse, Grenzen und nicht ausgeführte Prüfungen sind dokumentiert.
- Review zum aktuellen Commit ist dokumentiert; kritische Fehler sind behoben. Selbstprüfung ist gekennzeichnet.
- Dokumentation und gegebenenfalls ADR, Bedienhinweise und Release-Hinweise sind aktuell.
- Keine Geheimnisse, unzulässigen Daten, unerlaubten Kosten oder externen Änderungen wurden eingebracht.
- Pull Request nennt Risiken, offene Entscheidungen und nötige Freigaben.

Diese Kriterien machen einen Pull Request bereit für die Merge-Entscheidung. Abgeschlossen ist er erst nach ausdrücklicher Merge-Freigabe und tatsächlichem Merge. Ein produktiver Release benötigt zusätzlich die [Release-Checkliste](templates/release-checklist.md).

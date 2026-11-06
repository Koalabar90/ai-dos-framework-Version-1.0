# AI-DOS Framework 1.0

AI-DOS ist ein wiederverwendbares Arbeitsmodell für die KI-gestützte Entwicklung von Browser-Anwendungen. Der Mensch entscheidet als Product Owner über Ziele, Nutzen und Freigaben. KI-Agenten analysieren, entwerfen, entwickeln, prüfen und dokumentieren.

## Voraussetzungen und Einrichtung

Benötigt werden ein GitHub-Repository, Git und ein KI-Entwicklungsagent mit Zugriff auf die Projektdateien. Dieses Framework enthält Dokumentvorlagen und Prozesse; es installiert keine Anwendung, CI-Pipeline oder Cloud-Dienste. Laufzeit, Programmiersprache, Hosting und Lizenz werden pro Projekt entschieden.

1. Framework-Dateien in ein neues GitHub-Repository übernehmen. Vorhandene Dateien vorher vergleichen; niemals ungeprüft überschreiben.
2. Inhalte aus [project-template/](project-template/README.md) in die Wurzel des neuen Projekts kopieren. Die hier vorhandenen `AGENTS.md`, Rollen, Vorlagen, Workflows und GitHub-Vorlagen beibehalten.
3. Platzhalter im Projekt-README und Produktbrief ausfüllen. Die dort vorgeschlagenen Quellcode- und Testordner erst bei Bedarf anlegen.
4. Den Product Owner sowie die zuständigen Agenten in Issues benennen. Eine KI-Sitzung darf mehrere Rollen übernehmen; für die Prüfung möglichst eine getrennte Sitzung einsetzen. Selbstprüfung kenntlich machen.
5. Produktbrief als Pull Request abstimmen. Danach Features über GitHub-Issues beauftragen.

## Aufbau

| Bereich | Zweck |
| --- | --- |
| [AGENTS.md](AGENTS.md) | Verbindliche Arbeits- und Freigaberegeln |
| [agents/](agents/README.md) | Fünf Rollen mit Aufgaben und Übergaben |
| [templates/](templates/README.md) | Kopierbare Arbeitsdokumente |
| [workflows/](workflows/README.md) | Schritte für Features, Fehlerbehebung und Releases |
| [project-template/](project-template/README.md) | Startpunkt für ein konkretes Softwareprojekt |
| [.github/ISSUE_TEMPLATE/](.github/ISSUE_TEMPLATE/feature_request.md) | Standardisierte Aufträge und Fehlerberichte |
| [Pull-Request-Vorlage](.github/pull_request_template.md) | Nachweise und Freigaben für Änderungen |

## So nutzt der Product Owner das Framework

Beschreibe zuerst das gewünschte Ergebnis und für wen es nützlich ist. Technische Lösungen musst du nicht vorgeben. Prüfe anschließend die vom Product Analyst formulierten Akzeptanzkriterien: Das sind beobachtbare Bedingungen, an denen eine erfolgreiche Umsetzung erkannt wird. Offene Fragen bleiben sichtbar im Issue.

Ein typischer Auftrag lautet: „Analysiere Issue #12 nach AGENTS.md, schlage Akzeptanzkriterien vor und bereite die Umsetzung auf einem separaten Branch vor. Warte vor dem Merge auf meine Freigabe.“ Nach der Umsetzung erhältst du einen Pull Request mit verständlicher Zusammenfassung, Prüfergebnissen und offenen Punkten.

GitHub ist die verbindliche Informationsquelle: Issues enthalten Auftrag und fachliche Freigaben; Pull Requests enthalten Änderungen, Review und Merge-Freigabe; versionierte Dokumente enthalten Produktbrief, Architekturentscheidungen, Testberichte und Release-Checklisten. Relevante Chat-Entscheidungen werden vor der Weiterarbeit dort festgehalten. Lokale Arbeit bleibt bis zur Veröffentlichung vorläufig.

## Freigaben und Fertigstellung

Fachliche Freigabe, Merge-Freigabe und Produktionsfreigabe sind getrennte Entscheidungen. Eine Freigabe gilt nur für den dokumentierten Umfang und Stand. Kostenpflichtige Dienste und sonstige externe Änderungen benötigen ebenfalls vorherige Zustimmung; der konkrete Auftrag kann diese bereits enthalten. Die vollständige [Definition of Done](AGENTS.md#definition-of-done) gilt für jeden Pull Request. Ein Merge erfolgt erst nach ausdrücklicher Freigabe des Product Owners.

## Noch zu entscheiden

Vor dem ersten Softwareprojekt: Produktziel, Nutzergruppe, Daten und Schutzbedarf, Budget, Technologie, Hosting und Lizenz festlegen. Vor dem ersten Release: Versionsschema, Zielumgebung, Verantwortliche und Rückkehr zum vorherigen Stand abstimmen. Das Framework legt diese Entscheidungen bewusst nicht pauschal fest.

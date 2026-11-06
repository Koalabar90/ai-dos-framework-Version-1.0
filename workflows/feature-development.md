# Feature Development

| Schritt / Status | Verantwortlich | Ergebnis und Übergabe |
| --- | --- | --- |
| 1. Entwurf | Product Analyst | Issue aus Feature-Vorlage, Nutzen, Kriterien, Nicht-Ziele und offene Fragen |
| 2. Fachlich freigegeben | Product Owner | dokumentierte Zustimmung zu Umfang und Kriterien; Übergabe an Architect |
| 3. Geplant | Architect | kleiner Lösungsplan und bei Bedarf ADR; Kosten und wesentliche fachliche Folgen vorher freigeben lassen |
| 4. In Umsetzung | Developer | separater Branch, Implementierung, passende Tests und Dokumentation |
| 5. Im Review | QA Reviewer | PR und Testbericht zum aktuellen Commit; bei Befunden zurück an Developer und erneut prüfen |
| 6. Bereit zur Freigabe | QA Reviewer | Definition of Done geprüft, verständliche Empfehlung an Product Owner |
| 7. Übernommen | Product Owner; autorisierter ausführender Agent | ausdrückliche Merge-Freigabe zum geprüften Stand, danach Merge und Issue-Abschluss |

**Eingang:** Produktbrief und beauftragte Idee. **Ausgang:** freigegebene, übernommene Änderung mit Nachweisen. Veröffentlichungen folgen dem separaten [Release-Prozess](release-management.md).

Ändern sich Umfang oder Kriterien, vor abhängiger Umsetzung zu Schritt 2 zurückkehren. Bei offenem Entscheidungsbedarf den betroffenen Teil als blockiert markieren. Abgeschlossen ist das Feature nach Definition of Done, ausdrücklicher Merge-Freigabe und Merge.

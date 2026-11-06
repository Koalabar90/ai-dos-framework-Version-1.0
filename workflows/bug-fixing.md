# Bug Fixing

| Schritt / Status | Verantwortlich | Ergebnis und Übergabe |
| --- | --- | --- |
| 1. Erfasst | Product Analyst | Bug-Issue mit Soll/Ist, Reproduktionsschritten, Umgebung und Auswirkung; keine sensiblen Echtdaten |
| 2. Eingeordnet | Product Owner mit QA Reviewer | Priorität und erwartetes korrektes Verhalten bestätigen; bei unklarem Soll fachliche Klärung |
| 3. Analysiert | Developer; Architect bei strukturellen Folgen | Ursache und begrenzten Korrekturplan im Issue dokumentieren |
| 4. Korrigiert | Developer | separater Branch, Korrektur und geeigneter Regressionstest, soweit sinnvoll reproduzierbar |
| 5. Geprüft | QA Reviewer | ursprünglichen Fehler und betroffene Funktionen am aktuellen Commit nachprüfen; Testbericht |
| 6. Übernommen | Product Owner; autorisierter ausführender Agent | ausdrückliche Merge-Freigabe, Merge und Issue mit Nachweisen schließen |

**Eingang:** Fehlerbericht. **Ausgang:** nachgewiesene Korrektur mit erfüllter Definition of Done und Merge. Ist der Fehler nicht reproduzierbar, Beobachtungen und fehlende Informationen dokumentieren; keine erfolgreiche Behebung behaupten.

Auch dringende Fehler umgehen keine Freigaben. Produktive Änderungen folgen dem [Release-Prozess](release-management.md). Bei Sicherheitsproblemen sensible Details nicht in öffentliche Issues schreiben; zunächst vertraulichen Meldeweg mit dem Product Owner abstimmen.

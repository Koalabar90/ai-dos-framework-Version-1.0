# Release Management

1. **Vorbereitet – Release Manager:** Umfang, Version, Zielumgebung, exakten Commit und geplante externe Aktionen in der Release-Checkliste erfassen. Enthaltene PRs müssen geprüft und mit Merge-Freigabe übernommen sein.
2. **Geprüft – QA Reviewer:** Release-Stand, relevante Nutzungsschritte und bekannte Risiken prüfen. Nachweise zum exakten Commit verlinken. Release Manager ergänzt verständliche Änderungshinweise und Rückkehrplan.
3. **Zur Freigabe – Product Owner:** Prüffähige Checkliste vorlegen. Kosten, Tag/Release-Veröffentlichung und produktives Deployment jeweils ausdrücklich für Ziel und Stand genehmigen lassen. Nicht genehmigte Aktionen bleiben ausstehend.
4. **Veröffentlicht – Release Manager:** Nur genehmigte Aktionen ausführen. Ergebnis, Zeit und Links dokumentieren. Bei Störungen stoppen und nur im genehmigten Rahmen zurückkehren; sonst Entscheidung einholen.
5. **Abgeschlossen – Release Manager und QA Reviewer:** Erreichbarkeit und Kernfunktionen nachprüfen, Product Owner informieren und offene Maßnahmen mit Zuständigkeit festhalten. Bei Abbruch Status und Ursache dokumentieren.

**Definition of Done für einen Release:** Release-Checkliste ist vollständig ausgefüllt, alle ausgeführten Aktionen sind autorisiert, tatsächlicher Stand und Nachkontrolle sind belegt, offene Maßnahmen sind zugewiesen. Eine vorbereitete Checkliste allein bedeutet keine Veröffentlichung.

Ein bestimmtes Hosting, eine CI-Pipeline oder kostenpflichtige Dienste werden durch diesen Ablauf nicht vorausgesetzt.

# Release-Checkliste: <Version>

- Release Manager: <Name>
- Datum / Zielumgebung: <Werte>
- Exakter Commit / zugehörige PRs: <Hash und Links>
- Geplante externe Aktionen: <Tag, GitHub Release, Deployment einzeln nennen>
- Status: vorbereitet / freigegeben / veröffentlicht / abgebrochen

## Vorbereitung
- [ ] Umfang und Versionsschema sind abgestimmt.
- [ ] Enthaltene PRs erfüllen die Definition of Done und wurden mit Freigabe übernommen.
- [ ] QA-Bericht zum Release-Commit ist verlinkt: <Link>.
- [ ] Bekannte Einschränkungen und Änderungen für Nutzer sind beschrieben: <Text/Link>.
- [ ] Notwendige Datenänderungen und Sicherungen sind geklärt oder begründet nicht zutreffend.
- [ ] Rückkehr zum vorherigen Stand ist beschrieben: <vorheriger Stand, Schritte, Befugnis, Grenzen>.
- [ ] Zuständigkeit für Prüfung und Betrieb ist benannt: <Person/Rolle>.
- [ ] Kostenpflichtige Dienste sind ausdrücklich genehmigt oder nicht erforderlich.

## Freigaben
| Aktion | Ziel, Version und Commit | Product Owner / Datum | Nachweis |
| --- | --- | --- | --- |
| <konkrete Aktion> | <Stand und Ziel> | <Name, Datum> | <GitHub-Link oder ausstehend> |

Ohne passende Freigabe keine externe Aktion. Eine Merge-Freigabe erlaubt kein produktives Deployment.

## Durchführung und Nachkontrolle
- [ ] Nur die freigegebenen Aktionen wurden ausgeführt: <Zeitpunkt und Ergebnislinks>.
- [ ] Erreichbarkeit und zentrale Nutzungsschritte sind geprüft: <Nachweis>.
- [ ] Bei Fehlern ist der genehmigte Rückkehrplan angewendet oder die Entscheidung des Product Owners eingeholt worden.
- [ ] Tatsächlicher Endstatus, offene Maßnahmen und Verantwortliche sind dokumentiert: <Einträge>.

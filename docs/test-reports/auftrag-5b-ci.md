# Testbericht: Auftrag 5B – CI Quality Gates

- Datum: 2026-11-07.
- Ausgangsstand: `cb3b3966d48b4a99fb47dcf4907ca8f69fdad080` auf `main`.
- Branch: `codex/5b-ci-quality-gates`.
- Auftrag und fachliche Anforderungen: direkter Auftrag des Product Owners im Codex-Chat, im zugehörigen Pull Request festgehalten.
- Prüfart: Selbstprüfung; kein unabhängiger zweiter Prüfer.

## Ausgangslage und Umsetzung

Auf main besteht bereits ein einzelner Workflow mit allen fünf beauftragten Prüfungen: Framework-Struktur, Markdown-Format, interne Dateiverweise, GitHub-YAML und Secret-Erkennung. Diese werden erhalten. Auftrag 5B ergänzt verständlichere Fehler bei fehlgeschlagener Markdown-Werkzeuginstallation und YAML-Strukturproblemen sowie die sichere Maskierung von YAML-Dateinamen in GitHub-Annotationen. Keine neuen Actions, Abhängigkeiten, Job-Namen oder doppelten Prüfungen.

## Schutzregeln – ausschließlich lesend geprüft

Das Ruleset „AI-DOS Main Protection“, ID 26732560, wurde am 2026-11-07 über die GitHub-API gelesen: `enforcement: active`, Ziel `refs/heads/main`. Alle fünf Checks sind bereits verpflichtend und an GitHub Actions (Integration 15368) gebunden. Pull Requests bleiben vorgeschrieben, die Zahl zusätzlicher Genehmigungen steht auf 0. Auftrag 5B verändert weder Regeln noch Berechtigungen. Der gespeicherte Ausgangsstand wird vor Abschluss erneut verglichen.

## Tatsächliche Tests

Die bestehenden 20 Inhalts- und Fehlerfalltests aus Auftrag 005 wurden mit den tatsächlichen Inline-Prüfungen der aktualisierten Workflow-Datei erneut ausgeführt: **20/20 erwartete Ergebnisse erreicht**. Der gültige Stand bestand alle lokalen Prüfungen; fehlende Pflichtdateien/Ordner, kaputte Links, falsches Markdown/YAML/Workflow-Schema sowie künstliche Secrets im Arbeitsstand und ausschließlich in der Historie wurden korrekt abgewiesen. Fehlerfälle fanden nur in temporären Verzeichnissen statt.

Zusätzlich **6/6 Tests bestanden**: kontrolliert simulierte erfolgreiche und fehlgeschlagene npm-Installation, fehlendes und falsch typisiertes Issue-Pflichtfeld, falscher Titeltyp sowie doppelte YAML-Schlüssel in einem Dateinamen mit Komma und Zeilenumbruch. Die Fehlersimulation bestätigte den Fehlerstatus 1 und die verständliche Meldung, dass keine Formatprüfung stattgefunden hat. Der ungewöhnliche Dateiname wurde korrekt maskiert. Die echten npm-Pakete werden im PR-Durchlauf auf GitHub installiert; die Simulation ersetzt diesen Nachweis nicht.

Werkzeuge lokal: Node 22.23.4, Python 3.11.1, markdownlint 0.42.0, markdown-it-py 4.2.0, PyYAML 6.0.3, actionlint 1.7.12 und Gitleaks 8.30.1. Git-Formatprüfung und actionlint bestanden. Der verlinkte PR dokumentiert vor Übergabe die echten GitHub-Ergebnisse einschließlich Commit und Durchlauf. Ein lokaler Erfolg wird nicht als erfolgreicher GitHub-Durchlauf gewertet.

## Grenzen

Externe Webseiten, Überschriftenanker, HTML-Linkziele und undefinierte Referenzlabels werden weiterhin nicht validiert. Secret-Erkennung kann Fehlalarme und Erkennungslücken haben. GitHub-Laufzeit und externe Werkzeuge bleiben Vertrauensabhängigkeiten. Keine Anwendung vorhanden, daher keine Browser- oder Anwendungstests. Keine Veröffentlichung, kein Merge und keine Änderung von Schutzregeln durch Auftrag 5B.

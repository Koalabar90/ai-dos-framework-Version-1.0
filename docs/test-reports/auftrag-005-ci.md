# Testbericht: Auftrag 005 – CI-Qualitätsprüfungen

- Datum: 2026-11-06
- Auftrag: AI-DOS Auftrag 005, ausdrücklich durch den Product Owner im Codex-Chat beauftragt.
- Ausgangsstand: `main` auf `a26e01512aea5978e8b6b0374703ab91d9041d7b`.
- Entwicklungsbranch: `codex/005-ci-quality-checks`.
- Prüfart: Selbstprüfung durch den erstellenden Agenten; kein unabhängiges Review.
- Umfang: Erweiterung des einzigen vorhandenen Workflows; keine Repository-Regeln und keine Merge- oder Deployment-Aktionen.

## Lokale Umgebung und Durchführung

macOS ARM64, Node 22.23.4, Python 3.11.1; markdownlint 0.42.0, markdown-it-py 4.2.0, PyYAML 6.0.3, actionlint 1.7.12 und Gitleaks 8.30.1. Die heruntergeladenen Programme wurden gegen die offiziellen SHA-256-Werte geprüft. GitHub verwendet Ubuntu und Python 3.12; diese abweichende Umgebung wird zusätzlich durch den echten PR-Durchlauf geprüft.

Ein temporärer Testtreiber liest die tatsächlich im Workflow enthaltenen Inline-Prüfungen, führt sie auf einer wegwerfbaren Repository-Kopie aus und vergleicht die Rückgabewerte mit den erwarteten Ergebnissen. Die actionlint- und Secret-Befehle wurden ebenfalls ausgeführt. Fehlerfälle verändern weder das echte Repository noch dessen Historie. Künstliche Zugangsdaten sind nicht funktionsfähig und werden nicht in diesen Branch übernommen. Der Testtreiber dient der Implementierungsprüfung und wird nicht als aus Pull Requests ausführbares Projektskript eingebaut.

## Tatsächliche Ergebnisse

| Prüfung | Erwartet | Tatsächlich |
| --- | --- | --- |
| Gültiger Stand: Framework-Struktur | erfolgreich | erfolgreich |
| Gültiger Stand: Markdown-Format | erfolgreich | erfolgreich |
| Gültiger Stand: interne Verweise | erfolgreich | erfolgreich |
| Gültiger Stand: GitHub-YAML und Issue-Köpfe | erfolgreich | erfolgreich |
| Gültiger Stand: actionlint | erfolgreich | erfolgreich |
| Gültiger Stand: Secret-Scan von Arbeitsstand und Historie | kein Fund | kein Fund |
| README fehlt | Fehler mit Dateiname | korrekt abgewiesen |
| AGENTS fehlt | Fehler mit Dateiname | korrekt abgewiesen |
| Rollenordner fehlt | Fehler | korrekt abgewiesen |
| README ist symbolischer Link | Fehler | korrekt abgewiesen |
| Überschriftensprung und überflüssige Leerzeichen | Formatfehler | korrekt abgewiesen, MD009 bestätigt |
| Definierte Referenzlinks, kodierte Dateinamen, Wurzel- und Ordnerziele | erfolgreich | erfolgreich |
| Links in Codebeispielen und externe URLs | auslassen | korrekt ausgelassen |
| Fehlender Dateilink, fehlendes Bild und Pfad außerhalb des Repositorys | Fehler | korrekt abgewiesen |
| Ungültige YAML-Syntax | Fehler | korrekt abgewiesen |
| Doppelter YAML-Schlüssel | Fehler | korrekt abgewiesen |
| YAML-Liste statt Konfigurationszuordnung | Fehler | korrekt abgewiesen |
| Fehlendes Pflichtfeld im Issue-Kopf | Fehler | korrekt abgewiesen |
| Unbekanntes Feld statt `runs-on` | Strukturfehler | durch actionlint abgewiesen |
| Künstlicher Zugangsschlüssel im Arbeitsstand | Fund, geschwärzte Ausgabe | korrekt erkannt; sichtbare Meldung enthält nur Metadaten |
| Künstlicher Zugangsschlüssel nur in älterem Commit | Fund trotz sauberem aktuellem Stand | korrekt erkannt |

Der Testtreiber fasst die beiden zusammengehörigen Link-Erfolgsprüfungen zu einem Fall zusammen: **20 von 20 Testfällen erfüllten das erwartete Ergebnis**. Die absichtlich ungültigen Fälle endeten mit Fehlerstatus; das ist ihr erwarteter Erfolg und kein offener Defekt der Pipeline.

## GitHub-Durchlauf

Erster tatsächlicher [GitHub-Durchlauf](https://github.com/Koalabar90/ai-dos-framework-Version-1.0/actions/runs/42308606330), Commit `bd07948`: Struktur, Verweise, GitHub-Konfiguration und Secret-Scan bestanden. Die Markdown-Werkzeuginstallation schlug fehl; die Formatprüfung wurde deshalb übersprungen. Ursache war, dass npm dieselbe Datei `/dev/null` nicht gleichzeitig als Benutzer- und globale Konfiguration laden darf.

Korrektur: zwei getrennte leere Konfigurationsdateien im temporären Verzeichnis. Der korrigierte, unveränderte Installationsschritt aus dem Workflow wurde anschließend lokal mit Node 22 erfolgreich ausgeführt; 51 Pakete wurden ohne Installationsskripte bereitgestellt. Das ergänzt die 20 Inhalts- und Fehlerfalltests um einen erfolgreichen Test der tatsächlichen Werkzeugbereitstellung. Die nachfolgenden GitHub-Ergebnisse werden im [Pull Request #7](https://github.com/Koalabar90/ai-dos-framework-Version-1.0/pull/7) zum jeweiligen Commit dokumentiert. Ein fehlgeschlagener oder übersprungener Job wird nicht als bestanden gezählt.

Zweiter tatsächlicher [GitHub-Durchlauf](https://github.com/Koalabar90/ai-dos-framework-Version-1.0/actions/runs/42308876650), Commit `62db1904472c4e75bfd375652759808024c52a86`: **alle fünf Jobs vollständig ausgeführt und bestanden**. Insbesondere wurden diesmal sowohl die Markdown-Werkzeuginstallation als auch die eigentliche Formatprüfung erfolgreich ausgeführt.

| GitHub-Check | Zweiter Durchlauf |
| --- | --- |
| `CI / Framework structure` | bestanden |
| `CI / Markdown style` | bestanden |
| `CI / Markdown links` | bestanden |
| `CI / GitHub configuration` | bestanden |
| `CI / Secret scan` | bestanden |

Die anschließende Ergänzung dieses Berichts ändert keine Prüflogik; auch für diesen Dokumentationsstand werden die fünf PR-Prüfungen erneut abgewartet. Der jeweils aktuelle Stand ist im verlinkten Pull Request sichtbar.

## Grenzen und verbleibende Risiken

- Kein unabhängiger zweiter Prüfer und keine Browser- oder Anwendungstests; das Framework enthält noch keine Anwendung.
- Keine Prüfung externer Webseiten, HTML-Linkziele, nicht aufgelöster Referenzlabels oder Überschriftenanker.
- Der Secret-Scanner kann unbekannte Geheimnisse übersehen und harmlose Beispiele beanstanden. Nur abgerufene, erreichbare Historie ist prüfbar.
- Fremde Werkzeuge und GitHub-Laufzeit bleiben eine Vertrauensabhängigkeit. Versionen, Sperrdatei, Action-Commits und Prüfsummen begrenzen unbemerkte Änderungen.
- Änderungen am Workflow und an Werkzeugabhängigkeiten benötigen inhaltliches Review; der Workflow kann nicht seine eigene Unveränderlichkeit garantieren.
- Keine neuen verpflichtenden Checks oder Rulesets gesetzt. Kein Merge und kein Deployment durchgeführt.

Die [CI-Dokumentation](../ci-quality-checks.md) erklärt Regeln, Wartung und die fünf exakten Check-Namen.

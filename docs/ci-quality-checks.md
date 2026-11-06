# Automatische Qualitätsprüfungen

Die Datei `.github/workflows/framework-check.yml` enthält die einzige CI-Pipeline des Frameworks. „CI“ bedeutet hier: GitHub prüft vorgeschlagene Änderungen automatisch, bevor der Product Owner über die Übernahme entscheidet. Es werden keine Anwendungen veröffentlicht und keine zusätzlichen Dienste betrieben.

## Ausführung und Namen der Prüfungen

Die Prüfungen laufen bei neu eröffneten, wieder geöffneten oder aktualisierten Pull Requests mit Ziel `main`. Es gibt bewusst keinen zusätzlichen Push-Workflow und keinen Dateifilter, der wichtige Prüfungen auslassen könnte. Unter **Actions → AI-DOS Framework Check → Run workflow** ist ein manueller Start möglich, sobald dieser Workflow im Standardbranch liegt. Ein neuer Durchlauf ersetzt einen noch laufenden Durchlauf derselben Änderung.

| Exakter GitHub-Check-Name | Was wird geprüft? |
| --- | --- |
| `CI / Framework structure` | Die vorhandenen Framework-Ordner und ihre verbindlichen Dateien einschließlich README und AGENTS |
| `CI / Markdown style` | Ein ausdrücklich ausgewähltes, gemeinsames Regelwerk für alle versionierten Markdown-Dateien |
| `CI / Markdown links` | Interne Datei- und Ordnerziele von Markdown-Verweisen und Bildern |
| `CI / GitHub configuration` | YAML-Syntax, doppelte Schlüssel, Issue-Vorlagen und die Struktur der GitHub-Actions-Workflows |
| `CI / Secret scan` | Mögliche Zugangsdaten im aktuellen Dateistand und in der gesamten abgerufenen Git-Historie |

Die Jobs laufen unabhängig voneinander, sodass beispielsweise ein Formatfehler die Secret-Prüfung nicht verhindert. Alle fünf Namen sind unterschiedlich und können nach erfolgreichem Test gezielt als verpflichtende Prüfungen ausgewählt werden. Dieser Auftrag ändert keine Branch-Regeln oder Rulesets. Der bisherige Check-Name „Framework-Dateien prüfen“ wird durch `CI / Framework structure` ersetzt; die bisherige Prüfung von README und AGENTS bleibt enthalten.

## Framework-Struktur

Die Dateiliste steht gut sichtbar im ersten Job des Workflows. Sie folgt der tatsächlich vorhandenen Struktur: fünf Rollen, fünf Arbeitsvorlagen, drei Prozessbeschreibungen, Projektvorlage, GitHub-Issue- und PR-Vorlagen sowie die CI-Konfiguration und ihre Dokumentation. Die Bereichs-README-Dateien gehören ebenfalls dazu. Erforderliche Pfade müssen echte Dateien beziehungsweise Ordner sein; symbolische Links an diesen Stellen sind nicht erlaubt.

Absichtlich nicht verlangt werden Anwendungscode, ein `tests/`-Ordner, Cloud-Konfigurationen oder eine Laufzeitumgebung für ein späteres Softwareprojekt. Neue verbindliche Dateien werden ausdrücklich in diese Liste aufgenommen; die Pipeline erfindet keine Projektstruktur.

## Markdown-Regeln

Die Regeln stehen in `.github/ci/markdownlint.json`. Geprüft wird mit markdownlint 0.42.0. Die Grundmenge ist ausdrücklich ausgeschaltet (`default: false`); diese Regeln sind eingeschaltet:

| Regel | Bedeutung |
| --- | --- |
| MD001 | Keine übersprungenen Überschriftenebenen |
| MD003 | Überschriften mit `#` statt wechselnder Schreibweisen |
| MD009 | Keine überflüssigen Leerzeichen am Zeilenende; übliche Markdown-Zeilenumbrüche bleiben erlaubt |
| MD010 | Keine Tabulatoren |
| MD012 | Keine mehrfachen Leerzeilen |
| MD018, MD019, MD023 | Saubere Abstände und Einrückung von Überschriften |
| MD047 | Abschließender Zeilenumbruch |
| MD048 | Codeblöcke mit Backticks |
| MD050 | Hervorhebungen mit Sternchen |

Lange deutsche Absätze und Tabellen erhalten keine starre Zeilenlängenbegrenzung. Vorlagen dürfen Platzhalter in spitzen Klammern enthalten und mit einer Überschrift zweiter Ebene beginnen. Zusätzliche Leerzeilen vor Listen und nach Überschriften sind keine Pflicht dieses ersten Regelwerks. Andere Regeln bleiben aus, bis sie bewusst vereinbart werden. Regeln werden nicht durch Kommentare in einzelnen Markdown-Dateien deaktiviert. Es werden weder lokale JavaScript-Konfigurationen noch Markdown-Plugins aus dem Repository geladen.

## Interne Verweise

markdown-it-py 4.2.0 liest die Markdown-Struktur einschließlich Tabellen. Geprüft werden normale Links, definierte Referenzlinks und Bilder. Codebeispiele werden nicht als Links gewertet. Relative Ziele beziehen sich auf das Dokument; Ziele mit führendem `/` auf die Repository-Wurzel. Prozentkodierte Namen werden aufgelöst. Vorhandene Ordner sind gültige Ziele; Verweise außerhalb des Repositorys und nicht vorhandene Ziele führen zu einem Fehler. Auf GitHub zählt die Groß- und Kleinschreibung des Linux-Dateisystems.

Externe Webseiten werden nicht abgerufen; ihre Erreichbarkeit kann die CI daher nicht zufällig blockieren. Überschriftenanker nach `#`, rohe HTML-Verweise und nicht aufgelöste Referenzlabels werden nicht validiert. Ein vorhandenes Dateiziel sagt nichts über dessen fachliche Richtigkeit aus. Das spätere Kopieren der Projektvorlage muss weiterhin nach der README-Anleitung geprüft werden.

## GitHub-Konfigurationen

PyYAML 6.0.3 liest alle `.yml`- und `.yaml`-Dateien unter `.github/` mit einem sicheren Leser, der keine Objekte oder Programme aus YAML erzeugt. GitHubs Schlüssel `on` bleibt Text; doppelte Schlüssel und fehlerhafte Syntax werden abgewiesen. Die Wurzel muss eine Zuordnung von Schlüsseln und Werten sein. Die YAML-Köpfe der Markdown-Issue-Vorlagen benötigen `name` und `about`; optionale Felder `title`, `labels` und `assignees` müssen Text sein.

Zusätzlich prüft actionlint 1.7.12 die eigentliche Workflow-Struktur, Ereignisse, Job-Verweise und GitHub-Ausdrücke. Dabei werden keine im Workflow gefundenen Befehle ausgeführt. Projektdateien dürfen die actionlint-Konfiguration nicht übersteuern; die optionalen ShellCheck- und Pyflakes-Anbindungen sind ausgeschaltet. Andere GitHub-Konfigurationen erhalten eine Syntax- und Grundstrukturprüfung, keine vollständige fachliche Schema-Prüfung für jedes GitHub-Produkt. GitHub selbst entscheidet weiterhin, ob eine Konfiguration mit Kontoeinstellungen und aktuellen Plattformregeln zusammenpasst.

## Zugangsdaten erkennen

Gitleaks 8.30.1 arbeitet mit seinen mitgelieferten Standardregeln. Es prüft den Arbeitsstand und alle erreichbaren Commits der abgerufenen Historie. Der Secret-Job lädt deshalb die vollständige Historie. Eigene Ausschlussdateien, Baselines und `gitleaks:allow`-Kommentare aus dem Repository können diese Prüfung nicht abschwächen. Es wird kein Lizenzschlüssel und kein zusätzliches Secret benötigt.

Fundstellen werden mit Datei, Zeile, Regel und gegebenenfalls Commit angezeigt. Vertrauliche Werte und Quelltextausschnitte werden nicht in das sichtbare Ergebnis kopiert. Die internen Berichte sind vollständig geschwärzt und werden nicht als Artefakte veröffentlicht. Ein möglicher Fund ist zunächst ein Verdacht: Der Product Owner muss die Fundstelle prüfen lassen. Echte Zugangsdaten müssen beim ausstellenden Dienst gesperrt oder ersetzt werden; bloßes Löschen im aktuellen Stand entfernt sie nicht aus der Historie.

Auch dieser Scanner kann unbekannte Formate übersehen und harmlose Beispiele beanstanden. Nicht erreichbare oder nicht abgerufene Commits und Dateien außerhalb des Repositorys sind nicht erfasst. Die Prüfung ersetzt keinen sicheren Umgang mit Zugangsdaten und keine unabhängige Sicherheitsprüfung.

## Sicherheit und Wartung

- Standardberechtigung ist ausschließlich `contents: read`; alle anderen GitHub-Token-Rechte bleiben gesperrt.
- Es gibt kein `pull_request_target`, kein Deployment und keinen Zugriff auf eigene Secrets.
- Git speichert die automatisch bereitgestellten Lesezugangsdaten nicht dauerhaft im Checkout.
- Alle verwendeten GitHub Actions sind auf vollständige Commit-IDs festgelegt. Werkzeugversionen und SHA-256-Prüfsummen für actionlint und Gitleaks stehen direkt im Workflow. Python-Pakete sind auf Version und Wheel-Prüfsumme begrenzt; es werden keine Quellpakete gebaut.
- Markdown-Werkzeuge sind in `.github/ci/package.json` und `package-lock.json` mit Versionen und Integritätswerten festgehalten. Die Installation erfolgt außerhalb des Repositorys, ohne Lebenszyklus-Skripte und ohne Projekt-`.npmrc`.
- Der Workflow führt keine aus dem Repository geladenen Shell-, Python-, JavaScript- oder Anwendungsskripte aus. Die kurzen Prüfabläufe stehen unmittelbar im zu prüfenden Workflow. Deklarative JSON-Regeln werden als Daten gelesen; Programme und Konfigurationen der Prüfer stammen aus den festgelegten Werkzeugversionen.
- Änderungen am Workflow, an Werkzeugabhängigkeiten und Regeln müssen vor dem Merge inhaltlich geprüft werden. Ein PR kann seinen eigenen Workflow ändern; diese Pipeline verhindert das nicht und kann nicht selbst ihre Vertrauenswürdigkeit beweisen. Unveränderliche Actions schützen nicht vor böswilligen Änderungen der Workflow-Datei selbst.
- Jeder Job nutzt einen frischen GitHub-Rechner mit `ubuntu-latest` und höchstens zehn Minuten Laufzeit. GitHub-Laufzeit und die Betriebssystemabbilder werden von GitHub aktualisiert. Kostenpflichtige Zusatzdienste oder Abrechnungsänderungen werden nicht eingerichtet; vorhandene Actions-Kontingente und Kontoeinstellungen gelten weiter.

Werkzeugupdates werden als eigener Pull Request vorgenommen: Version, Action-Commit beziehungsweise Prüfsumme und Sperrdatei gemeinsam aktualisieren, Dokumentation anpassen, positiven und absichtlich fehlerhaften Fall testen und alle fünf GitHub-Prüfungen abwarten. Ein Netz- oder Downloadfehler ist ein fehlgeschlagener Durchlauf und darf nicht als bestandene Inhaltsprüfung beschrieben werden.

## Fehler verstehen und lokal nachprüfen

Die Jobs nennen betroffene Dateien und, soweit verfügbar, Zeilennummern. Alle Prüfungen enden bei Fehlern mit einem erfolglosen Status; es gibt kein `continue-on-error`. Die Secret-Prüfung zeigt ausschließlich Fundstellen-Metadaten. Die Workflow-Strukturprüfung zeigt actionlint-Befunde im Protokoll.

Die konkreten Prüfbefehle stehen bei jedem Schritt in der Workflow-Datei. Für eine lokale Wiederholung dieselben Werkzeugversionen bereitstellen, die jeweilige Inline-Prüfung im Repository ausführen und die temporären Werkzeugpfade an die lokale Umgebung anpassen. Linux-Binärdateien und die Python-3.12-Linux-Wheel-Prüfsumme aus dem Workflow sind für GitHub vorgesehen; auf anderen Systemen die passenden offiziellen Pakete und Prüfsummen verwenden. Keine geheimen Testwerte in den Arbeitsbranch einchecken.

Die tatsächlichen Durchläufe und kontrollierten Fehlerfälle für Auftrag 005 werden im [Testbericht](test-reports/auftrag-005-ci.md) dokumentiert. Inhaltliche Qualität, Produktentscheidungen, Browser-Funktion und produktive Betriebsbereitschaft bleiben weiterhin Aufgaben des Reviews und gegebenenfalls eigener Anwendungstests.

## Werkzeugdokumentation

- [GitHub-Workflow-Syntax](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax)
- [markdownlint-Regeln](https://github.com/DavidAnson/markdownlint/blob/v0.42.0/doc/Rules.md)
- [markdown-it-py](https://markdown-it-py.readthedocs.io/en/latest/using.html)
- [PyYAML](https://pyyaml.org/wiki/PyYAMLDocumentation)
- [actionlint](https://github.com/rhysd/actionlint/tree/v1.7.12/docs)
- [Gitleaks](https://github.com/gitleaks/gitleaks/tree/v8.30.1)

## Quality Gates – Auftrag 5B

Am 2026-11-07 wurde über die GitHub-API verifiziert: Das Ruleset „AI-DOS Main Protection“ (ID 26732560) ist aktiv und gilt für `refs/heads/main`. Die fünf oben genannten Checks sind dort bereits als verpflichtend hinterlegt und an GitHub Actions gebunden. Das ist eine Aufnahme des Prüfzeitpunkts, keine automatische Überwachung späterer Einstellungsänderungen. Auftrag 5B verändert weder dieses Ruleset noch Repository-Berechtigungen.

Die vorhandenen fünf Jobs und ihre Namen bleiben erhalten. Bei einer fehlgeschlagenen Markdown-Werkzeuginstallation erscheint nun ausdrücklich, dass die eigentliche Formatprüfung nicht ausgeführt wurde. Ein solcher Fehler bedeutet keine erfolgreiche Markdown-Prüfung. Für YAML werden fehlende Pflichtfelder, falsche Feldtypen und doppelte Schlüssel verständlicher benannt. YAML-Quelltext wird dabei nicht ausgegeben; ungewöhnliche Dateinamen werden für GitHub-Fehlermeldungen maskiert.

Die bisherigen Regeln und Einschränkungen gelten weiterhin. Der [Testbericht zu Auftrag 5B](test-reports/auftrag-5b-ci.md) enthält die tatsächlich ausgeführten Prüfungen. Die bereits durchgeführte absichtliche Umbenennung von `AGENTS.md` in [Test-PR #8](https://github.com/Koalabar90/ai-dos-framework-Version-1.0/pull/8) bleibt ein Nachweis der bestehenden Struktur- und Linkprüfung; sie wird in 5B nicht erneut eingebaut.

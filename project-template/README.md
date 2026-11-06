# <Projektname>

> Vorlage: Dieses Dokument beim Projektstart in die Projektwurzel kopieren, Platzhalter ersetzen und diesen Hinweis entfernen. Die Framework-Regeln und Verzeichnisse aus AI-DOS beibehalten. Es wird kein lauffähiges Softwaregerüst mitgeliefert.

## Ziel und Nutzer
<Welches Problem löst die Browser-Anwendung für wen?>

## Verbindliche Informationen

- Produktbrief: [docs/product-brief.md](docs/product-brief.md)
- Arbeitsregeln: `AGENTS.md` in der Projektwurzel
- Aufträge und Freigaben: <GitHub-Repository und Issues>
- Product Owner: <Name>
- Status: <Planung / Entwicklung / Betrieb>

## Lokale Einrichtung
<Voraussetzungen, Installation und Startbefehle erst nach der Technologieentscheidung ergänzen. Keine erfundenen oder ungeprüften Befehle veröffentlichen.>

## Verwendung und Prüfung
<Wichtigste Nutzungsschritte, Testbefehle und benötigte Beispieldaten nach Implementierung beschreiben.>

## Empfohlene Struktur

```text
docs/product-brief.md     Produktziel und fachliche Grenzen
docs/decisions/           Architekturentscheidungen bei Bedarf
docs/test-reports/        Konkrete Prüfnachweise
docs/releases/            Release-Checklisten bei Bedarf
src/                     Anwendungscode nach Technologieentscheidung
tests/                   Tests nach vereinbarter Teststrategie
```

Ordner erst bei Bedarf anlegen. Zusätzlich gelten `agents/`, `templates/`, `workflows/` und `.github/` aus dem Framework. Keine verschachtelte Kopie von `project-template/` im neuen Projekt nötig.

## Entscheidungen vor Umsetzung

- [ ] Produktbrief und erste Akzeptanzkriterien freigegeben.
- [ ] Technologie und Teststrategie begründet festgelegt.
- [ ] Daten, Zugriffsrechte und Schutzbedarf geklärt.
- [ ] Budget, Lizenz und gegebenenfalls Hosting entschieden.
- [ ] Lokale Einrichtung dokumentiert und tatsächlich geprüft.

## Veröffentlichung
<Zielumgebung, zuständige Person und Links zu Release-Checklisten ergänzen. Produktiver Betrieb benötigt eine gesonderte Freigabe.>

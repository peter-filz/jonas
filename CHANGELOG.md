# Changelog

Alle wichtigen Änderungen an diesem Projekt werden in dieser Datei dokumentiert.

Das Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
und dieses Projekt folgt [Semantic Versioning](https://semver.org/lang/de/).

## [1.4.5] - 2025-01-14

### Behoben
- **Kritischer Bugfix**: Fehlgeschlagene Shell-Befehle (Exit Code != 0) wurden nicht in der Session-Historie getrackt. Dies führte dazu, dass Jonas nicht wusste, welche Befehle bereits ausgeführt wurden, und sie immer wieder ausführte.
- Jetzt werden **ALLE** ausgeführten Befehle in der Historie gespeichert, unabhängig davon, ob sie erfolgreich waren oder fehlgeschlagen sind.
- Befehle ohne Output-ID (z.B. fehlgeschlagene Befehle) werden in der History-Anzeige mit "(kein Output gespeichert)" markiert.

### Geändert
- `cli.py`: Alle ausgeführten Befehle werden zur `executed_commands` Liste hinzugefügt, auch wenn sie keine Output-ID haben
- `cli.py`: History-Anzeige zeigt jetzt auch Befehle ohne Output-ID an

## [1.4.4] - 2025-01-14

### Behoben
- **Kritischer Bugfix**: Shell-Befehle, die ihre Ausgabe nach stderr schreiben (z.B. curl, git, npm), wurden fälschlicherweise als fehlgeschlagen behandelt, obwohl sie mit Exit Code 0 endeten. Dies führte dazu, dass diese Befehle keine Output-ID erhielten und somit nicht in der Session-Historie (`history` Befehl) auftauchten.
- Die Fehlerbehandlung in `shell_tools.py` wurde korrigiert: Jetzt wird nur noch der Exit Code zur Fehlerbestimmung verwendet. stderr-Ausgaben werden bei Exit Code 0 als normale Ausgabe behandelt und mit stdout kombiniert.
- Im Timeout-Fall (maximale Anzahl von Tool-Call-Iterationen erreicht) werden jetzt die `executed_commands` korrekt gespeichert.

### Geändert
- `shell_tools.py`: Fehlerprüfung basiert jetzt ausschließlich auf dem Exit Code (returncode != 0)
- `shell_tools.py`: Bei erfolgreichen Befehlen (Exit Code 0) werden stdout und stderr kombiniert
- `cli.py`: Im Timeout-Szenario werden `executed_commands` an die finale Response angehängt

## [1.4.3] - 2025-01-XX

### Hinzugefügt
- Initiale Version mit allen Basis-Features

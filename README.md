# JONAS - Just Operate Nicely And Securely

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

Ein intelligenter Shell-Assistent, der die OpenAI Responses API nutzt, um Shell-Befehle sicher auszuführen und natürliche Gespräche zu führen.

## Features

- 🤖 **Intelligenter Chat**: Natürliche Gespräche mit automatischer Kontext-Verwaltung
- 🔧 **Tool-Calling**: Sichere Ausführung von Shell-Befehlen mit Bestätigung
- 📝 **Markdown-Rendering**: Schöne Formatierung von Antworten
- 🔄 **Mehrere Tool-Calls**: Parallele Ausführung mehrerer Befehle
- ⚡ **Thinking-Anzeige**: Visuelles Feedback während API-Aufrufen
- 🔒 **Sicherheitsabfragen**: Farbcodierte Bestätigung (Rot=schreibend, Magenta=lesend)
- 🎨 **Rich Terminal UI**: Farbige, formatierte Ausgaben mit Box-Design
- 📊 **Output-Management**: Große Outputs werden gespeichert und können durchsucht werden
- 🔍 **Output-Tools**: `get_output_head()`, `get_output_tail()`, `search_output()`, `display_output()`
- 📜 **Session-Historie**: Automatische Speicherung der letzten 15 Turns
- 🌐 **Web-Search**: Integrierte Web-Suche für aktuelle Informationen
- 🎯 **Auto-Korrektur**: Erkennt und korrigiert fehlende Tool-Calls

## Installation

### Via pip (empfohlen)

```bash
pip install jonas
```

Nach der Installation ist der Befehl `jonas` systemweit verfügbar.

### Aus dem Quellcode

1. **Repository klonen:**
   ```bash
   git clone https://github.com/peterfilz/jonas.git
   cd jonas
   ```

2. **Installieren:**
   ```bash
   pip install -e .
   ```

## Konfiguration

Beim ersten Start von JONAS wirst du interaktiv nach folgenden Werten gefragt:

- **OPENAI_API_KEY**: Dein OpenAI API-Schlüssel
- **OPENAI_MODEL**: Das zu verwendende Modell (z.B. `gpt-4o`, `gpt-4.1`)
- **TOKENLIMIT**: Token-Schwellenwert für Output-Speicherung (Standard: 300)

Die Konfiguration wird in `jonas.cfg` gespeichert.

Zum Ändern der Konfiguration verwende im Chat:
```
config
```

## Verwendung

Starte JONAS einfach mit:
```bash
jonas
```

### Verfügbare Befehle:
- `exit`, `quit`, `bye` - Chat beenden
- `config` (oder `configure`) - Konfiguration ändern (API-Key, Model, TokenLimit)
- `delconfig` - Konfiguration löschen und beenden
- `history` - Gespeicherte Session-Historie anzeigen

- Oder gebe Anweisungen in natürlicher Sprache ein

### Beispiel-Interaktion:

```
Du: Zeige mir den Inhalt von /Users
Intention: Verzeichnisinhalt anzeigen
Befehl:    ls /Users
Ausführen? [j/N] j

Jonas: Das Verzeichnis /Users enthält: Applications, Library, Users, ...

Du: Welche Python-Version verwendest du?
Intention: Python-Version prüfen
Befehl:    python3 --version
Ausführen? [j/N] j

Jonas: Ich verwende Python 3.12.0

Du: history
─────────────────────────────────────────────────────────
Session-Historie:
─────────────────────────────────────────────────────────

Du: Zeige mir den Inhalt von /Users
Jonas: Das Verzeichnis /Users enthält...
Ausgeführte Befehle:
  • ls /Users → out1

Du: exit
Auf Wiedersehen!
```

## Features im Detail

### Tool-Calling mit Sicherheit
- **Readonly-Flag**: Befehle werden als lesend (Magenta) oder schreibend (Rot) markiert
- **Intention-Anzeige**: Zeigt, was der Befehl tun soll
- **Bestätigungs-Prompts**: Jeder Befehl erfordert explizite Bestätigung
- **Auto-Korrektur**: Erkennt, wenn das Modell Aktionen behauptet ohne Tool-Call
- **Timeout**: 5 Minuten für längere Befehle (apt-get upgrade, docker build, etc.)

### Output-Management
- **Automatische Speicherung**: Outputs >300 Tokens werden als `out1`, `out2`, etc. gespeichert
- **get_output_head(output_id, num_lines)**: Zeigt die ersten N Zeilen
- **get_output_tail(output_id, num_lines)**: Zeigt die letzten N Zeilen
- **search_output(output_id, pattern)**: Durchsucht Output mit Regex
- **display_output(output_id)**: Zeigt kompletten Output an
- **Automatische Bereinigung**: Alte Outputs werden beim History-Trimming gelöscht

### Session-Historie
- **Automatisches Trimming**: Maximal 15 User/Assistant-Paare werden gespeichert
- **Persistente Output-IDs**: Zugriff auf frühere Befehlsausgaben
- **JSON-Struktur**: `{"answer": "...", "executed_commands": [...]}`
- **History-Befehl**: Zeigt alle gespeicherten Turns mit ausgeführten Befehlen

### Markdown-Rendering
- Tabellen werden korrekt formatiert
- Code-Blöcke mit Syntax-Highlighting
- Listen, Links und andere Markdown-Elemente
- Rich Terminal-Ausgaben mit Farben


## Projekt-Struktur

```
jonas/
├── jonas.py             # Haupt-Chat-Anwendung mit Dialog-Logik
├── shell_tools.py       # Tool-Definitionen und Shell-Ausführung
├── requirements.txt     # Python-Abhängigkeiten
├── jonas.cfg           # Konfigurationsdatei (wird beim ersten Start erstellt)
├── venv/               # Virtuelle Umgebung
└── README.md          # Diese Datei
```

## Abhängigkeiten

- `openai`: OpenAI API-Client (Responses API)
- `pydantic>=2.7.0`: Datenvalidierung
- `rich>=13.7.0`: Schöne Terminal-Ausgaben mit Markdown-Support
- `tiktoken>=0.5.0`: Token-Zählung für Output-Management
- `typer[all]>=0.12`: CLI-Framework

## Sicherheitshinweise

- ⚠️ **API-Keys** niemals committen!
- ⚠️ **Jeder Shell-Befehl** erfordert explizite Bestätigung
- ⚠️ **Timeout** (5 Minuten) verhindert hängende Prozesse
- ⚠️ **Readonly-Flag** signalisiert Risiko (Rot vs. Magenta)
- ⚠️ **Auto-Korrektur** verhindert Halluzinationen von Befehlsausführungen
- ⚠️ **Output-Bereinigung** beim History-Trimming

## Autor

**Peter Filz**  
📧 peter.filz@googlemail.com

## Lizenz

GNU General Public License v3.0 oder später - siehe LICENSE-Datei für Details.

JONAS ist freie Software: Sie können sie unter den Bedingungen der GNU General Public License,
wie von der Free Software Foundation veröffentlicht, weitergeben und/oder modifizieren,
entweder gemäß Version 3 der Lizenz oder (nach Ihrer Option) jeder späteren Version.

Dieses Programm wird in der Hoffnung verteilt, dass es nützlich sein wird, aber
OHNE JEDE GEWÄHRLEISTUNG. Siehe die GNU General Public License für weitere Details.

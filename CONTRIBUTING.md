# Contributing to JONAS

Vielen Dank für dein Interesse an JONAS! Beiträge sind willkommen.

## Entwicklungsumgebung einrichten

1. **Repository forken und klonen:**
   ```bash
   git clone https://github.com/peter-filz/jonas.git
   cd jonas
   ```

2. **Virtual Environment erstellen:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # Linux/macOS
   ```

3. **Package im Development-Mode installieren:**
   ```bash
   pip install -e .
   ```

4. **Optional: Development-Dependencies installieren:**
   ```bash
   pip install -e ".[dev]"
   ```

## Code-Änderungen

1. **Branch erstellen:**
   ```bash
   git checkout -b feature/meine-aenderung
   ```

2. **Änderungen vornehmen**
   - Code in `src/jonas/` bearbeiten
   - Tests hinzufügen (falls vorhanden)

3. **Testen:**
   ```bash
   jonas  # Funktioniert direkt nach pip install -e .
   ```

4. **Commit und Push:**
   ```bash
   git add .
   git commit -m "Beschreibung der Änderung"
   git push origin feature/meine-aenderung
   ```

5. **Pull Request erstellen**

## Code-Style

- Python 3.8+ kompatibel
- Folge PEP 8 Konventionen
- Nutze aussagekräftige Variablennamen
- Kommentiere komplexe Logik

## Projekt-Struktur

```
jonas/
├── src/jonas/          # Haupt-Package
│   ├── __init__.py     # Package-Metadaten
│   ├── cli.py          # Hauptlogik
│   └── shell_tools.py  # Shell-Tool-Funktionen
├── pyproject.toml      # Package-Konfiguration
└── README.md           # Dokumentation
```

## Bug Reports

Bitte erstelle ein GitHub Issue mit:
- Beschreibung des Problems
- Schritte zur Reproduktion
- Erwartetes vs. tatsächliches Verhalten
- Python-Version und OS

## Feature Requests

Feature-Vorschläge sind willkommen! Erstelle ein GitHub Issue mit:
- Beschreibung des Features
- Use Case / Motivation
- Mögliche Implementierung (optional)

## Fragen?

Bei Fragen kannst du:
- Ein GitHub Issue erstellen
- Eine Email an peter.filz@googlemail.com schicken

Danke für deine Unterstützung! 🚀

# TestSprite MCP Server Schnellstart auf Deutsch

_Inoffizielle deutsche Uebersetzung und Zusammenfassung der zentralen TestSprite-Docs, recherchiert am 2026-04-22. Quellen: [Introduction](https://docs.testsprite.com/mcp/getting-started/introduction), [Overview](https://docs.testsprite.com/mcp/getting-started/overview), [Installation](https://docs.testsprite.com/mcp/getting-started/installation), [First Test](https://docs.testsprite.com/mcp/getting-started/first-test), [API Keys](https://docs.testsprite.com/web-portal/admin/api-keys)._

## Einfuehrung

TestSprite beschreibt sich als ein KI-Testagent fuer vollautomatisiertes Software-Testing. Das Produkt soll Testzyklen ohne manuelles QA-Setup in etwa **10 bis 20 Minuten** abschliessen. Der **TestSprite MCP Server** verbindet dabei den KI-Assistenten in deiner IDE mit der TestSprite-Testengine, damit du Testplanung, Ausfuehrung, Auswertung und Fehlerbehebung direkt aus dem Editor heraus anstossen kannst.

Der Kerngedanke ist einfach: Statt selbst Testfaelle zu schreiben, Frameworks aufzusetzen und Fehlersuchen manuell zu koordinieren, gibst du der IDE einen natuerlich formulierten Prompt. TestSprite uebernimmt dann die Analyse des Projekts, die Testfallgenerierung, die Cloud-Ausfuehrung und die Rueckgabe strukturierter Reports.

## Was der TestSprite MCP Server macht

Laut Dokumentation ist TestSprite MCP Server eine Integration fuer IDE-Assistenten wie Cursor oder Windsurf. Die Plattform soll komplette Test-Workflows automatisieren und in die bestehende Entwicklungsumgebung einbetten.

Die in den Docs gezeigte Standardaufforderung lautet:

```
Help me test this project with TestSprite.
```

Alternativ wird an anderer Stelle auch dieser Prompt verwendet:

```
Can you test this project with TestSprite?
```

Nach dem Start fuehrt TestSprite den Nutzer durch den Rest des Workflows. Die versprochenen Hauptvorteile sind:

- **Fuer Entwickler:** keine manuelle Testfall-Erstellung, schnelleres Feedback, weniger Kontextwechsel und KI-gestuetzte Analyse von Fehlern.
- **Fuer Teams:** vorhersehbarere Qualitaet, breitere Testabdeckung, schnellere Releases und weniger manueller QA-Aufwand.

Im Vergleich zu klassischem Testing betont TestSprite vor allem diese Unterschiede:

- Testfaelle werden **automatisch von KI erzeugt** statt manuell geschrieben.
- Das Setup soll **nahezu ohne Konfiguration** funktionieren.
- Fehler sollen nicht nur erkannt, sondern auch analysiert und fuer automatische Fixes vorbereitet werden.
- Tests laufen nicht isoliert ausserhalb des Entwicklungsflusses, sondern direkt im Coding-Workflow.
- Die Plattform verspricht **umfassendere Edge-Case-Abdeckung** als traditionelle, begrenzt gepflegte Test-Suites.

## Unterstuetzte Testarten

Die Dokumentation beschreibt TestSprite als Loesung fuer Frontend- und Backend-Testing. Dazu gehoeren unter anderem:

### Frontend / Business-Flow-E2E

- Navigation durch User Journeys
- Formulare, Flows und Validierung
- visuelle Zustaende und Layouts
- interaktive Komponenten und zustandsbehaftete UI
- Authentifizierung und Autorisierungs-Flows
- Fehlerbehandlung in der Benutzeroberflaeche

### Backend / API / Integration

- funktionale API-Workflows
- Contract- und Schema-Validierung
- Fehlerbehandlung und Resilienz
- Autorisierung und Authentifizierung
- Boundary- und Edge-Case-Tests
- Datenintegritaet und Persistenz
- Security-Testing

## Voraussetzungen fuer die Installation

Bevor du den MCP Server installierst, nennt TestSprite drei Grundvoraussetzungen:

1. kompatible IDE oder MCP-faehiger Client
2. ein TestSprite-Konto
3. **Node.js >= 22**

Die Dokumentation verlinkt fuer die Kontoerstellung direkt auf den kostenlosen Sign-up bei TestSprite.

## API Key beschaffen

Vor jeder Installation brauchst du einen API Key. Die Dokumentation beschreibt dafuer diesen Ablauf:

1. im **TestSprite Dashboard** anmelden
2. zu **API Keys** unter den Einstellungen navigieren
3. auf **"New API Key"** klicken
4. den erzeugten Schluessel kopieren

Im Admin-Bereich der Web-Portal-Dokumentation wird ausserdem erklaert, wie API Keys verwaltet werden. Dort sieht man pro Key unter anderem:

- **Key Name** - beschreibender Bezeichner
- **Key Value** - teilweise maskierter Wert, z. B. `sk_test_****...****abcd`
- **Created Date** - Erstellungsdatum
- **Last Used** - letzte Verwendung

Zusaetzliche Aktionen im Portal:

- **View Details** - Nutzungsstatistiken ansehen
- **Revoke** - den Key sofort deaktivieren
- **Delete** - den Key dauerhaft loeschen

## Installation in verschiedenen Clients

Die Docs zeigen mehrere Installationswege.

### Trae

1. API Key holen.
2. In Trae zu `AI Sidebar > AI Management` gehen.
3. `MCP > Add > Add from Marketplace` waehlen.
4. Nach **TestSprite** suchen und den Eintrag hinzufuegen.
5. API Key eintragen und bestaetigen.
6. **Builder with MCP** waehlen und Tests starten.

### Cursor

TestSprite beschreibt zwei Wege: One-Click-Installation oder manuelle Konfiguration. Fuer die manuelle Variante wird diese Konfiguration angegeben:

```json
{
  "mcpServers": {
    "TestSprite": {
      "command": "npx",
      "args": ["@testsprite/testsprite-mcp@latest"],
      "env": {
        "API_KEY": "your-api-key"
      }
    }
  }
}
```

Danach soll ein gruener Punkt am MCP-Server-Symbol anzeigen, dass die Tools erfolgreich geladen wurden.

Die Dokumentation weist ausserdem auf eine wichtige Cursor-Einstellung hin: Wenn Cursor MCP-Tools standardmaessig im Sandbox-Modus startet, koennen TestSprite-Prozeduren fehlschlagen. Deshalb soll unter `Chat -> Auto-Run -> Auto-Run Mode` entweder **"Ask Everytime"** oder **"Run Everything"** aktiviert werden.

### Claude Code

Fuer Claude Code zeigt TestSprite diesen Installationsbefehl:

```
claude mcp add TestSprite --env API_KEY=your_api_key -- npx @testsprite/testsprite-mcp@latest
```

Danach kann die Installation mit folgendem Kommando geprueft werden:

```
claude mcp list
```

Erwartete Ausgabe:

```
TestSprite: npx @testsprite/testsprite-mcp@latest - ✓ Connected
```

### VS Code

Fuer VS Code wird die MCP-Server-Konfiguration ueber die Command Palette beschrieben. Die relevante Beispielkonfiguration lautet:

```json
{
  "servers": {
    "testsprite": {
      "command": "npx",
      "args": ["-y", "@testsprite/testsprite-mcp@latest"],
      "env": {
        "API_KEY": "your-api-key"
      }
    }
  },
}
```

Anschliessend soll man im `mcp.json`-Eintrag auf **start** klicken. Wenn der Server ohne Fehler startet und die Tools geladen werden, gilt die Installation als erfolgreich.

### Andere IDEs

Fuer sonstige MCP-faehige Clients wird erneut eine einfache `mcpServers`-Konfiguration mit `npx @testsprite/testsprite-mcp@latest` und dem `API_KEY` gezeigt.

## Installation verifizieren

Die Erfolgskriterien werden in den Docs klar benannt:

- der KI-Assistent sieht die **TestSprite MCP tools**
- es gibt keine **"command not found"**-Fehler
- die Umgebung ist bereit, Projekte zu testen

Als schneller Funktionstest wird wieder dieser Prompt empfohlen:

```
Help me test this project with TestSprite.
```

Wenn der Assistent daraufhin anbietet, TestSprite-MCP-Tools zu verwenden, ist die Anbindung laut Dokumentation korrekt eingerichtet.

## Ersten Test ausfuehren

Die Seite **First Test** beschreibt einen kompletten Erstlauf.

### Schritt 1: Projekt vorbereiten

Die Anwendung soll lokal laufen. Die Docs zeigen als Beispiele:

```
# For frontend applications (examples)
npm run dev          # Usually runs on port 3000, 5173, or 8080
 
# For backend applications (examples)
node index.js        # Usually runs on port 8000, 3001, or 4000
```

Beispiel fuer die Projektstruktur:

```
my-project/
├── frontend/          # React, Vue, Angular, etc.
│   ├── src/
│   ├── package.json
│   └── ...
├── backend/           # Node.js, Python, etc.
│   ├── app.py
│   ├── requirements.txt
│   └── ...
├── README.md
└── package.json
```

### Schritt 2: Magic Command

In der IDE oeffnet man ein neues Chatfenster und sendet:

```
Can you test this project with TestSprite?
```

Optional kann man den Projektordner in den Chat ziehen, wenn nur ein bestimmtes Teilprojekt getestet werden soll.

### Schritt 3: Pflichtkonfiguration

Wenn das Bootstrap-Tool startet, muessen laut Dokumentation mehrere Angaben gemacht werden:

1. **Testing Type**
   - **Frontend** fuer UI und User Flows
   - **Backend** fuer APIs, Services oder Serverlogik

2. **Scope**
   - **Codebase** fuer einen kompletten Testlauf ueber das gesamte Projekt
   - **Code Diff** fuer einen schnelleren Lauf nur ueber aktuelle Aenderungen

3. **Test Account Credentials**, falls die Anwendung Login braucht

Beispiel:

```
  Username: test@example.com
  Password: your-test-password
```

Die Dokumentation nennt diese Authentifizierungstypen:

- **Basic** - Benutzername und Passwort
- **Bearer** - tokenbasierte Authentifizierung
- **API-key** - Zugriff per API-Schluessel
- **None** - keine Authentifizierung noetig

4. **Application URLs**

```
Frontend: http://localhost:5173
Backend: http://localhost:4000
```

5. **Product Requirements Document**

Ein vorhandenes PRD soll hochgeladen werden. Laut Docs reicht auch ein unfertiger oder schwacher Entwurf, weil TestSprite daraus ein normalisiertes PRD erzeugt.

### Schritt 4: Automatisierter Workflow

Nach der Konfiguration uebernimmt der KI-Assistent den gesamten Prozess: Projektverstaendnis, Testplanung, Testausfuehrung und Auswertung. Die Dokumentation verweist fuer Details auf den umfassenderen Workflow-Bereich.

### Schritt 5: Ergebnisse pruefen

Nach dem Lauf sollen unter anderem diese Dateien im Projekt erscheinen:

```
testsprite_tests/
├── tmp/
│   ├── prd_files/                 # Uploaded PRD files
│   ├── config.json               # Test configuration
│   ├── code_summary.json         # Code analysis
│   ├── report_prompt.json        # AI analysis data
│   └── test_results.json         # Detailed test results
├── standard_prd.json             # Normalized PRD
├── TestSprite_MCP_Test_Report.md # Human-readable report
├── TestSprite_MCP_Test_Report.html # HTML report
├── TC001_Login_Success_with_Valid_Credentials.py
├── TC002_Login_Failure_with_Invalid_Credentials.py
└── ...                           # Additional test files
```

Die Reports sollen Gesamt-Coverage, Pass-Rate, fehlgeschlagene Tests inklusive Ursachenanalyse sowie Kategorien wie Funktionalitaet, UI/UX, Security und Performance sichtbar machen.

### Schritt 6: Automatische Bugfixes

Fuer die Korrektur fehlgeschlagener Tests nennt die Dokumentation diesen Prompt:

```
Please fix the codebase based on TestSprite testing results.
```

Daraufhin soll die KI:

- fehlschlagende Tests analysieren
- problematische Codebereiche finden
- gezielte Fixes anwenden
- Tests erneut ausfuehren
- den Prozess iterativ wiederholen, bis Probleme geloest sind

## Ergebnisse im Web Portal ansehen

Wenn Tests ueber MCP in der IDE gestartet wurden, lassen sich die Resultate laut Dokumentation im Web Portal unter **TESTING > MCP Tests** ansehen. Dort zeigt TestSprite unter anderem:

- **Test Name** - Beschreibung des ausgefuehrten Tests
- **Execution Time** - Zeitpunkt der Ausfuehrung
- **Duration** - Laufzeit
- **Status** - Passed, Failed oder In Progress
- **Test Type** - Frontend, Backend oder Mixed

Ein Klick auf ein Ergebnis soll detailierte Ausfuehrungslogs, einzelne Testfall-Resultate, Fehlermeldungen, Debugging-Informationen und Performance-Metriken oeffnen.

## Kurzfazit

Die TestSprite-Dokumentation positioniert den MCP Server als sehr niedrigschwelligen Einstieg in automatisiertes Testing mit KI-Unterstuetzung. Besonders klar beschrieben sind die Installationspfade fuer gaengige IDEs, die Rolle des API Keys und der erste End-to-End-Testlauf. Fuer deutschsprachige Entwickler ist der wichtigste praktische Ablauf:

1. Konto anlegen und API Key erzeugen
2. MCP-Server in der bevorzugten IDE konfigurieren
3. lokale App starten
4. den TestSprite-Prompt im IDE-Chat ausfuehren
5. Konfiguration, URLs und PRD angeben
6. Reports und automatische Fix-Vorschlaege pruefen

Damit liegt eine gut nachvollziehbare Grundlage vor, um TestSprite ohne manuelle Test-Suite-Erstellung in einen bestehenden Entwicklungsworkflow einzubauen.

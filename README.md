# 🇩🇪 DEUTSCHE VERSION

# py_telegramDiceBot

## 1. Projektübersicht

**py_telegramDiceBot** ist ein Python-basierter Telegram-Bot für Pen-and-Paper-Rollenspiele mit einer intuitiven Benutzeroberfläche. Der Bot ermöglicht es Spielern, verschiedene Würfel-Typen zu werfen und zufällige Ergebnisse für Spielmechaniken zu erhalten.

Projektinformationen

    Repository: CodefrogCF/py_telegramDiceBot
    Programmiersprache: Python 100%
    Lizenz: Keine (keine Lizenz spezifiziert)
    Status: Aktiv / In Entwicklung
    Erstellungsdatum: 10. April 2025
    Sichtbarkeit: Öffentlich

## 2. Funktionalität

Der Bot bietet folgende Würfelwurf-Funktionen:
Funktion 	Beschreibung 	Bereich
D3 	Würfelt einen 3-seitigen Würfel 	1-3
D6 	Würfelt einen 6-seitigen Würfel 	1-6
D20 	Würfelt einen 20-seitigen Würfel 	1-20
3xD20 	Würfelt drei 20-seitige Würfel gleichzeitig 	3x(1-20)
Bodypart 	Bestimmt zufällig eine Körperstelle 	Kopf, Torso, Arm, Bein

## 3. Architektur

### 3.1 Hauptkomponenten

main.py (4024 Bytes)
  -Logging-Modul
  -Telegram Bot Application
  -Message Handler
  -Command Handler

### 3.2 Kernmodule

**Verwendete Bibliotheken:**
- `telegram`: Telegram Bot API-Wrapper
- `telegram.ext`: Extension-Framework für Bots (Application, Handler, Filter)
- `logging`: Logging und Debugging
- `random`: Pseudozufallsgenerator

## 4. Installation und Setup

### 4.1 Voraussetzungen
- Python 3.7 oder höher
- pip (Python Package Manager)
- Telegram Bot Token (von @BotFather)

### 4.2 Installationsschritte

**1. Repository klonen**
git clone https://github.com/CodefrogCF/py_telegramDiceBot.git
cd py_telegramDiceBot

**2. Dependencies installieren**
pip install -r requirements.txt

**3. Bot Token konfigurieren**
Öffne main.py und ersetze "<YOUR TOKEN>" mit deinem Bot Token:
application = Application.builder().token("<DEIN TOKEN HIER>").build()

**4. Bot starten**
python main.py

## 5. Benutzeroberfläche

### 5.1 Tastatur-Layout

Der Bot präsentiert eine persistent sichtbare Reply-Keyboard mit folgenden Schaltflächen:

──────────────────────────────────────────
  [D3]  [D6]  [D20]  [3xD20]  [Bodypart]  
──────────────────────────────────────────

### 5.2 Interaktionsmöglichkeiten

Über Buttons:

    Benutzer tippen auf die gewünschte Schaltfläche
    Sofortige Wurfelergebnis-Anzeige

Über Befehle:

    /start - Zeigt Willkommensnachricht und Tastatur an
    /d3 - Würfelt D3
    /d6 - Würfelt D6
    /d20 - Würfelt D20
    /d3x20 - Würfelt 3x D20
    /bodypart - Wählt Körperstelle
    /stop - Beendet die Konversation

## 6. Technische Dokumentation

### 6.1 Funktionsablauf

**Initialisierung**
start() → Zeigt Keyboard an

**Benutzerinteraktion**
echo() → Erkennt Eingabe → Ruft entsprechende Würfelfunktion auf

**Würfeln**
random_X() → Generiert Zufallszahl → Formatiert HTML-Ausgabe → Sendet an User

**Beendigung**
cancel() → Entfernt Keyboard → Beendet Konversation

### 6.2 Wichtige Funktionen

start(update, context)

    Initialisiert den Bot und zeigt die Tastatur
    one_time_keyboard=False: Tastatur bleibt sichtbar
    resize_keyboard=True: Responsive Tastaturgröße

random_X(update, context) (D3, D6, D20, 3xD20)

    Generiert Zufallszahlen mit random.randint()
    Formatiert Ausgabe mit HTML-Tags für Fettdruck
    Sendet Ergebnis als Text-Nachricht

random_bodypart(update, context)

    Generiert Zahlen 1-4
    Konvertiert zu Körperteilen (Kopf, Torso, Arm, Bein)

echo(update, context)

    Message Handler für Text-Eingaben
    Erkennt Button-Presses und leitet weiter
    Nur für TEXT und KEINE COMMAND-Nachrichten

### 6.3 Handler-System

CommandHandler("/start", start)          # Befehl-Handler
CommandHandler("/d3", random_3)          # Spezifische Befehle
MessageHandler(filters.TEXT, echo)       # Text-Nachrichten

## 7. Logging

Der Bot implementiert strukturiertes Logging:

logging.basicConfig(
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    level=logging.INFO
)

Ausgabe-Format:

TIMESTAMP - MODULNAME - LEVEL - NACHRICHT
2025-04-10 15:20:45 - main - INFO - Bot gestartet

## 8. Dateien und Struktur

Datei	Größe	Typ	Beschreibung
main.py	4 KB	Python	Hauptanwendung mit alle Funktionen
requirements.txt	-	Text	Python-Abhängigkeiten
.gitignore	7 Bytes	Konfiguration	Git-Ausschlussregeln

## 9. Konfiguration und Anpassung

### 9.1 Bot Token

Ersetze in main.py Zeile 84:

application = Application.builder().token("<DEIN_TOKEN_HIER>").build()

### 9.2 Tastatur anpassen

Buttons können in der start() Funktion modifiziert werden:
Python

reply_keyboard = [['D3', 'D6', 'D20', '3xD20', 'Bodypart']]

### 9.3 Würfel erweitern

Neue Würfelfunktion hinzufügen:

async def random_12(update: Update, context) -> None:
    dice = random.randint(1, 12)
    await update.message.reply_text(f"<b>You rolled a:\n {dice}</b>", parse_mode='HTML')

#In main():
application.add_handler(CommandHandler("d12", random_12))

## 10. Problembehebung

Problem	Ursache	Lösung
Bot antwortet nicht	Ungültiger Token	Token in main.py überprüfen
ModuleNotFoundError	Fehlende Abhängigkeiten	pip install -r requirements.txt ausführen
Tastatur wird nicht angezeigt	Handler nicht registriert	Ensure Handler in main() hinzugefügt



# 🇬🇧 ENGLISH VERSION

# py_telegramDiceBot

## 1. Project Overview

**py_telegramDiceBot** is a Python-based Telegram bot for pen & paper tabletop role-playing games featuring an intuitive user interface. The bot enables players to roll various types of dice and generate random results for game mechanics.

### Project Information
- **Repository:** CodefrogCF/py_telegramDiceBot
- **Programming Language:** Python 100%
- **License:** None (no license specified)
- **Status:** Active / In Development
- **Created:** April 10, 2025
- **Visibility:** Public

## 2. Features and Functionality

The bot provides the following dice-rolling functions:

| Function | Description | Range |
|----------|-------------|-------|
| **D3** | Rolls a 3-sided die | 1-3 |
| **D6** | Rolls a 6-sided die | 1-6 |
| **D20** | Rolls a 20-sided die | 1-20 |
| **3xD20** | Rolls three 20-sided dice simultaneously | 3x(1-20) |
| **Bodypart** | Randomly determines a body part | Head, Body, Arm, Leg |


## 3. Architecture

### 3.1 Main Components

main.py (4024 Bytes)
 ├── Logging Module
 ├── Telegram Bot Application
 ├── Message Handler
 └── Command Handler

### 3.2 Core Dependencies

**Required Libraries:**
- `telegram`: Telegram Bot API wrapper
- `telegram.ext`: Extension framework for bots (Application, Handler, Filter)
- `logging`: Logging and debugging
- `random`: Pseudorandom number generator

## 4. Installation and Setup

### 4.1 Prerequisites
- Python 3.7 or higher
- pip (Python Package Manager)
- Telegram Bot Token (from @BotFather)

### 4.2 Installation Steps

**1. Clone the repository**
git clone https://github.com/CodefrogCF/py_telegramDiceBot.git
cd py_telegramDiceBot

**2. Install dependencies**
pip install -r requirements.txt

**3. Configure bot token**
Open main.py and replace "<YOUR TOKEN>" with your bot token:
application = Application.builder().token("<YOUR TOKEN HERE>").build()

**4. Start the bot**
python main.py

## 5. User Interface

### 5.1 Keyboard Layout

The bot presents a persistent reply keyboard with the following buttons:
Code

┌──────────────────────────────────────────┐
│  [D3]  [D6]  [D20]  [3xD20]  [Bodypart]  │
└──────────────────────────────────────────┘

### 5.2 Interaction Methods

Via Buttons:

    Users tap on the desired button
    Instant dice result display

Via Commands:

    /start - Shows welcome message and keyboard
    /d3 - Rolls D3
    /d6 - Rolls D6
    /d20 - Rolls D20
    /d3x20 - Rolls 3x D20
    /bodypart - Selects random body part
    /stop - Ends the conversation

## 6. Technical Documentation

### 6.1 Function Flow

**Initialization**
start() → Displays keyboard

**User Interaction**
echo() → Recognizes input → Calls corresponding dice function

**Dice Roll**
random_X() → Generates random number → Formats HTML output → Sends to user

**Termination**
cancel() → Removes keyboard → Ends conversation

### 6.2 Key Functions

start(update, context)

    Initializes the bot and displays the keyboard
    one_time_keyboard=False: Keyboard remains visible
    resize_keyboard=True: Responsive keyboard sizing

random_X(update, context) (D3, D6, D20, 3xD20)

    Generates random numbers using random.randint()
    Formats output with HTML tags for bold text
    Sends result as text message

random_bodypart(update, context)

    Generates numbers 1-4
    Converts to body parts (Head, Body, Arm, Leg)

echo(update, context)

    Message handler for text input
    Recognizes button presses and routes accordingly
    Only processes TEXT messages and NOT COMMAND messages

### 6.3 Handler System

CommandHandler("/start", start)          # Command handler
CommandHandler("/d3", random_3)          # Specific commands
MessageHandler(filters.TEXT, echo)       # Text messages

## 7. Logging

The bot implements structured logging:

logging.basicConfig(
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    level=logging.INFO
)

Output Format:

TIMESTAMP - MODULE_NAME - LEVEL - MESSAGE
2025-04-10 15:20:45 - main - INFO - Bot started

## 8. File Structure

File	Size	Type	Description
main.py	4 KB	Python	Main application with all functions
requirements.txt	-	Text	Python dependencies
.gitignore	7 Bytes	Configuration	Git exclusion rules

## 9. Configuration and Customization

### 9.1 Bot Token

Replace in main.py line 84:

application = Application.builder().token("<YOUR_TOKEN_HERE>").build()

### 9.2 Customize Keyboard

Buttons can be modified in the start() function:

reply_keyboard = [['D3', 'D6', 'D20', '3xD20', 'Bodypart']]

### 9.3 Add New Dice Type

To add a new dice function:

async def random_12(update: Update, context) -> None:
    dice = random.randint(1, 12)
    await update.message.reply_text(f"<b>You rolled a:\n {dice}</b>", parse_mode='HTML')

#In main():
application.add_handler(CommandHandler("d12", random_12))

## 10. Troubleshooting

Issue	Cause	Solution
Bot doesn't respond	Invalid token	Verify token in main.py
ModuleNotFoundError	Missing dependencies	Run pip install -r requirements.txt
Keyboard not displayed	Handler not registered	Ensure handler is added in main()


    Repository: https://github.com/CodefrogCF/py_telegramDiceBot
    Author: CodefrogCF
    Issue Tracker: Available in the repository

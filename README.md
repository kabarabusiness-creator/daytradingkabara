# Day Trader Dashboard

Ein lokales Dashboard für die 11 Day-Trader-Skills (`trader-*`). Alles an einem Ort: Scanner, News, Einstieg, Stop und Ziel, Time Machine, Positionsgröße, Risiko-Check, Ticket, Alerts, Earnings-Analyst und Kongress-Trades.

Nur Python 3.8+ nötig, nichts zu installieren.

## Start

```
python3 server.py --demo     # erst ausprobieren: offline, Beispieldaten vom 19.10.2026 (TSLA)
python3 server.py            # live: echte Daten von Yahoo, SEC, Nasdaq Trader, House Clerk
```

Der Browser öffnet sich auf `http://127.0.0.1:8765/`. Windows: `start.bat` (live) oder `start-demo.bat`. Mac/Linux: `./start.sh` bzw. `./start.sh --demo`.

## Ablauf an einem Handelstag

1. **Scanner & News → „Aktienliste laden“** (einmal pro Tag), dann **Scan starten**. Vor Börsenstart „Täglich“, nach 09:45 New York „Opening-Range-Ausbruch“.
2. Treffer anklicken (**Trade**) oder oben im Trade-Tab eine Aktie eintragen und **Ganze Kette starten**. Die Kette macht: Einstieg prüfen → Stop & Ziel → Time Machine → Positionsgröße → Risiko-Check → Ticket. Sie stoppt, wenn der Einstieg noch nicht ausgelöst hat.
3. **Alerts → „Aus Plan“** legt Stop, Ziel und „raus bis 15:55“ als Alarme an. Mit „automatisch alle 60 s“ prüft das Dashboard laufend (Tab offen lassen).
4. **Bestellen geht nur im Claude-Chat:** `/trader-broker` aufrufen, das Ticket mit „yes“ bestätigen, in Claudes Allow-Karte freigeben.

Die NYSE handelt 09:30–16:00 New York, das ist meist 15:30–22:00 deutscher Zeit.

## Was das Dashboard bewusst nicht tut

- **Keine Orders senden, kein „Ja“ speichern.** Das bleibt im Chat, damit du jede Order einzeln bestätigst.
- **Sicherheitsschalter** (`paper`, `allow_options`, `allow_margin`, `allow_short`, `pdt_guard`) werden nur angezeigt. Ändern nur von Hand in `workspace/trader/config.json`.
- **Nur auf `127.0.0.1`** erreichbar, nur eine feste Liste von Aktionen mit geprüften Parametern, keine Shell.

## Einstellungen

Im Tab „Einstellungen“: Budget, Max. Verlust pro Trade, Tagesverlust-Limit, Trades pro Tag, Einstiegsfenster, gesperrte Aktien. Für News und Analyst verlangt die SEC einen Namen und eine E-Mail im Feld **SEC-User-Agent** (`Dein Name deine@mail.de`).

## Dateien

```
server.py        Server (Whitelist der Skill-Aufrufe)
index.html       Oberfläche
skills/          die 11 Skills (Code von github.com/Jakeschincariol/day-trader-skill, MIT)
demo/            Beispieldaten für --demo
workspace/       deine Daten (trader/*.json), entsteht beim ersten Start
workspace-demo/  Daten des Demo-Modus
```

## Hinweise

- Keine Anlageberatung. Die Daten sind gratis und teils verzögert, ein Stop ist ein Plan und keine Garantie. Die Time Machine ist eine Simulation, keine Prognose. Die meisten Daytrader verlieren Geld.
- „PDFs lesen“ im Pelosi-Tracker braucht `pdftotext` (Poppler).
- Läuft ein Scan über das ganze Universum, dauert das einige Minuten. Mit Symbolliste oder Limit geht es schnell.

## Lizenz und Herkunft

`server.py`, `index.html` und die Start-Skripte sind eine Oberfläche für die Skills aus
[Jakeschincariol/day-trader-skill](https://github.com/Jakeschincariol/day-trader-skill) (MIT, siehe `skills/LICENSE-day-trader-skill`).
Der Skill-Code in `skills/` stammt unverändert von dort.

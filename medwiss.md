# Einführung Digital Humanities Methoden für die Medienwissenschaft

_Auswertung der Top 250 Filme aus der IMDb_ ([Liste](https://www.imdb.com/chart/top?ref_=nv_mv_250))

## Voraussetzungen
* eigener Laptop
* Webbrowser Chrome
* Scraper Chrome Extension [Chrome Web Store](https://chrome.google.com/webstore/detail/scraper/mbigbapnjcgaffohmbkdlecaccepngjd)
* LibreOffice [download](https://de.libreoffice.org/)
* WLAN

## Themen
* __Webscraping__ mit Scraper (15 min)
* Datenaufbereitung mit __RegEx__ (LibreOffice) (30 min)
* Datenanalyse und -visualisierung mit __R__ (im Browser mit https://rnotebook.io) (40 min)
* ggfs. __Markdown__ als Auszeichnungssprache

## Workshop
### Webscraping
1. (https://www.imdb.com/chart/top?ref_=nv_mv_250) aufrufen
1. HTML-Struktur erläutern
1. Scraper starten und Elemente auswählen
1. in Zwischenablage abspeichern

### LibreOffice 1
1. Inhalt aus Zwischenablage einfügen
1. Aufräumen mit RegEx

### RegEx-Intro
__1. tbd__

### LibreOffice 2
Suchen/Ersetzen-Fenster: Erweiterte Optionen: Reguläre Ausdrücke

|Aufgabe|RegEx suchen| ersetzen|
|----|----|----|
|Whitespace am Zeilenanfang löschen| ^\s*| |
|mind. 2 Whitespace durch Tab ersetzen| \s{2,}|\t|
|Tab am Zeilenende löschen| \t$ | |
|Jahreszahlen ohne Klammern darstellen|\\((\d{4})\\)|$1|

Vor dem Bereinigen der Jahreszahlen, den Text in Calc einfügen: Tabellenbearbeitungsprogramme (wie Calc/Excel) manipulieren Daten zur Darstellung/Bearbeitung im Hintergrund!

Speichern als txt-Datei: `top250.txt` (ist jetzt im tsv-Format; alternative wäre csv, kann aber mit Textdateien mitunter problematisch sein!)

### R - Einführung
(Kursvorlage: https://rnotebook.io/anon/3d009cdef3980755/tree)

1. Ein R-Jupyter-Notebook öffnen: https://rnotebook.io
1. __Einführung tbd__

### R - Datenauswertung
1. `top250.txt` hochladen
1. Datei als tsv einlesen
1. Daten überprüfen
1. Jahreszahlen als Vektor speichern
1. Jahreszahlen auf Jahrzehnte reduzieren
1. Plotten
1. Tagcloud der Titel?


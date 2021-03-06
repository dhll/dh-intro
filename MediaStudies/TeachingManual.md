# Teaching Manual
# Einführung Digital Humanities Methoden für die Medienwissenschaft

_Auswertung der Top 250 Filme aus der IMDb_ ([Liste](https://www.imdb.com/chart/top?ref_=nv_mv_250))

## Voraussetzungen
* eigener Laptop
* Webbrowser Chrome
* Scraper Chrome Extension [Chrome Web Store](https://chrome.google.com/webstore/detail/scraper/mbigbapnjcgaffohmbkdlecaccepngjd)
* LibreOffice [download](https://de.libreoffice.org/)
* WLAN

## Themen
* HTML-Struktur und __Webscraping__ mit Scraper (15 min)
* Datenaufbereitung mit __RegEx__ (LibreOffice) (30 min)
* Datenanalyse und -visualisierung mit __R__ (im Browser mit https://rnotebook.io) (40 min)
* ggfs. __Markdown__ als Auszeichnungssprache

## Workshop
### Webscraping

> (https://www.imdb.com/chart/top?ref_=nv_mv_250) aufrufen.

Die Liste der beliebtesten Filme aus der IMDb soll ausgewertet werden. Um es nicht zu komplex zu machen, soll die einfache Frage beantwortet werden, aus welchem Jahr die meisten Filme aus der Liste stammen.

Um die Liste der Filme und die zugehörigen Informationen (Jahre, Bewertung, ...) von der Webseite zu bekommen, könnten sie einfach alles markieren und per Copy-Paste übernehmen. Manchmal kann das funktionieren -- oft allerdings nicht, und manchmal sind die Daten auch nicht so sauber in einer Tabelle, wie in diesem Beispiel.

Um an Informationen von Webseiten zu kommen, gibt es eine Technik, die sich __Webscraping__ nennt. Mit Webscraping kann man genau die Informationen einer Webseite "abschürfen", die man haben möchte. Und das funktioniert, weil Webseiten nicht reine Textdokumente sind, sondern die Informationen der Webseite strukturiert sind mit einer sog. Auszeichnungssprache: __HTML__ (Hypertext Markup Language).

Der HTML-Quelltext der IMDb-Seite sieht so aus: `Strg-U` (in Chrome). Das ist etwas verwirrend, aber einige der Grundelemente möchte ich Ihnen erläutern.

### Intro HTML

Um eine Einführung in HTML zu bekommen, ist folgende Seite sehr hilfreich:

> (https://www.w3schools.com/html/html_intro.asp) aufrufen. Zur Illustration am Seitenende scrollen ("HTML Page Structure")

Alles auf einer Webseite steht zwischen Tags, die das Element, das sie umfassen definieren.
Das, was Sie auf einer Webseite sehen, steht zwischen den sog. `<body>-Tags`. Body definiert, dass alles, was dazwischen steht, auf der Webseite (in irgendeiner Form) erscheint.
Vor dem Body steht der `<head>-Tag`. Im Head sind sog. Metadaten enthalten, z.B. der Titel der Webseite (das was Sie in der Kopfzeile des Browsers sehen), aber noch viel mehr.
Ganz am Anfang einer html-Seite wird der Dokumententyp definiert, so dass der Webbrowser weiß, um was für ein Dokument es sich handelt (z.B. html, oder pdf, oder Bild, ...)

> (https://www.w3schools.com/html/html_basic.asp) aufrufen.

Alle Elemente einer Webseite, sind in Tags eingeschlossen, die definieren, um was es sich handelt. Z.B. **Überschriften** in versch. Ebenen, oder **Absätze**, **Links** oder **Bilder**.

> Jeweils Click auf Try it Yourself

Bei Bilder und Links sehen Sie, dass die Tags auch noch _Attribute_ haben (können), z.B. beim Link ist die URL angegeben, die durch Klick aufgerufen wird. Der dargestellte Text steht (wie üblich) zwischen den Tags. Beim `<img>`-Tag sind mehrere Attribute aufgeführt: die Quelle/die Datei; ein Alternativtext, der von Screenreadern gelesen wird oder das Bild in Suchmaschinen finden lässt; sowie die Größenangaben. Im realen Leben sind die Webseiten sehr komplex aufgebaut und die Tags vielfach ineinander geschachtelt. In den Beispielen ist das alles noch sehr übersichtlich.

Einen ersten Eindruck, wie solche Verschatelungen aussehen, gibt die Formatierung von **Tabellen**:

* `<table>`
  * `<tr>` Table row
    * `<th>` Table Heading
    * `<td>` Table data (= Zelle)

Mithilfe der Tags ist es möglich, spezifische Elemente einer Webseite abzufragen, um sie für das Datamining/die Datenanalyse zu nutzen.

Genau das machen wir jetzt mit der Liste aus der IMDb, diese Liste ist als Tabelle strukturiert.

### IMDb-Tabelle

Tabelle und HTML-Code nebeneinander und anhand des ersten Eintrags "Shawshank Redemption" zeigen, von wo bis wo das `<tr>` und `<td>` geht, dass es zahlreiche weitere Informationen gibt, die nicht sichtbar sind.

Mit Scraper jetzt eine komplette `<tr>` markieren und dann per Rechtsklick scrapen.

Oben links sehen stehen die Tags (im XPath-Feld).

Copy to clipboard, wenn alle 250 Einträge erfasst sind.


### LibreOffice 1
>Inhalt aus Zwischenablage einfügen: Das sieht recht unschön aus. Es ist zwar einigermaßen strukturiert, aber es wimmelt von Leerzeichen und Tabulatoren.

Um halb strukturierte Daten aufzuräumen und in eine ordentliche (Tabellen)Struktur zu bringen, helfen **RegEx**

### RegEx-Intro
Reguläre Ausdrücke sind eine Art formalisierter Sprache, die es erlaubt, nach Zeichenmustern zu suchen, also komplexere Suchen-und-Ersetzen-Aktionen durchzuführen. Mit RegEx können Sie auch nach reinen Strukturen suchen, unabhängig von Wörtern.
Den gerade in LibreOffice eingefügten Text säubern wir gleich. Zunächst noch einige Beispiele von RegEx-Ausdrücken.

>Rufen Sie die Datei https://github.com/dhll/dh-intro/blob/master/RegEx-Bspl.txt auf und kopieren den Text in die Zwischenablage.
>Rufen Sie als nächstes die Webseite (https://regex101.com) auf und fügen den Text in das große Fenster (Test String) ein.

Z.B. in einem Text nach einer Zahl 1877 suchen; aber: alle Jahreszahlen der 2. Hälfte des 19. Jhds. zu finden, ist mit herkömmlichen Suchen/Ersetzen schwieriger/aufwändiger (185?, 186?, 187?, 188?, 189?). Vollends komplex wird es, wenn z.B. nur die gerade Jahre gesucht werden. Hier können RegEx helfen, z.B. `18[5-9][02468]`

In größeren Abschlussarbeiten können RegEx benutzt werden, um Text zu korrigieren, z.B. um doppelte Satzzeichen zu finden; in Word müssten sämtliche Kombinationen getestet werden, in RegEx leicht abzufragen: `[[:punct:]]{2,}`

Oder doppelte Leerzeichen/Leerzeichen und Tabulator `\s{2,}`

In den drei kleinen Beispielen haben Sie schon einiges zu RegEx gesehen, das möchte ich noch etwas erläutern. Dazu gibt es noch ein **Handout**, mit gängigen Grundelementen von RegEx.

* Einfache Zeichen (im Bspl `18`)
* Sonderbedeutung und Übersteuerungszeichen
* Metazeichen/Zeichenklassen (im Bspl. `\s`)
* Quantoren (im Bspl `\s{2,}`)

>Aufgabe (2er Gruppen): Suchen Sie alle vierstelligen Zahlen, die am Zeilenanfang stehen.  
>Lsg: `^\d{4}`

>Aufgabe (2er Gruppen): Suchen Sie alle Zeilenenden, die mit einem Punkt enden.  
>Lsg 1: `\.\n` = Newline! D.h. findet letztes Zeilenende nicht! (Da es keine neue Zeile gibt!)  
>Lsg 2: `\.$`= Zeilenende! Findet auch letzte Zeile.

>Warum findet er die Zeile "1891: Der DFCB wird gegründet." nicht?  
>Nach dem Punkt kommt noch ein Leerzeichen. Wie finden Sie alle Zeilen, die mit einem Leerzeichen enden?  
>Lsg 3: `\s§`

* Schließlich gibt es noch weitere Zeichenklassen, die durch eckige Klammern markiert werden (im Bspl `[5-9]` und `[02468]`)
Bei Zeichenklassen gibt es noch zwei Besonderheiten. Je nach Position kann sich die Bedeutung eines Zeichens verändern:
* `-` zwischen mehreren Zeichen bezeichnet einen Bereich; am Anfang einer Klasse ist es literal/wörtlich zu verstehen. Wenn Sie nach dem Zeichen suchen wollen, müssen Sie es an den Anfang einer Klasse setzten.
* Andersherum ist es mit `^`. Wenn es am Anfang steht, negiert es den Inhalt der Klasse, wenn Sie nach dem Zeichen suchen wollen, müssen Sie es an andere Stelle einfügen.
* I.d.R. sind RegEx Case sensitive. Es gibt einen Unterschied zw. Groß- und Kleinschreibung. [a-z] ist ein anderer Bereich als [A-Z]. I.d.R. fehlen bei diesen Bereichsangaben zudem deutsche "Sonderzeichen" (ß, ä, ö, ü). Die sind mit drin, wenn Sie [a-ü] eingeben.
Es gibt zudem noch bes. Zeichenklassen, z.B. hatten wir anfangs alle Interpunktionszeichen gesucht mit `[[:punct:]]`.

>Aufgabe (2er Gruppen): Zurück zur obigen Frage: Wie finden Sie alle Zeilen, die nicht mit einem Satzzeichen abschließen?  
>Lsg 4: `[^[:punct:]]$`

### LibreOffice 2

Jetzt haben Sie einen ersten kurzen Einblick in Reguläre Ausdrücke und können sicherlich die Tabelle der 250 beliebtesten Filme in Libre Office selber bereinigen.

In LibreOffice finden Sie die Suchen-Ersetzen-Funktion über das Icon bzw. Menüs. Wählen Sie unter erweiterte Optionen "Reguläre Ausdrücke" aus.

**Aufgabe (2er Gruppen):**

>1. Löschen Sie den Whitespace am Zeilenanfang  
>2. Ersetzen Sie alle mehrfachen (! nicht die einfachen Leerzeichen in den Titelfeldern) Leerzeichen und Tabs durch einen einfachen Tab  
>1. Löschen Sie die Tabs am Zeilenende  
>1. Kopieren Sie den Text und fügen ihn in die Tabellenkalkulation ein (via `Bearbeiten/Inhalte Einfügen/Unformatierter Text`)

Die Tabs werden als Spaltentrenner interpretiert und die Tabelle als Tabelle dargestellt. Fällt Ihnen etwas auf?

Tabellenkalkulationsprogramme versuchen z.T. (v.a.) Zahlenformate zu interpretieren und wandeln sie im Hintergrund um. Hier z.B. die Jahreszahlen. Excel & Co sind tolle Programme, die viel Arbeit abnehmen können, aber sie machen manchmal Sachen, die man nicht will, die man z.T. auch nicht sieht. Und dann können am Ende die Daten verfälscht sein. Deshalb sollten Sie wenn es um Datenanalyse geht, möglichst nicht mit Tabellenkalkulationsprogrammen arbeiten.

Zur weiteren Analyse verwenden wir deshalb ein anderes Programm, genauer: eine Programmiersprache, die v.a. für statistische und Datenanalyse entwickelt wurde, in den letzten Jahren aber zu einer der Standardsprachen für digitale Geisteswissenschaften geworden ist: R.

>Aufgabe (2er Gruppen): Aber zuvor noch eine kleine Bereinigung in LibreOffice: Gehen Sie zurück in das Textdokument und versuchen Sie, die Jahreszahlen ohne Klammern darzustellen. Das ist ziemlich tricky!

|Aufgabe|RegEx suchen| ersetzen|
|----|----|----|
|Whitespace am Zeilenanfang löschen| ^\s*| |
|mind. 2 Whitespace durch Tab ersetzen| \s{2,}|\t|
|Tab am Zeilenende löschen| \t$ | |
|Jahreszahlen ohne Klammern darstellen|\\((\d{4})\\)|$1|

>Löschen Sie als letztes noch die erste Zeile (die Spaltenüberschriften).

Speichern als txt-Datei: `top250.txt` (ist jetzt im tsv-Format; alternative wäre csv, kann aber mit Textdateien mitunter problematisch sein!)

### R - Einführung

1. Ein R-Jupyter-Notebook öffnen: https://rnotebook.io

Das ist ein sog. "Jupyter-Notebook", das das Schreiben von Text, Schreiben von Auswertungs-Code, Ausführen des Codes und die graphische Darstellung der Analysen in einem Dokument ermöglicht.

Die einzelnen Elemente (Text- und Code-Blöcke) sind in "Zellen" organisiert, die einzeln ausgeführt werden können.

Wenn Sie Umschalt-Enter drücken, wird die aktuelle Zelle ausgeführt und eine neue Zelle eingefügt.

## R als Taschenrechner


```R
10+5
```


```R
10-5
```


```R
10*5
```


```R
10/5
```

## R als besserer Taschenrechner


```R
10* pi # In R gibt es vorgespeicherte Werte
```


```R
sqrt(12) # In R gibt es built-in functions
```


```R
abs(-23)
```


```R
round(pi)
```


```R
#eine ähnliche Funktion wie round:
trunc(pi)
```

>Wo könnte der Unterschied liegen?

Funktionen können miteinander kombiniert und geschachtelt werden. Die Ausführung erfolgt von innen nach außen


```R
round(sqrt(12))
```

Viele Funktionen erlauben/erfordern zusätzliche Parameter, hier Anzahl der Nachkommastellen


```R
round(sqrt(12),2)
```

## Vergleiche durchführen


```R
5>6
```


```R
pi <= sqrt(12)
```


```R
2*5 == 10
```


```R
2*5 != 10
```

## Werte zuweisen

Aus Mathe ist der "Zuweisungsoperator" ("assignement operator") "=" bekannt: x = 6

In R ist der Zuweisungsoperator "<-"


```R
x <- 10
```


```R
x # Dann kann die Variable "x" einfach aufgerufen werden, und der Wert wird ausgegeben.
```


```R
print(x) # Oder man kann die Variable "ausdrucken" lassen mit dem Print-Befehl.
```


```R
x- 7 # mit Variablen kann man rechnen
```


```R
x <- x - 5 # Variablen können mit sich selber rechnen (und verändern)
```


```R
x
```


```R
y <- "Hallo Welt!" #Variablen können auch Wörter und Sätze sein (Anführungszeichen!)
```


```R
print(y)


# R - Analyse der Filmdaten

## Einlesen der Datei (Tabelle)


```R
top250.t <- read.delim("top250.txt", sep="\t", header=FALSE)
```
Hier rufen Sie eine Funktion auf (read.delim), geben ihr als Argumente den Namen der Datei (in Anführungszeichen!), die Art, wie die Felder der Tabelle getrennt sind (als RegEx: Tabulator-getrennt), und dass es keine Spaltenüberschriften gibt).
Schließlich weisen Sie die Tabelle der Variablen "top250.t" zu.

Wenn Sie eine Datei eingelesen haben, sollten Sie als erstes überprüfen, ob die Datei korrekt eingelesen wurde.

Wurden alle Zeilen eingelesen? Dazu gibt es die Funktion `nrow` (Number of rows):
```R
nrow(top250.t)
```

Sind die Tabellenzellen richtig getrennt? Lassen Sie sich die ersten/letzten 6 Einträge der Tabelle anzeigen:

```R
head(top250.t)
tail(top250.t)
```


```R
?head 
# mit ? vor einer Funktion, wird die Hilfefunktion aufgerufen. 
# (Manchmal ist der Hilfetext hilfreich, oftmals ist Google besser)
```

>Aufgabe 1: lassen Sie sich die ersten 10 Zeilen der Tabelle anzeigen.  
>Aufgabe 2: lassen Sie sich die letzten 10 Zeilen der Tabelle anzeigen.


```R
tail(top250.t, n=10)
```


```R
head(top250.t, n=10)
```

## Tabelle bearbeiten

### überflüssige Spalten entfernen

```R
# einzelne Zeilen anzeigen lassen
top250.t[4,]
```


```R
# einzelne Zelle anzeigen lassen
top250.t[20,2]
```

```R
# einzelne Spalte anzeigen lassen
top250.t[,3]
```

```R
# um mehrere Zeilen auszuwählen, wird der Bereich angegeben
top250.t[1:4,]
```

```R
# um mehrere Spalten auszuwählen, wird der Bereich angegeben
top250.t[,2:3]
```

Um Spalten zu löschen, können die gewünschten Spaltennummern ausgewählt werden, die erhalten bleiben sollen und mit dem gleichen Variablen-Namen gespeichert werden.

>Aufgabe: erstellen Sie eine neue Tabelle (mit dem gleichen Tabellen-Namen top250.t), der nur die Spalten 1-4 enthält.  
Zur Überprüfung, lassen Sie sich die Zeilen 6-9 der neuen Tabelle anzeigen.


```R
top250.t <- top250.t[,1:4]
```


```R
top250.t[6:9,]
```

### Spaltennamen hinzufügen

```R
colnames(top250.t) <- c("Rang", "Titel", "Jahr", "Bewertung")
```

>Aufgabe: Überprüfen Sie, ob die Tabelle jetzt Spaltennamen hat (ohne sich die ganze Tabelle anzeigen zu lassen.)

```R
head(top250.t)
```

## Visualisieren

```R
plot(top250.t$Jahr)
```


Verteilung zeigt, dass zwar mehr Filme ab ca. den 90ern in den Top 250 sind als ältere Filme, dass es aber keinen Zusammenhang zwischen Alter des Filmes und der Beliebtheit gibt. 

### Filme nach Jahrzehnten gruppieren


```R
Tabelle <- table(top250.t$Jahr) #table-Funktion summiert nach gleichen Werten
print(Tabelle)
```

>Aufgabe: Können Sie die table-Funktion so umschreiben und erweitern, dass sie nicht die einzelnen Jahre, sondern Jahrzehnte zusammengefasst haben?


```R
TabelleJahrzehnt <- table(trunc(top250.t$Jahr/10)) # mathematische Operation und trunc-Funktion!
print(TabelleJahrzehnt)
```


```R
#visualisiert sieht das so aus:
plot(TabelleJahrzehnt)
```

Statt **192, 193, ...** soll am Ende **1920er, 1930er, ...** stehen. Dazu gehen wir nochmal einen Schritt zurück und erstellen eine Variable mit allen Jahreszahlen, die zu Jahrzehnten umgeschrieben werden (aber noch keine Häufigkeitstabelle!):


```R
dek <- trunc(top250.t$Jahr/10)
print(dek)
```


```R
# um aus 199, 197, 200 => 1990, 1970, 2000,... zu machen:
dek <- 10*dek
print(dek)
```

Bislang haben wir noch Zahlen; jetzt machen wir aus den Zahlen Text, so dass aus **1990, 1970, ...** => **1990er, 1970er, ...** wird.

```R
dek <- paste(dek,"er", sep="")
# hat 3 Parameter: die beiden Werte, die zusammen gefügt werden sollen und den Trenner
print(dek)
```



```R
# Und jetzt fügen wir diese Information noch als zusätzliche Spalte zu unserer Tabelle hinzu
top250.t$Dekade <- dek
```


```R
head(top250.t)
```


```R
plot(table(top250.t$Dekade))
```

```R
#Die Hilfefunktion zum Plot finden Sie:
?plot
```

>Aufgabe: Machen Sie den Plot etwas schöner, indem Sie die Linienart und Farbe ändern, eine Überschrift hinzufügen und die Bezeichnung der y-Achse ändern


```R
plot(table(top250.t$Dekade), type="b", col="dark red", 
main="Die beliebtesten Kino-Jahrzehnte", ylab="Häufigkeit")
```

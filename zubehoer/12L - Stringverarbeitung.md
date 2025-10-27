# Übungen zur Stringverarbeitung


## Übung 1 - verstecktes Wort

Im folgenden Text wurde ein Wort versteckt. Geben Sie nur die Zeichen am
Monitor aus, deren Index ein Vielfaches von 31 ist, also deren Index
sich durch 31 ohne Rest teilen lässt. Dabei wurde der Index 0 nicht
berücksichtigt. Das „“ am Ende macht nur den Zeilenumbruch im Editor
möglich. Benutzen Sie dazu eine geeignete Schleife.

**Text zum Kopieren:**

``` python
s = "Lorem ipsum dolor sit amet, conpectetur adipisici elit,\
lapsed yusmod tempor incidunt ut laborte et dolore magna\
aliquasum. Uthenim ad minim veniam, quis nosorud exercihation\
ullamco laborin nisi ut aliquid ex consequat."
```

``` python
# Insert code here
s = "Lorem ipsum dolor sit amet, conpectetur adipisici elit,\
lapsed yusmod tempor incidunt ut laborte et dolore magna\
aliquasum. Uthenim ad minim veniam, quis nosorud exercihation\
ullamco laborin nisi ut aliquid ex consequat."

print("Der Text:")
print("="*10)
print(s)
print("-"*10)
print("Anzahl Zeichen:", len(s))
print("="*10)
print("Das versteckte Wort lautet:")

for i in range(1, len(s)):
    if (i % 31) == 0:
        print(s[i], end="")
print()
```

    Der Text:
    ==========
    Lorem ipsum dolor sit amet, conpectetur adipisici elit,lapsed yusmod tempor incidunt ut laborte et dolore magnaaliquasum. Uthenim ad minim veniam, quis nosorud exercihationullamco laborin nisi ut aliquid ex consequat.
    ----------
    Anzahl Zeichen: 217
    ==========
    Das versteckte Wort lautet:
    Lpython

## Übung 2 - Widerstand

Ein Messgerät liefert einen String, welchen den gleichzeitig gemessenen
Spannungswert und die Stromstärke enthält. Aus diesen beiden Werten soll
der Widerstandswert errechnet und am Monitor ausgegeben werden.

U = 12,54 V I = 17,53 A

Formel Berechnung Widerstand:

<img src="images/widerstand.png" width=100 /> R = 715.35 Ω

**Text zum Kopieren:**

``` python
s= "Messwerte=12,54V-17,53mA"
```

``` python
# Insert code here
s = "Messwerte=12,54V-17,53mA"
#u = float(s[10:15].replace(",","."))
#i = float(s[17:22].replace(",","."))/1000
#r = u/i

s_teilu = s[10:15]
s_teili = s[17:22]

u = float(s_teilu.replace(",","."))
i = float(s_teili.replace(",","."))/1000
r = u / i 

print("gemessene Spannung [V]:", u)
print("gemessener Strom [A]:", i)
print("berechneter Widerstand [\u03A9]:", round(r,2))
```

    gemessene Spannung [V]: 12.54
    gemessener Strom [A]: 0.01753
    berechneter Widerstand [Ω]: 715.35

## Übung 3 - Textausgabe rückwärts am Monitor ausgeben

-   Lesen Sie einen String über die Tastatur ein und geben Sie den Text
    rückwärts am Monitor aus.
-   Zählen Sie, wie oft ein über die Tastatur eingebbares Zeichen darin
    enthalten ist. Geben Sie die Positionen am Monitor aus.

**Mögliche Ausgabe**

    Vorwärts:  Python macht Spass!
    Rückwärts:  !ssapS thcam nohty
    --------------------

    Nach welchem Zeichen soll gesucht werden?  a
    a kommt im Text 2 mal vor

``` python
# Insert code here
text = input("Vorwärts: ")
# Alternative 1 - Mit Schleife gelöst
rueck = ""
for i in range(len(text)-1, -1, -1):
    rueck += text[i]
print("Rückwärts: ", rueck)

# Alternative 2
print("Rückwärts: ", text[::-1]) # The fastest (and easiest?) way is to use a slice that steps backwards, -1.

print("-"*20)
zeichen = input("Nach welchem Zeichen soll gesucht werden? ")
anzahl = text.count(zeichen)
print(zeichen, "kommt im Text", anzahl, "mal vor")
```

    Vorwärts:  Python macht Spaß!
    Rückwärts:  !ßapS thcam nohtyP
    Rückwärts:  !ßapS thcam nohtyP
    --------------------
    Nach welchem Zeichen soll gesucht werden?  a
    a kommt im Text 2 mal vor

## Übung 4 - Zeichenkette in Teilbereiche zerlegen

Eine Windkraftanlage misst die erzeugte Leistung und Windstärke jede
Stunde und stellt diese Information durch Semikolon “;“ getrennt in
einer Zeichenkette zur Verfügung. - Datum, Uhrzeit - Windstärke -
Leistung

**Text zum Kopieren:**

``` python
wkr = "2020-12-16,08:00;8ms;2,3MW"
```

1.  Zerlegen Sie den String in Teilbereiche und geben sie diese am
    Monitor aus.
2.  Wandeln Sie das Datumsformat in das in Deutschland gebräuchliche
    Format um.

**Mögliche Ausgabe**

    2020-12-16,08:00;8ms;2,3MW
    --------------------
    Datum, Uhrzeit:  2020-12-16,08:00
    Windstärke:  8ms
    Leistung:  2,3MW
    --------------------
    Datum, Uhrzeit:  16.12.2020,08:00

``` python
# Insert code here
wkr = "2020-12-16,08:00;8ms;2,3MW"
print(wkr)
print('-'*20)
splits = wkr.split(";")
print("Datum, Uhrzeit: ", splits[0])
print("Windstärke: ", splits[1])
print("Leistung: ", splits[2])
print('-'*20)

dateTimeS = splits[0].split(",")
dateS = dateTimeS[0].split("-")
dateS.reverse()
datum = ".".join(dateS)
datumUhr = datum+","+dateTimeS[1]
print("Datum, Uhrzeit: ", datumUhr)
```

    2020-12-16,08:00;8ms;2,3MW
    --------------------
    Datum, Uhrzeit:  2020-12-16,08:00
    Windstärke:  8ms
    Leistung:  2,3MW
    --------------------
    Datum, Uhrzeit:  16.12.2020,08:00

## Übung 5 - Geheime Botschaft aus Zeichenkette

Sie sollen aus einem Text eine geheime Botschaft herausfiltern. In
diesem Text ist mehrfach der Teilstring „nad“ enthalten. Das zu suchende
Wort setzt sich aus den Buchstaben zusammen, die direkt nach diesem
Teilstring im Text enthalten sind.

Beispiel: Hallo Wnadxelt -\> würde den Buchstaben „x“ liefern.

Schreiben Sie einen Algorithmus, der alle geheimen Buchstaben aus dem
Text herausfiltert, diese zusammensetzt und am Monitor ausgibt.

**Text zum Kopieren:**

``` python
s = "Lorem ipsum dolor sit amet, consectetuer adipiscing elit,\
sed diamnadg nonummy nibh euismod tincidunt ut laoreet dolore\
magna aliquam eratnade volutpat. Ut wisi enim ad minim veniam,\
quis nostrud exerci tation ullamcorper suscipit lobortis\
nisl ut aliquip ex ea commodo consequat. Duis autem vel eum\
iriure dolor in hendrerit in vulputate velit esse molestie\
consequat, vel illum dolore eu feugiat nulla facilisis at\
vero et accumsan et iusto odio dignissim qui blandit\
praesent luptatum zzril delenit augue duis dolore te feugait\
nulla facilisi. Lorem ipsum dolornadh sit amet, consectetuer\
adipiscing elit, sed diam nonummy nibh euismod tincidunt ut\
laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad\
minim veniam, quis nostrud exercinade tation ullamcorper\
suscipit lobortisnadi nisl ut aliquip ex ea commodo consequat.\
Duis autem vel eum iriure dolor in hendrerit in vulputate\
velit esse molestie consequat, vel illum dolore eu feugiat\
nulla facilisis at veronadm et accumsan et iusto odio dignissim\
qui blandit praesent luptatum zzril delenit augue duis\
dolore te feugait nulla facilisi. Nam liber tempor cum soluta\
nobis eleifend option congue nihil imperdiet doming id quod\
mazim placerat facer possim assum."
```

``` python
# Insert code here
s = "Lorem ipsum dolor sit amet, consectetuer adipiscing elit,\
sed diamnadg nonummy nibh euismod tincidunt ut laoreet dolore\
magna aliquam eratnade volutpat. Ut wisi enim ad minim veniam,\
quis nostrud exerci tation ullamcorper suscipit lobortis\
nisl ut aliquip ex ea commodo consequat. Duis autem vel eum\
iriure dolor in hendrerit in vulputate velit esse molestie\
consequat, vel illum dolore eu feugiat nulla facilisis at\
vero et accumsan et iusto odio dignissim qui blandit\
praesent luptatum zzril delenit augue duis dolore te feugait\
nulla facilisi. Lorem ipsum dolornadh sit amet, consectetuer\
adipiscing elit, sed diam nonummy nibh euismod tincidunt ut\
laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad\
minim veniam, quis nostrud exercinade tation ullamcorper\
suscipit lobortisnadi nisl ut aliquip ex ea commodo consequat.\
Duis autem vel eum iriure dolor in hendrerit in vulputate\
velit esse molestie consequat, vel illum dolore eu feugiat\
nulla facilisis at veronadm et accumsan et iusto odio dignissim\
qui blandit praesent luptatum zzril delenit augue duis\
dolore te feugait nulla facilisi. Nam liber tempor cum soluta\
nobis eleifend option congue nihil imperdiet doming id quod\
mazim placerat facer possim assum."

offset = 0
key = 'nad'
word = ''
while True:
    pos = s.find(key, offset)
    if pos <= 0:
        break
    else:
        offset = pos+len(key)
        word+=s[offset]
        
print("Das gesuchte Geheimwort lautet:", word)
```

    Das gesuchte Geheimwort lautet: geheim

## Übung 6 - EAN Prüfziffer

Schreiben Sie ein Programm mit dem man sowohl die Prüfziffer einer EAN-
Nummer (Europäische Artikel- Nummerierung) berechnen als auch überprüfen
kann.

Die EAN- Nummer besteht aus 13 Ziffern, wobei es sich bei der letzten
Ziffer um die Prüfziffer handelt.

Beispiel für eine EAN ohne Prüfziffer: 978381582086\[?\]

Die Prüfziffer wird berechnet, indem man die ersten 12 Ziffern von links
beginnend abwechselnd mit 1 und 3 multipliziert und anschließend die
Produkte summiert.

Die Differenz zum nächsten Vielfachen von 10 ist die Prüfziffer.

Ist die Summe durch 10 teilbar, ist die Prüfziffer die Ziffer 0.

9·1 + 7·3 + 8·1 + 3·3 + 8·1 + 1·3 + 5·1 + 8·3 + 2·1 + 0·3 + 8·1 + 6·3 =
9 + 21 + 8 + 9 + 8 + 3 + 5 + 24 + 2 + 0 + 8 + 18 = 115 115 + 5 = 120 ⇒
Prüfziffer: 5

``` python
# Insert code here
# Lösung 1 - Iteration über die Länge des Strings
s ="978381582086"
summe = 0 
for i in range(len(s)):
    c = s[i]
    if i%2 == 0:
        summe +=int(c) 
    else:
        summe +=3*int(c) 
print("Prüfziffer: ",10 - summe%10)
```

    Prüfziffer:  5

``` python
# Lösung 2 mit enumerate() (siehe https://book.pythontips.com/en/latest/enumerate.html)
s ="978381582086"
summe = 0 
for i,c in enumerate(s):
    if i%2 == 0:
        summe +=int(c) 
    else:
        summe +=3*int(c) 
print("Prüfziffer: ",10 - summe%10)
```

    Prüfziffer:  5

``` python
# Lösung 3 mit List Comprehension (siehe https://www.w3schools.com/python/python_lists_comprehension.asp)
s ="978381582086"
summe = sum([int(c) if i%2==0 else 3*int(c) for i,c in enumerate(s)])
print("Prüfziffer: ",10 - summe%10)
```

    Prüfziffer:  5

## Übung 7 - Geheimtext erzeugen:

Schreiben Sie ein Programm, welches unter Angabe eines Textes und eines
Wortes den Text mit verstecktem “Geheimwort” erzeugt, wie sie ihn
bereits in Übung 1 kennengelernt haben. Die Zeichen des Geheimtextes
sollen hierbei gleichmäßig über den Text verteilt werden. Der Abstand
bestimmt sich hierbei über eine Floor-Division aus der Länge des Textes
und der Länge des geheimen Wortes.  
**Beispiel:**  
Anzahl Zeichen Text = 20  
Anzahl Zeichen geheimes Wort = 5  
Abstand = 4

Belegen Sie die Funktionalität Ihrer Kodierung, indem Sie mit Hilfe der
Lösung aus Übung 1 das geheime Wort wieder aus Ihrem neuen Text
auslesen.

``` python
# Insert code here
s = "Lorem ipsum dolor sit amet, conectetur adipisici elit,lapsed usmod tempor \
incidunt ut labore et dolore magnaaliquasum. Utenim ad minim veniam, quis \
nosrud exercihationullamco labori nisi ut aliquid ex consequat."

# Geheimtext einkodieren
geheim = "e1fx"
sNeu = ""
gZaehler = 0
i = 0
abstand = len(s)//len(geheim)
for c in s:
    sNeu += c
    i+=1
    if (i % abstand) == 0 and i > 0 and gZaehler < len(geheim):
        sNeu += geheim[gZaehler]
        gZaehler+=1
        i+=1
        
print("Neuer Geheimtext: ", sNeu)

# Geheimtext aus neuem Text lesen
for i in range(1, len(sNeu)):
    if (i % abstand) == 0:
        print(sNeu[i], end="")
```

    Neuer Geheimtext:  Lorem ipsum dolor sit amet, conectetur adipisici eliet,lapsed usmod tempor incidunt ut labore et dolore 1magnaaliquasum. Utenim ad minim veniam, quis nosrudf exercihationullamco labori nisi ut aliquid ex consxequat.
    e1fx

## Übung 8 - Caesar-Verschlüsselung

Bei der Caesar-Verschlüsselung wird jedem Buchstaben um einen Wert
(Schlüssel) nach hinten geschoben. Das Verfahren ist zirkulär. Wird ein
Z beispielsweise um 3 nach hinten geschoben, wird aus dem Z ein C.
Schreiben Sie ein Programm, welches unter Angabe eines Textes und eines
Schlüssels dein verschlüsselten Text ausgibt. Kontrollieren Sie Ihr
Ergebnis.

Beispiel:

Text: Volkswagen<br> Schlüssel: 10<br> verschlüsselter Text: Fyvucgkqox

``` python
# Insert code here
str = 'Volkswagen'
key = 10
strCaesar = ''
for i in range(len(str)):
    codepoint = ord(str[i])
    codepointCaesar = codepoint + key
    if (chr(codepoint).islower() and codepointCaesar > ord('z')) or (chr(codepoint).isupper() and codepointCaesar>ord('Z')):
        codepointCaesar=codepointCaesar-26
    strCaesar+=chr(codepointCaesar)
print(strCaesar)    
```

    Fyvucgkqox

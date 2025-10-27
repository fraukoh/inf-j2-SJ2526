# Übungen: Generatoren


#### Aufgabe 1

Schreibe eine Generator-Funktion `kehrwerte(n)`, die für alle Zahlen von
1 bis n die Kehrwerte generiert.

Bsp. kehrwerte(20) –\> 1.00 0.50 0.33 0.25 0.20 0.17 0.14 0.12 0.11 0.10
0.09 0.08 0.08 0.07 0.07 0.06 0.06 0.06 0.05

``` python
def kehrwerte(n):
    """Generator, der alle Kehrwerte von 1/1, 1/2, ..., 1/n erzeugt."""
    for x in range(1, n):
        yield 1/x
        
for zahl in kehrwerte(20):
    print(f"{zahl:.2f}", end=" ")   # zahl:.2f --> der Wert von zahl wird auf 2 Nachkommastellen genau angezeigt
```

    1.00 0.50 0.33 0.25 0.20 0.17 0.14 0.12 0.11 0.10 0.09 0.08 0.08 0.07 0.07 0.06 0.06 0.06 0.05 

#### Aufgabe 2

Schreibe eine Generator-Funktion `substrings(text, laenge)`, die alle
Teilstrings von `text` mit der Länge `laenge` erzeugt.

Bsp. substrings(“Python ist cool!”, 6) generiert folgende Strings:

`Python ython  thon i hon is on ist n ist   ist c ist co st coo t cool  cool!`

``` python
def substrings(text, laenge):
    for i in range(len(text) - laenge + 1):
        yield text[i:i+laenge]
        
for sub in substrings("Python ist cool!", 6):
    print(sub)
```

    Python
    ython 
    thon i
    hon is
    on ist
    n ist 
     ist c
    ist co
    st coo
    t cool
     cool!

#### Aufgabe 3

Schreibe eine Generator-Funktion `zaehle(start, ziel, schritt)`, die von
`start` bis `ziel` mit der Schrittweite `schritt` zählt (Defaultwert:
1).

Bsp. zaehle(start=10, ziel=20, schritt=0.5) –\>  
10 10.5 11.0 11.5 12.0 12.5 13.0 13.5 14.0 14.5 15.0 15.5 16.0 16.5 17.0
17.5 18.0 18.5 19.0 19.5 20.0

``` python
def zaehle(start, ziel, schritt=1):
    zahl = start
    while zahl <= ziel:
        yield zahl
        zahl += schritt
        
for zahl in zaehle(start=10, ziel=20, schritt=0.5):
    print(zahl, end= " ")  
```

    10 10.5 11.0 11.5 12.0 12.5 13.0 13.5 14.0 14.5 15.0 15.5 16.0 16.5 17.0 17.5 18.0 18.5 19.0 19.5 20.0 

Zur Kontrolle: Mit der `islice()`-Funktion aus dem (genialen!) [Modul
*itertools* der
Standardbibliothek](https://docs.python.org/3/library/itertools.html)
solltest du nun z.B. die ersten 10 Zahlen einer Zahlenfolge auswählen
können, die mit deiner Funktion `zaehle()` generiert wurde. Z.B. sollte
die folgende Zelle diese Ausgabe erzeugen:

\[100, 105, 110, 115, 120, 125, 130, 135, 140, 145\]

``` python
from itertools import islice

zaehler = zaehle(start=100, ziel=200, schritt=5)
zahlen = islice(zaehler, 10)
list(zahlen)
```

    [100, 105, 110, 115, 120, 125, 130, 135, 140, 145]

#### Aufgabe 4

Ändere deine Lösung der vorigen Aufgabe (oder die Musterlösung dazu) so
ab, dass ein *unendlicher* Generator ensteht, d.h. ein Zähler, der
prinzipiell vom Startwert aus unendlich lange immer weiter zählt.

Solange du mit `islice()` oder einer ähnlichen Funktion sicherstellst,
dass nur *endlich* viele Werte ausgelesen werden, kannst du sicher
nicht, nicht in eine Endlosschleife zu geraten!

``` python
def zaehle(start, ziel=None, schritt=1):
    zahl = start
    while ziel is None or zahl <= ziel:
        yield zahl
        zahl += schritt

from itertools import islice

zaehler = zaehle(start=0, schritt=7)
zahlen = islice(zaehler, 200)
for zahl in zahlen:
    print(zahl, end= " ")   
```

    0 7 14 21 28 35 42 49 56 63 70 77 84 91 98 105 112 119 126 133 140 147 154 161 168 175 182 189 196 203 210 217 224 231 238 245 252 259 266 273 280 287 294 301 308 315 322 329 336 343 350 357 364 371 378 385 392 399 406 413 420 427 434 441 448 455 462 469 476 483 490 497 504 511 518 525 532 539 546 553 560 567 574 581 588 595 602 609 616 623 630 637 644 651 658 665 672 679 686 693 700 707 714 721 728 735 742 749 756 763 770 777 784 791 798 805 812 819 826 833 840 847 854 861 868 875 882 889 896 903 910 917 924 931 938 945 952 959 966 973 980 987 994 1001 1008 1015 1022 1029 1036 1043 1050 1057 1064 1071 1078 1085 1092 1099 1106 1113 1120 1127 1134 1141 1148 1155 1162 1169 1176 1183 1190 1197 1204 1211 1218 1225 1232 1239 1246 1253 1260 1267 1274 1281 1288 1295 1302 1309 1316 1323 1330 1337 1344 1351 1358 1365 1372 1379 1386 1393 

#### Aufgabe 5

Schreibe eine Generator-Funktion `substrings(text)`, die **alle**
Teilstrings von `text`erzeugt.

Bsp. substrings(“Python”) generiert folgende Strings:

`P, Py, Pyt, Pyth, Pytho, Python, y, yt, yth, ytho, ython, t, th, tho, thon, h, ho, hon, o, on, n`

``` python
def substrings(text):
     for start in range(len(text)):
            for end in range(start+1, len(text)+1):
                yield text[start:end]

", ".join(substrings("Python"))
```

    'P, Py, Pyt, Pyth, Pytho, Python, y, yt, yth, ytho, ython, t, th, tho, thon, h, ho, hon, o, on, n'

# Funktionen höherer Ordnung, Lambdas, Closures


Funktionen sind in Python ganz normale *Objekte*, deshalb können sie in
Variablen gespeichert, in Listen gesammelt oder auch selbst als Argument
einer anderen Funktion verwendet werden.

``` python
# Beispiel: Ein paar einfache Funktionen

def sage_hallo():
    print("Hallo")

def fancy_hallo():
    print("*************")
    print("*   Hallo   *")
    print("*************")

def begruesse_zufaellig():
    from random import choice
    begruessungen = "Servus Tach Moin Mahlzeit Ciao".split()
    begruessung = choice(begruessungen)
    print(begruessung)
    
f1 = sage_hallo   # Eine andere Referenz auf dasselbe Funktionsobjekt
f2 = fancy_hallo
f3 = begruesse_zufaellig

f1()    # Klammern hinter dem Variablennamen --> Aufrufen (funktioniert auch über die neue Referenz)

funktionen = [f1, f2, f3]   # Eine Liste voller Funktionsreferenzen

print("Führe die nullte Funktion in der Liste aus:")
funktionen[0]()  # Element 0 wird aus der Liste geholt und dann sofort ausgeführt

print("Führe alle Funktionen in der Liste aus:")
for f in funktionen:
    f()
```

    Hallo
    Führe die nullte Funktion in der Liste aus:
    Hallo
    Führe alle Funktionen in der Liste aus:
    Hallo
    *************
    *   Hallo   *
    *************
    Moin

In Programmen müssen oft Befehle eine bestimmte Anzahl von Malen
wiederholt werden. Die meisten Programmiersprachen bieten dafür keinen
eigenen Schleifentyp. In Python z.B. muss man über ein `range`
iterieren - für Anfänger verwirrend wie die Schreibweise
`for(int i; i < n; i++)` in von C abgeleiteten Sprachen.

Könnte man nicht eine Wiederholungsschleife *selbst* programmieren?

``` python
def wiederhole(anzahl, eine_funktion):    # Die Funktion erhält eine andere Funktion als *Parameter*
    for i in range(anzahl):
        eine_funktion()   # Hier wird die übergebene Funktion ausgeführt
        
wiederhole(3, fancy_hallo)  
print("----------")
wiederhole(7, begruesse_zufaellig)
```

    *************
    *   Hallo   *
    *************
    *************
    *   Hallo   *
    *************
    *************
    *   Hallo   *
    *************
    ----------
    Moin
    Tach
    Ciao
    Servus
    Tach
    Servus
    Moin

``` python
import random

funktionen = [sage_hallo, begruesse_zufaellig]   # Eine Liste voller Funktionen
eine_funktion = random.choice(funktionen)   # Eine Variable, die eine Funktion enthält
n = random.randint(1, 6)
print(f"Die zufällig ausgewählte Funktion {eine_funktion.__name__} wird {n}-mal ausgeführt:")
wiederhole(n, eine_funktion)
```

    Die zufällig ausgewählte Funktion begruesse_zufaellig wird 6-mal ausgeführt:
    Servus
    Moin
    Tach
    Mahlzeit
    Ciao
    Moin

## Eine typische Anwendung: Sortieren mit `key`-Funktionen

``` python
namen = ['Tony Stark', 'Peter Parker', 'Wanda Maximoff', 'Natasha Romanoff', "T'Challa", "Steve Rogers", "Bruce Banner"]
print(sorted(namen))
# Aber was, wenn wir nach einem anderen Prinzip sortierten wollen?
print(sorted(namen, key=len))  # sorted ist eine HOF: len wir als Argument übergeben und (erst) intern aufgerufen

# Hilfsfunktion, um an den Nachnamen zu kommen
def nur_nachname(name):
    return name.split()[-1]

print(sorted(namen, key=nur_nachname))  # Diesmal nutzen wir eine selbstdefinierte Funktion als Sortierschlüssel
```

    ['Bruce Banner', 'Natasha Romanoff', 'Peter Parker', 'Steve Rogers', "T'Challa", 'Tony Stark', 'Wanda Maximoff']
    ["T'Challa", 'Tony Stark', 'Peter Parker', 'Steve Rogers', 'Bruce Banner', 'Wanda Maximoff', 'Natasha Romanoff']
    ['Bruce Banner', 'Wanda Maximoff', 'Peter Parker', 'Steve Rogers', 'Natasha Romanoff', 'Tony Stark', "T'Challa"]

…aber richtig praktisch wird das Sortieren mit `key`-Funktionen erst im
Zusammenspiel mit *Lambda-Ausdrücken*.

## Lambda-Ausdrücke

Keine Sorge: Lambda-Ausdrücke sind weder magisch, mystisch, noch
besonders schwierig zu verstehen. Lambda-Ausdrücke sind schlicht
**anonyme Funktionen**, d.h. Funktionen, die nur so kurzzeitig gebraucht
werden, dass es sich nicht einmal lohnt, ihnen einen Namen zu geben.

``` python
# Bsp. Hier passiert genau dasselbe wie im letzten Beispiel des vorigen Abschnitts:
sorted(namen, key=lambda name: name.split()[-1])
# nur wird als key diesmal eine anonyme Funktion übergeben, die danach direkt wieder vergessen wird
```

    ['Bruce Banner',
     'Wanda Maximoff',
     'Peter Parker',
     'Steve Rogers',
     'Natasha Romanoff',
     'Tony Stark',
     "T'Challa"]

Lambda-Ausdrücke werden dort verwendet, wo “schnell mal” eine Funktion
gebraucht wird. Deshalb ist ihre Syntax auch denkbar vereinfacht.

`lambda param1, param2, ...: Rückgabeausdruck`

Das bedeutet: - Die Funktion hat keinen Namen, sondern wird nur mit dem
Schlüsselwort *lambda* eingeleitet - Die Parameter der Funktion stehen
nicht in Klammern - Die Funktion besteht nur aus einem einzigen
Ausdruck, der ausgewertet und dann zurückgegeben wird - Das
Schlüsselwort `return` entfällt

Wichtig ist auch: Lambdas sind *Ausdrücke*, d.h. sie haben einen Wert
(nämlich die neudefinierte Funktion) und können, falls nötig, in
Variablen gespeichert werden:

``` python
# eine ziemlich triviale Funktion
def addiere(a, b):
    return a + b

# Und noch einmal als Lambda-Ausdruck:
addiere = lambda a, b: a + b

# HOF, die auf zwei Argumente angewendet wird
def berechne(eine_funktion, a, b):
    return eine_funktion(a, b)

# Die beiden folgenden Aufrufe sind äquivalent:
berechne(addiere, 19, 23)
berechne(lambda a, b: a+b, 19, 23)

# Auch das ist möglich:
addiere2 = lambda a, b: a+b    # Dies entspricht *exakt* der Definition von addiere() oben
berechne(addiere2, 19, 23)

# Mithilfe von Lambda-Ausdrücken können wir berechne() schnell und vielfältig einsetzen:
berechne(lambda a, b: a*b, 19, 23)
berechne(lambda c, d: c**d, 3, 4)
berechne(lambda c, d: len(c)+len(d), "Tim", "Tina")
berechne(lambda a, b: f"{a} liebt {b}", "Tim", "Tina")

```

    'Tim liebt Tina'

#### Ein etwas anspruchsvolleres Beispiel: Terme berechnen

``` python
# Das folgende Dictionary ordnet jedem Rechenzeichen einen zu dieser Rechnung passenden Lambda-Ausdruck, d.h eine Funktion zu
rechenoperation = {"+" : lambda a, b: a+b, "-" : lambda a, b: a-b, "^" : lambda a, b: a**b,
                   "*" : lambda a, b: a*b, "/" : lambda a, b: a/b}

def einlesen(term):
    """Parsing des Terms.  Extrem vereinfacht, da für unser Thema unwichtig."""
    import re
    symbole = re.findall('[0-9.]+|.', term.replace(" ", ""))
    a = int(symbole[0])
    op = symbole[1]
    b = int(symbole[2])
    return a, op, b

def berechne(term):
    a, op, b = einlesen(term)
    funktion = rechenoperation[op]   # Hole die passende Funktion aus dem Dictonary 
    return funktion(a, b)  # Führe die Funktion mit den beiden Argumenten aus

#term = input("Gib einen einfachen Term ein (z.B. 42/21 oder 5 - 123 oder 2^8 usw.): ")
term = "840 * 20"
ergebnis = berechne(term)
print(f"{term} = {ergebnis}")
    
```

    840 * 20 = 16800

## map und filter

Die beiden wahrscheinlich berühmtesten Funktionen höherer Ordnung heißen
`map` und `filter`. (Im selben Atemzug wird oft auch noch `reduce`
erwähnt - diese Funktion ist aber eher berühmt-berüchtigt und spielt
außerdem zum Glück keine Rolle für unser Zertifikat.) In *funktionalen*
Programmiersprachen spielen `map` und `filter` eine zentrale Rolle. In
Python ist es aber meist idiomatischer *list comprehensions* oder
*generator expressions* einzusetzen. Fürs Zertifikat (ab und zu auch für
die Praxis) sollten Sie map und filter aber auf jeden Fall kennen. V.a.
vertiefen Sie durch die Beschäftigung damit Ihr Verständnis von
Funktionen höherer Ordnung und ihrem Einsatz.

-   `map(fn, iterable)`: wendet die Funktion `fn` auf jedes Element des
    iterables an und liefert *alle* Ergebnisse in einem neuen iterable
    zurück. (map = “Abbildung” im mathematischen Sinn.)
-   `filter(pred_fn, iterable)`: Hier ist `pred_fn` ein sogenanntes
    *Prädikat*, d.h. eine Funktion, die einen *Wahrheitswert*
    zurücklieft. Der Aufruf `filter(pred_fn, iterable)` wendet die
    Funktion `pred_fn` auf jedes Element des iterables an und liefert
    dann alle diejenigen *Originalwerte* zurück, für die `pred_fn` den
    Wert `True` ergeben hat.

Am besten versteht man `map` und `filter`, wenn man Beispiele für ihre
Verwendung betrachtet:

``` python
namen = ["Anna", "Bibi", "Clara", "Dora", "Emma"]

# Beispiel für map()
laengen = map(len, namen)     # wende die Standardfunktion len auf alle Namen an
# Ergebnis: [4, 4, 5, 4, 4]

# Beispiel für filter()
def ist_lang(wort):
    return len(wort) > 4
lange_namen = filter(ist_lang, namen)
# Ergebnis: ['Clara']   (denn nur Namen mit mehr als 4 Buchstaben gelangen durch den Filter)
```

Man sieht gut: - `map(len, namen)` bildet eine Menge von Namen auf eine
Menge von Zahlen ab - `filter(ist_lang, namen)` liefert eine
eingeschränkte (“gefilterte”) Teilmenge der Ursprungsmenge

und das auf einer sehr kompakte Weise (die man nach ein bisschen
Gewöhnungszeit auch gut lesen kann, versprochen!)

Hinweis: map und filter arbeiten mit beliebigen (potentiell auch
*unendlichen*) iterables (s. Kapitel “Generatoren”) und liefern deshalb
auch iterables zurück. Deshalb muss man, wenn man die von map und filter
produzierten Ergebnisse ausgeben will, diese erstmal z.B. in eine Liste
konvertieren. Im Allgemeinen werden die beiden Funktionen aber sowieso
dazu benutzt um in *mehreren* Schritten Daten zu *transformieren* - es
ist daher auch aus Effizienzgründen praktisch, zwischendurch mit
iterables zu arbeiten (die evtl gar nie ganz erzeugt werden).

#### Weitere Beispiele für die Verwendung von `map`

``` python
namen = ["Anna", "Bibi", "Clara", "Dora", "Emma"]

# eine Hilfsfunktion für das folgende Beispiel
def rueckwaerts(s):
    return s[::-1]   # Bsp: "Python" -> "nohtyP"

laengen = map(len, namen)     # wende die Standardfunktion len auf alle Namen an
verkehrt = map(rueckwaerts, namen)     # wende die selbstdefinierte Funktion rueckwaerts auf alle Namen an
gross = map(lambda name: name.upper(), namen)     # wende eine anonyme Funktion auf alle Namen an 
gross2 = map(str.upper, namen)   # Besonders interessant: Eine String-*Methode* wird hier wie eine Funktion verwendet! Warum funktioniert das?

print(list(laengen))
print(list(verkehrt))
print(list(gross))
print(list(gross2))
```

    [4, 4, 5, 4, 4]
    ['annA', 'ibiB', 'aralC', 'aroD', 'ammE']
    ['ANNA', 'BIBI', 'CLARA', 'DORA', 'EMMA']
    ['ANNA', 'BIBI', 'CLARA', 'DORA', 'EMMA']

#### Weitere Beispiele für die Verwendung von `filter`

``` python
satz = "Onkel Otto sitzt mit seiner Quietschente in der Badewanne"
worte = satz.split()

kurze = filter(lambda wort: len(wort) <= 4, worte)
palindrome = filter(lambda wort: wort.lower() == rueckwaerts(wort).lower(), worte)
mit_o = filter(lambda wort: "o" in wort.lower(), worte)
substantive = filter(str.istitle, worte)   # Besonders interessant: Eine String-*Methode* wird hier wie eine Funktion verwendet! Warum funktioniert das?
        
print(list(kurze))
print(list(palindrome))
print(list(mit_o))
print(list(substantive))
```

    ['Otto', 'mit', 'in', 'der']
    ['Otto']
    ['Onkel', 'Otto']
    ['Onkel', 'Otto', 'Quietschente', 'Badewanne']

#### Welche Version bevorzugen Sie?

``` python
# Zum Vergleich: Welche Version bevorzugen Sie?

# 1. old-school
laengen = []
for name in worte:
    laengen.append(len(name))

# 2. funktional
laengen = map(len, worte) 

# 3. mit list comprehension
laengen = [len(name) for name in worte]
    

# Noch ein Vergleich: Welche Version bevorzugen Sie hier?
# 1. old-school
namen_mit_o = []
for name in worte:
    if "o" in name:
        namen_mit_o.append(name)

# 2. funktional
namen_mit_o = filter(lambda name: "o" in name, worte) 

# 3. mit list comprehension
name = [name for name in worte if "o" in name]
```

## Closures

-   sind dynamisch erzeugte Funktionen, also Funktionen, die erst zur
    Laufzeit definiert werden, z.B. innerhalb einer anderen Funktion
    oder einer Methode
-   und die Teile des sie umgebenden Kontexts “einschließen”, d.h. eine
    Variable “von außen” in der eigenen Definition verwenden.

Da das ein ziemlich abstraktes Konzept ist, betrachten wir ein paar
Beispiele:

``` python
# Eine Log-Funktion, zuerst in einer Variante ohne Closure
def log(level, msg):
    level_strings = {0: "ALL", 1: "DEBUG", 2: "WARN", 3: "ERROR"}
    level_str = level_strings[level]
    print(f"{level_str}: {msg}")

log(2, "Irgendwas läuft hier wahrscheinlich nicht wie geplant.")
log(3, "Das Programm ist leider abgestürzt!")
```

    WARN: Irgendwas läuft hier wahrscheinlich nicht wie geplant.
    ERROR: Das Programm ist leider abgestürzt!

``` python
# Schöner wäre es eigentlich, wir hätten für jedes Log-Level eine eigene Funktion.
# Aber muss man die einzeln definieren? Sie sind doch alle irgendwie gleich.
# Lösung: Wir definieren eine Funktion, die angepasste Log-Funktionen *erzeugt*!

def neuer_logger(level):
    level_strings = {0: "ALL", 1: "DEBUG", 2: "WARN", 3: "ERROR"}
    
    def neue_funktion(msg):
        level_str = level_strings[level]
        print(f"{level_str}: {msg}")

    return neue_funktion    

warnung = neuer_logger(2)
error = neuer_logger(3)

warnung("Irgendwas läuft hier wahrscheinlich nicht wie geplant.")
error("Das Programm ist leider abgestürzt!")
```

    WARN: Irgendwas läuft hier wahrscheinlich nicht wie geplant.
    ERROR: Das Programm ist leider abgestürzt!

Ein anderes Beispiel:

``` python
def inkrementierer(inkrement):
    def neue_funktion(x):
        return x + inkrement   # inkrement ist *kein* Parameter der neuen Funktion, sondern stammt von außen
    return neue_funktion   # funktion inkrementierer() erzeugt bei Ausführung eine neue Funktion mit individuellem Verhalten
    
plus7 = inkrementierer(7)   # plus7 ist eine neue Funktion
plusplus = inkrementierer(1)
print(plus7(8))
print(plus7(12))
print(plus7(5))
print(plusplus(99))
```

    15
    19
    12
    100

##### Korrekte HTML-Tags schreiben mit Closures

``` python
def html_tag(tg):
    tg2 = tg
    tg2 = tg[0] + '/' + tg[1:]

    def neue_funktion(str):
        return tg + str + tg2
    return neue_funktion


h1 = html_tag("<h1>")
b = html_tag('<b>')
div = html_tag('<div>')

print(h1("Überschrift"))
print(div(b('Monty Python')))
```

    <h1>Überschrift</h1>
    <div><b>Monty Python</b></div>

#### Ist es eine Funktion? Ist es ein Objekt? Es ist eine Closure!

``` python
def neuerZaehler():
    c = 0            # neue Zählvariable
    def f():         # innere Funktion f
        nonlocal c   # c stammt aus umgebender Fkt
        c += 1       # c darf verändert werden 
        return c         # f gibt aktuelles c zurück
    return f         # neuerZaehler gibt f zurück
```

``` python
z = neuerZaehler()
z()
```

    1

``` python
z()
```

    2

``` python
z()
```

    3

``` python
z2 = neuerZaehler()
z2()
```

    1

``` python
z()
```

    4

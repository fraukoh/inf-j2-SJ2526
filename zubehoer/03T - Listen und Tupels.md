# Listen, Tupel, List Comprehensions


## Listen

In Python ist die **Liste** eine der wichtigsten und meistverwendeten
Datenstrukturen. Wegen der Verwendung eckiger Klammern erinnert sie an
Java-Arrays, entspricht in der Implementierung aber eher Javas
`ArrayList`: Listen können beliebig wachsen und schrumpfen, sind aber so
implementiert, dass sie trotzdem die hervorragenden
Laufzeiteigenschaften von Arrays haben.

``` python
zahlenliste = [2, 3, 5, 7, 11, 13]
namensliste = ["Anna", "Berta", "Carla", "Doris", "Emilia", "Franziska", "Gabi", "Hannah", "Iris"]
gemischte_liste = ["Harry", 12, "Albus", 115, "Nicolas", 665]
verschachtelte_liste = [["Dudley", 13, ["Privet Drive", 4]], ["Albus", 115, ["Hogwarts"]]]
```

``` python
zahlenliste[0]
```

``` python
zahlenliste[0] = 42
zahlenliste
```

``` python
namensliste[3]
```

``` python
len(namensliste)
```

``` python
namensliste.append("Johanna")   # ein neues Element anfügen
#namensliste.extend(["Klara", "Lilli"])   # eine andere Liste anhängen
namensliste = namensliste + ["Klara", "Lilli"]
namensliste
```

``` python
namensliste.append("Gina")   # Oh, jetzt haben wir ja zwei Namen mit "G" - also entfernen wir einen wieder!
namensliste.remove("Gabi")   # aber die alphabetische Reihenfolge ist dahin... Was tun?
namensliste.sort()           # ...und fertig sortiert!
namensliste
```

``` python
# Wie kommt man an das letzte Element? In den meisten anderen Sprachen müsste man schreiben:
# namensliste[len(namensliste)-1]  
# In Python geht das viel einfacher:
namensliste[-1]  
```

## Slicing: Listen “scheibchenweise”

``` python
namensliste[1:3]   # Slicing: liefert einen "Ausschnitt" (Teilliste).  [Start(inkl):Ende(exkl):Schrittweite]  
#namensliste[1:3] + namensliste[3:5]
```

``` python
namensliste[0:7:2]  # Schrittweite 2, d.h. nur Element 0, 2, 4, 6
```

``` python
namensliste[::2]  # Start- und Endindex fehlen, nur Schrittweite 2 wird angegeben
```

``` python
namensliste[-3::-1]   # vom drittletzten Element rückwärts (Schrittweite -1)
```

### Verschachtelte Listen

Listen können u.a. selbst auch Listen enthalten:

``` python
verschachtelt = [[0, 1], [2, 3], [4, 5], [6, 7]]
verschachtelt[2][1]
```

``` python
# Bsp. für einen Baumstruktur mit Listen:

baum = ["Säugetier", ["Affe", ["Gorilla", "Schimpanse"]], ["Hund", ["Pudel", "Dackel", ["Zwergdackel", "Rauhaardackel"]]]]

# oft ist es allerdings noch geschickter, für solche Strukturen ein *dictionary* zu verwenden (s. dort).
```

### Über Listen iterieren

#### Die for-Schleife

Über alle Elemente einer Liste zu iterieren ist in Python denkbar
einfach:

``` python
for name in namensliste:
    print("Hallo", name)
    
# entspräche in Java der "erweiterten" for-Schleife (for each):
# for(String name : namensliste) {...}
```

#### enumerate()

Manchmal benötigt man nicht nur die Elemente selbst, sondern auch ihren
Index, d.h. ihre Position. Dazu könnte man dann doch eine klassische
“Zählschleife” verwenden - das ist aber nicht besonders schön und gilt
daher als nicht “pythonisch”:

``` python
# eher verpönt ist es, über einen Range mit der Länge der Liste zu iterieren:
for i in range(len(namensliste)): 
    name = namensliste[i]
    print(name)
```

Viel eleganter ist es, die Funktion `enumerate()` zu nutzen. Diese
erzeugt aus einer Liste von Werten *Paare* der Form (Index, Wert):

``` python
# Die "pythonische" Lösung:
#print(list(enumerate(namensliste)))

for i, name in enumerate(namensliste):     # erzeugt [(0, 'Anna'), (1, 'Berta'), (2, 'Carla'), (3, 'Doris'), ...]
    print(i, name)
    #print(f"{name} steht an Position {i} der Liste, d.h. sie ist das {i+1}. Element.")
```

#### zip()

Wie geht man vor, wenn man “parallel” über zwei Listen iterieren will?

Im folgenden Beispiel soll der vollständige Name jeder Person ausgegeben
werden. Allerdings sind die Vor- und Nachnamen in zwei *separaten*
Listen gespeichert. Auch hier wäre die “unpythonische” Lösung, anhand
eines Index (ähnlich wie im vorigen Abschnitt) gleichzeitig auf Elemente
beider Liste zugreifen.

Stattdessen nutzt man hier die Funktion `zip()`, die - wie ein
Reißverschluss (engl. zipper) - die Elemente beider Listen paarweise
“ineinander verhakt”:

``` python
vornamen = ["Anna", "Berta", "Carla"]
nachnamen = ["Adler", "Bär", "Chamäleon"]

for vn, nn in zip(vornamen, nachnamen):   # erzeugt [("Anna", "Adler"), ("Berta", "Bär") usw.]
    print(vn, nn)
```

``` python
# Beispiel: Die Elemente der beiden Listen sollen paarweise addiert werden zu: [11, 22, 33, 44, 55]
zahlen1 = [1, 2, 3, 4, 5]
zahlen2 = [10, 20, 30, 40, 50]

# nicht so hübsch:
"""
for i in range(len(zahlen1)):
    z1 = zahlen1[i]
    z2 = zahlen2[i]
    print(z1+z2)
"""

# "pythonic":
for z1, z2 in zip(zahlen1, zahlen2):
    print(z1+z2)
```

## Tupel

Auch **Tupel** werden in Python häufig verwendet. Intuition: Ein Tupel
repräsentiert einem **Datensatz** mit *fester* Länge mit Werten
potentiell unterschiedlicher Datentypen.

Bsp. `produkt = ("Tesla", "Model X", 100000)`

Tupel ähneln Listen; die meisten üblichen Listenoperationen sind auch
mit Tupeln möglich. Sie werden aber mit *runden* statt mit eckigen
Klammern geschrieben.

Wichtige Eigenschaften von Tupeln: \* unveränderlich (immutable) \*
insb. kann auch kein Wert hinzugefügt oder gelöscht werden \*
unterschiedliche Datentypen möglich

``` python
person1 = ("Harry", "Potter", 11)
person2 = ("Hermione", "Granger", 11)
person3 = ("Nicolas", "Flamel", 690)
```

``` python
person1[0]    # Zugriff auf Einzelwerte wie bei Liste/Array über Index.  Alternativ: namedtuple oder dataclass (ab 3.7)
# person1[0] = "James"   # das ist verboten!
```

``` python
tup = 1, 2, 3   # Klammern können auch weggelassen werden
type(tup)
```

``` python
(z1, z2, z3) = (32, 17, -4)   # Destrukturierung: Das Tupel wird in seine Einzelteile zerlegt und verschiedenen Variablen zugewiesen
print(z3, z2, z1)
vorname, nachname, alter = person1   
print(vorname, alter)
```

``` python
a = 1
b = 2
a, b = b, a   # Schau mal, Mama - ohne Hilfsvariable!!! Der Trick: Eigentlich steht da folgendes:
(a, b) = (b, a)   # Ein neues Tupel wird aus den Elementen eines anderen Tupels erzeugt
print(a, b)
```

``` python
for wert in person1:   # Schleife über die Elemente des Tupels
    print(wert)
```

``` python
personen = [person1, person2, person3]     # Liste von Tupeln
for person in personen:
    for wert in person:
        print(wert)
```

### Listen kopieren

``` python
a = [1, 2, 3]
b = a        # b ist eine neue Referenz, aber auf dasselbe Listenobjekt
c = list(a)  # Kopie der Liste
d = a[:]     # Kopie der Liste
a[0] = 42
d

t1 = (1, 2, 3)
t2 = t1
t3 = (1, 2, 3)
print(t1 == t2)   # enthalten gleiche Inhalte   s. equals() in Java
print(t1 == t3)   # enthalten gleiche Inhalte   s. equals() in Java
print(t1 is t2)   # Referenz auf dasselbe Objekt
print(t1 is t3)   # Referenz auf unterschiedliche Objekte
```

### List comprehension (unüblicher deutscher Name: Listenabstraktion)

([Ausführliches englisches
Tutorial](https://realpython.com/list-comprehension-python/))

Eine der wesentlichen Aufgaben des Computers ist die
“Datenverarbeitung”: Datenmengen werden untersucht, ausgewählt,
bearbeitet und wieder zurückgeliefert. Datenbanksprache wie SQL erlauben
es, solche Datenabfragen oder -transformationen kompakt darzustellen.
Eine SELECT-Anweisung in SQL ist **deklarativ**, d.h. sie beschreibt,
wie das gesuchte Ergebnis aussehen, aber nicht, mit welchem Verfahren es
berechnet werden soll.

In den meisten Programmiersprachen hingegen wird meist mit einer
Schleife über eine Liste/Array iteriert, mit if-Befehlen eine Auswahl
getroffen und (evtl. veränderte) Daten in einer neuen Liste gespeichert.
Hier wird dem Computer genau gesagt, wie er vorgehen soll; die
Beschreibung ist also **prozedural**. Der Code ist dabei meist deutlich
länger und die eigentliche Bedeutung der so generierten neuen Liste ist
nur schwer zu erkennen.

Python bietet mit *list comprehensions* eine kompakte, deklarative
Darstellung solcher Auswahl- und Transformationsprozesse. Sie ist an die
mathematische Mengenschreibweise angelegt. So beschreibt der Ausdruck $
{ x^2 | 10 x \< 20, x } $ die Menge der Quadratzahlen aller natürlichen
Zahlen zwischen 10 und 20. In Python schreibt man analog:

``` python
quadrate = [x**2 for x in range(10, 20)]
quadrate
```

Die Listennotation mit \[eckigen Klammern\] wird also nicht nur
verwendet, um Elemente explizit aufzuzählen, sondern auch um Listen aus
anderen zu *berechnen* bzw. *auszuwählen*.

Syntax: \[Berechnung for Variable in Liste if Bedingung\]

Vergleiche die Lösungen der folgenden

**Aufgabe:** Gib in GROSSBUCHSTABEN alle Namen aus einer Liste aus, die
länger als vier Zeichen sind.

``` python
liste = ["Anna", "Berta", "Carla", "Doris", "Emilia", "Franziska", "Gabi", "Hannah", "Iris"]

# mit Schleife:
namen_neu = []
for name in liste:
    if len(name) > 4:
        namen_neu.append(name.upper())
print(namen_neu)

# mit list comprehension:
namen_neu = [name.upper() for name in liste if len(name) > 4]
print(namen_neu)
```

##### Und noch eine Aufgabe

Berechne die Summe aller ungeraden Zahlen in der folgenden Liste.

*Tipp:* In SQL wäre die Lösung

    SELECT SUM(z) FROM zahlen WHERE z % 2 = 1

``` python
zahlen = [7, 43, 12, 0, -3, -35, 33, 24, 8, 45, 60, 2, 13, -1, 22, 9]

# Lösung:

sum(z for z in zahlen if z % 2 == 1)    # genau wie in SQL, oder?
```

*Frage:* Müssten bei `sum(z for z in zahlen if z % 2 == 1)` nicht noch
eckige Klammern rein?

*Antwort:* Innerhalb eines Funktionsaufrufs, wie hier in `sum()`, ist
diese Kurzform ohne Klammern tatsächlich möglich. Warum, erfährst du
beim Thema *Generatoren*.

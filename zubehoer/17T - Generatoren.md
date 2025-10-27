# Generatoren und Iteratoren


Links: - https://www.w3schools.com/python/python_iterators.asp -
https://edube.org/learn/pe-2/generators-and-closures-42 (vorher anmelden
auf www.edube.org) - Einführung in Generatoren bei
[python-kurs.eu](https://www.python-kurs.eu/python3_generatoren.php)

In Python gibt es verschiedene Möglichkeiten, über Datenstrukturen zu
*iterieren*, d.h. sie elementweise zu durchlaufen. Die gebräuchlichste
ist die for-Schleife. Mit ihr kann man nicht nur Listen durchlaufen,
sondern auch Tupel, Dictionaries, Zahlenbereiche (ranges), usw.
Allerdings hat der Begriff “Durchlaufen” für jede Datenstruktur eine
eigene Bedeutung. Zur Vereinheitlichung verwendet Python deshalb intern
sogenannte *Iteratoren*.

### Iteratoren und Iterables

Um zu verstehen, was Iteratoren sind, schauen wir uns an, was bei einer
for-Schleife in Python im Hintergrund passiert. Der folgende Code…

``` python
# als Bsp eine Menge (set), könnte aber auch list, dict, etc sein
irgendein_container = {3, 7, -1, 2, 43}  

for elmt in irgendein_container:
    print(elmt, end=" ")
```

    2 3 7 43 -1 

…wird intern ungefähr so interpretiert:

``` python
# erzeuge einen Iterator für diesen Container
iterator = iter(irgendein_container)

while True:
    try:
        # Hole das nächste Element aus dem Iterator
        elmt = next(iterator)
        print(elmt, end=" ")
    except StopIteration:
        # Sobald eine StopIteration-Exception geworfen wird, brich die Schleife ab
        break
```

    2 3 7 43 -1 

Die entscheidenden Schritte hierbei sind: 1. Der Aufruf von `iter`
erzeugt und initialisiert einen Iterator, 2. aus dem dann mit `next`
solange Elemente ausgelesen und verarbeitet werden, 3. bis der Iterator
“verbraucht” ist und eine StopIteration-Exception die Schleife beendet.

Man kann das Iterieren über einen Container “von Hand” simulieren, z.B.
so:

``` python
# Am besten demonstriert man dieses Beispiel im interaktiven Debugger von Thonny oder vscode.
liste = [1, 2, 3]
iterator = iter(liste)
print(next(iterator))
print(next(iterator))
print(next(iterator))
print(next(iterator))  # Hier wird die Exception geworfen
```

    1
    2
    3

    StopIteration: 

Was aber passiert *in* den beiden Funktionen `iter` und `next`? Für die
in Python bereits vorhandenen Container-Typen kann das variieren, für
alle anderen Klassen gilt: - `iter(ein_container)` ruft
`ein_container.__iter__()` auf und - `next(ein_iterator)` ruft
`ein_iterator.__next__()` auf.

Diese beiden “magic methods” kann man für die eigene Klasse selbst
implementieren - und sie danach sofort mit einer for-Schleife
durchlaufen. Betrachten wir ein praktisches Beispiel:

``` python
# Leider akzeptiert range() keine float-Werte für den step-Parameter. Wir können also nicht schreiben:
# for x in range(0, 10, 0.5):
#     print(x, end=" ")
# Aber... wir können uns das selbst bauen!

class float_range:
    def __init__(self, start, stop, inc):
        self.start = start
        self.stop = stop
        self.inc = inc

    def __iter__(self):
        self.counter = self.start  # Initialisierung
        return self  # Klasse ist ihr eigener Iterator
    
    def __next__(self):
        if self.counter >= self.stop:  # Ziel erreicht?
            raise StopIteration   # Iteration beenden
        tmp = self.counter
        self.counter += self.inc
        return tmp


for x in float_range(0, 10, 0.5):
    print(x, end=" ")
```

    0 0.5 1.0 1.5 2.0 2.5 3.0 3.5 4.0 4.5 5.0 5.5 6.0 6.5 7.0 7.5 8.0 8.5 9.0 9.5 

Anmerkung: Andere Sprachen definieren für diesen Zweck ein *Interface*,
z.B. das [Iterable-Interface in
Java](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Iterable.html).
Python nutzt - ganz im Geist des [“duck
typing”](https://realpython.com/lessons/duck-typing/) - stattdessen ein
*Protokoll*, d.h. sobald eine Klasse die Methoden `__iter__` und
`__next__` zur Verfügung stellt, ist sie *iterable* und kann mit
iter/next bzw. v.a. in einer for-Schleife verwendet werden.

## Generatoren

Iteratoren sind äußerst hilfreich - aber etwas unschön zu programmieren.
Da das “Zen of Python” gleich als erstes Prinzip festhält *“Beautiful is
better than ugly”*, gibt es natürlich eine elegantere Variante,
Iteratoren zu definieren, nämlich die sogenannten *Generatoren*.

Generatoren sehen auf den ersten Blick aus wie Funktionen. Statt eines
return-Befehls enthalten sie jedoch (ein- oder mehrfach) das
Schlüsselwort `yield`. Beim Aufruf einer solchen “Funktion” wird ein
Objekt der Klasse `Generator` erzeugt und zurückgegeben. Dieses verhält
sich wie ein Generator: Es liefert Werte und wirft zum Schluss eine
StopIteration-Exception. Die Werte werden in diesem Fall aber nicht
durch eine `__next__`-Methode erzeugt, sondern über den `yield`-Befehl
an den aufrufenden Code zurückgeliefert.

Am besten sieht man das an einem Beispiel:

``` python
def fibonacci1():     # Am besten demonstriert man diesen und die folgenden Generatoren im interaktiven Debugger von Thonny oder vscode.
    yield 0
    yield 1
    yield 1
    yield 2
    yield 3
    yield 5
    
fibo = fibonacci1()   # Generator-Objekt wird erzeugt, macht aber noch nichts
print(fibo)
print(next(fibo))     # Generator wird ausgeführt bis zum ersten yield
print(next(fibo))     # ...bis zum nächsten yield
print('Eine kleine Zwischenausgabe aus dem "Hauptprogramm"...')
print(next(fibo))     # ...bis zum nächsten yield
print(next(fibo))     # ...usw.
print(next(fibo))
print(next(fibo))
print(next(fibo))     # Und was passiert jetzt?
```

    <generator object fibonacci1 at 0x000001DB17DCB0B0>
    0
    1
    Eine kleine Zwischenausgabe aus dem "Hauptprogramm"...
    1
    2
    3
    5

    StopIteration: 

Wir sehen: Die `yield`-Befehle verhalten sich ähnlich wie Breakpoints,
d.h. jedesmal, wenn ein `yield` erreicht wird liefert der Generator
einen neuen Wert an den aufrufenden Code zurück - springt aber beim
nächsten Aufruf *wieder an genau die Stelle im Generator zurück, an er
zuletzt verlassen wurde*!

Natürlich nutzt man Generatoren normalerweise nicht wie im obigen
Beispiel, sondern in einer for-Schleife:

``` python
fibo = fibonacci1()   # Generator-Objekt wird erzeugt, macht aber noch nichts
for zahl in fibo:     # Wir erinnern uns: die for-Schleife ruft die Elemente der Iterators schrittweise ab
    print(zahl, end=" ")
```

    0 1 1 2 3 5 

Ihre eigentliche Stärke zeigen Generatoren im Zusammenspiel mit
Schleifen:

``` python
def fibonacci(maximum):
    x = 0
    y = 1
    while x < maximum:
        yield x
        x, y = y, x + y
        
fibo = fibonacci(1000)
print(next(fibo), end=" ")   # Generiere das 1. Element
print(next(fibo), end=" ")   # Generiere das 2. Element
for zahl in fibo:            # Generiere alle weiteren Elemente - d.h. der Generator wird *nicht* neu gestartet
    print(zahl, end=" ")
print()

for zahl in fibonacci(250):  # ein neuer Generator wird erzeugt
    print(zahl, end=" ")

fib100 = list(fibonacci(100))  # Werte des Generators in Liste speichern
print(fib100)
```

    0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 
    0 1 1 2 3 5 8 13 21 34 55 89 144 233 [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]

Aber es kommt noch besser…

### Unendliche Generatoren/Iteratoren

Iteratoren und Generatoren sind *lazy* (s. Lazy Evaluation), d.h. sie
berechnen erst dann einen neuen Wert, wenn sie per next() danach gefragt
werden. Dies ermöglicht es, Geneatoren/Iteratoren zu definieren, die
prinzipiell unendlich viele Werte liefern können.

``` python
def alle_ungeraden_zahlen():
    """Generator, der *alle* ungeraden natürlichen Zahlen liefert"""
    n = 1
    while True:
        yield n
        n += 2
        
def summiere_bis(zahlen, maximum):
    """ganz normale Funktion, die so lange Zahlen addiert, bis eine bestimmte Summe erreicht ist"""
    summe = 0
    for zahl in zahlen:
        if summe + zahl > maximum:
            return summe
        summe += zahl 
        
zahlen = alle_ungeraden_zahlen()   # Ist das eine Endlosschleife?
summe = summiere_bis(zahlen, 500)     # oder ist hier die Endlosschleife?
print(summe)
```

    484

Es kommt also zu *keiner* Endlosschleife, obwohl `alle_ungeraden_zahlen`
so wirkt, als enthielte es eine! Solange der Code, der der Generator
verwendet, selbst irgendwann aufhört, weitere Werte anzufordern, kann
nichts passieren.

Diese Eigenschaft von Generatoren erlaubt häufig eine sehr elegante
Programmierweise. Z.B. können wir die Fibonacci-Folge wie in der
Mathematik als unendliche, induktiv definierte Zahlenfolge beschreiben:

``` python
def fibonacci_unendlich():
    x, y = 0, 1
    while True:
        yield x
        x, y = y, x + y
```

Wie wir diesen unendlich Generator dann verwenden, ist von seiner
Definition völlig losgelöst. Z.B. so:

``` python
anzahl = 20
fib = fibonacci_unendlich()  # Generator wird erzeugt, aber noch nicht aufgerufen - also wieder keine Endlosschleife!
for i, zahl in enumerate(fib):  # Versucht enumerate() etwa, die gesamte Fibonacci-Folge durchzunummerieren? 
    print(zahl, end=" ")
    if i >= anzahl:
        break
```

    0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597 2584 4181 6765 

Noch eleganter aber z.B. so:

``` python
def hole(anzahl, iterator):
    """holt anzahl Elemente aus dem iterator"""
    for _ in range(anzahl):
        yield next(iterator)
        
for zahl in hole(20, fibonacci_unendlich()):    # die ersten 20 Elemente einer unendlichen Folge --> keine Endlosschleife dank lazy evaluation
    print(zahl, end=" ")   
```

    0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597 2584 4181 

Eine Funktion wie `hole` ist im Umgang mit unendlichen Iteratoren oder
unendlichen Datenstrukturen sehr nützlich - deswegen gibt es sie in der
Python-Standardbibliothek natürlich schon längst, sogar in erweiterter
Form:

``` python
from itertools import islice    # islice(iterator, start, stop, step) funktioniert wie liste[start:stop:step] oder range(start, stop, step)
# Fundamentaler Unterschied: islice kann auch mit *unendlichen* Datenstrukturen arbeiten!!!

for zahl in islice(fibonacci_unendlich(), 0, 20, 2):
    # liefert jede zweite der ersten zwanzig Fibonacci-Zahlen
    print(zahl, end=" ")   
```

    0 1 3 8 21 55 144 377 987 2584 

## Generator Expressions

``` python
# Sie kennen schon list comprehensions:
o1 = [n**2 for n in range(20) if n % 2 == 1]    # list comprehension
print(o1)
print(sum(o1))

# Generator comprehensions nutzt man exakt gleich - nur mit runden statt eckigen Klammern
o2 = (n**2 for n in range(20) if n % 2 == 1)    # generator expression
print(o2)  # der Generator wird noch nicht evaluiert - also auch nicht als Liste ausgegeben
print(sum(o2))
```

    [1, 9, 25, 49, 81, 121, 169, 225, 289, 361]
    1330
    <generator object <genexpr> at 0x000001DB17CC7820>
    1330

Ein nettes kleines syntaktisches “Zuckerl” von Python ist, dass man die
runden Klammern um eine Generator Expression sogar ganz weglassen darf,
wenn diese als einziges Argument einer Funktion verwendet wird. Die
folgenden Ausdrücke sind also äquivalent:

``` python
s1 = sum((n**2 for n in range(20)))
s2 = sum(n**2 for n in range(20))
print(s1, s2)
```

    2470 2470

### Laufzeit und Speicherverbrauch

``` python
anzahl = 20_000_000
```

``` python
%%time
sum([n**2 for n in range(anzahl) if n % 2 == 0])
```

    CPU times: total: 4.22 s
    Wall time: 4.27 s

    1333333133333340000000

``` python
%%time
sum(n**2 for n in range(anzahl) if n % 2 == 0)
```

    CPU times: total: 4.06 s
    Wall time: 4.11 s

    1333333133333340000000

Es sieht so aus, als gäbe es keinen großen Laufzeitunterschied zwischen
Listen (bzw. list comprehensions) und Generatoren (bzw. generator
expressions).

Aber schauen wir uns noch ein weiteres Beispiel an. Wir wollen prüfen,
ob eine Folge von Zahlen einen bestimmten Wert enthält:

``` python
anzahl = 10**7
```

``` python
%%time
if 1_000_000 in [n**2 for n in range(anzahl) if n % 2 == 0]:
    print("gefunden")
else:
    print("nicht gefunden")
```

    gefunden
    CPU times: total: 1.92 s
    Wall time: 1.93 s

``` python
%%time
if 1_000_000 in (n**2 for n in range(anzahl) if n % 2 == 0):
    print("gefunden")
else:
    print("nicht gefunden")
```

    gefunden
    CPU times: total: 0 ns
    Wall time: 3.85 ms

**Wie bitte - null Nanosekunden? Ist das Zauberei?**

Können Sie erklären, wie es zu diesem gigantischen Unterschied kommt?

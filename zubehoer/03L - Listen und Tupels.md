# Lösungen: Listen, Tupel, List Comprehensions


### Listen

##### Aufgabe 1

Gib für die folgende Liste jeweils aus: 1. das 7. Element 1. die
Elemente an Position 0 bis 2 (d.h. drei Elemente) 1. das vorletzte
Element 1. jedes zweite Element 1. das Element in der Mitte der Liste

``` python
liste = ["Anna", "Berta", "Carla", "Doris", "Emilia", "Franziska", "Gabi", "Hannah", "Iris"]

# Lösung:
print(liste[6])     # Start bei 0
print(liste[0:3])   # letzter Index gehört nicht mehr dazu
print(liste[-2])    # vorletztes Element
print(liste[::2])   # Schrittweite 2
mitte = len(liste) // 2
print(liste[mitte])
```

    Gabi
    ['Anna', 'Berta', 'Carla']
    Hannah
    ['Anna', 'Carla', 'Emilia', 'Gabi', 'Iris']
    Emilia

##### Aufgabe 2

Berechne für die folgende Liste: 1. das größte Element 1. den
Durchschnitt 1. den Median

``` python
zahlen = [2, 3.14159, -12, 99, 42/13, 0.0, 10, -1, 4]

# Lösung:
groesstes = zahlen[0]    # Annahme (hier der Einfachheit halber): Liste ist nicht leer
summe = 0

for zahl in zahlen:
    summe += zahl
    if zahl > groesstes:
        groesstes = zahl

print("Größtes Listenelement:", groesstes)
print("Durchschnitt:", summe / len(zahlen))
        
sortiert = sorted(zahlen)   # sorted(): lässt ursprüngliche Liste unverändert
mitte = len(sortiert) // 2
print("Median:", sortiert[mitte])
```

    Größtes Listenelement: 99
    Durchschnitt: 12.041373247863246
    Median: 3.14159

##### Aufgabe 3

Erzeuge aus der gegebenen Liste jeweils eine neue: 1. die Quadrate der
gegebenen Zahlen 1. nur Zahlen zwischen 30 und 50 1. nur ungerade Zahlen

``` python
zahlen = [13, 47, 4, 12, 23, 17, 83, 45, 52, 63, 37, 94, 49, 8, 11, 31, 44, 72, 47]

# Lösung:
quadrate, zwischen30und50, ungerade = [], [], []
for zahl in zahlen:
    quadrate.append(zahl * zahl)
    if 30 < zahl < 50:
        zwischen30und50.append(zahl)
    if zahl % 2 == 1:
        ungerade.append(zahl)
        
print(quadrate)
print(zwischen30und50)
print(ungerade)
```

    [169, 2209, 16, 144, 529, 289, 6889, 2025, 2704, 3969, 1369, 8836, 2401, 64, 121, 961, 1936, 5184, 2209]
    [47, 45, 37, 49, 31, 44, 47]
    [13, 47, 23, 17, 83, 45, 63, 37, 49, 11, 31, 47]

##### Aufgabe 4

Prüfe für jede der Listen aus `listen`, ob sie ein *Palindrom* ist, d.h.
von vorne wie von hinten gleich ist.

Übrigens: Viele Listenoperationen funktionieren auch mit String (s.
letztes Element von `listen`)!

``` python
listen = [[1, 2, 3, 2, 1], [1, 2, 3, 1], ["ich", "bin", "ich"], "LAGERREGAL"]

# Lösung:
for liste in listen:
    ergebnis = "ein" if liste[::-1] == liste else "kein"    # Java: ergebnis = bedingung ? trueV : falseV;
    print(f"{liste} ist {ergebnis} Palindrom.")
    
    
# Lösung:
for liste in listen:
    if liste[::-1] == liste: 
        ergebnis ="ein"
    else: 
        ergebnis ="kein"
    print(f"{liste} ist {ergebnis} Palindrom.")
    
for liste in listen:
    for i in range(len(liste) // 2):
        if liste[i] != liste[-i-1]:
            ergebnis = "kein"
            break
        else:
            ergebnis = "ein"
    print(f"{liste} ist {ergebnis} Palindrom.")
```

    [1, 2, 3, 2, 1] ist ein Palindrom.
    [1, 2, 3, 1] ist kein Palindrom.
    ['ich', 'bin', 'ich'] ist ein Palindrom.
    LAGERREGAL ist ein Palindrom.
    [1, 2, 3, 2, 1] ist ein Palindrom.
    [1, 2, 3, 1] ist kein Palindrom.
    ['ich', 'bin', 'ich'] ist ein Palindrom.
    LAGERREGAL ist ein Palindrom.
    [1, 2, 3, 2, 1] ist ein Palindrom.
    [1, 2, 3, 1] ist kein Palindrom.
    ['ich', 'bin', 'ich'] ist ein Palindrom.
    LAGERREGAL ist ein Palindrom.

### List Comprehensions

##### Aufgabe 1

Erzeuge (s.o.) aus der gegebenen Liste *mithilfe einer list
comprehension* jeweils eine neue: 1. die Quadrate der gegebenen
Zahlen 1. nur Zahlen zwischen 30 und 50 1. nur ungerade Zahlen

Vergleiche mit der ursprünglichen schleifenbasierten Lösung.

``` python
zahlen = [13, 47, 4, 12, 23, 17, 83, 45, 52, 63, 37, 94, 49, 8, 11, 31, 44, 72, 47]

# Lösung:
quadrate = [zahl * zahl for zahl in zahlen]
zwischen30und50 = [zahl for zahl in zahlen if 30 < zahl < 50]
ungerade = [zahl for zahl in zahlen if zahl % 2 == 1]
```

##### Aufgabe 2

Erzeuge eine Liste mit denjenigen Namen aus der Liste `gallier`, die mit
‘x’ enden, und zwar in korrekter Schreibweise, d.h. der Anfangsbuchstabe
des jeweiligen Namens wird groß, die restlichen Buchstaben
kleingeschrieben.

``` python
gallier = ["asterix", "OBELIX", "Miraculix", "CaEsaR", "TROUBADIX", "Gutemine"]

# Lösung:
[name.title() for name in gallier if name.lower().endswith('x')]
# alternativ: [name.title() for name in gallier if name.lower()[-1] == 'x']
```

    ['Asterix', 'Obelix', 'Miraculix', 'Troubadix']

##### Aufgabe 3

Erzeuge aus einer Liste mit Namen der Form “Vorname Nachname” eine Liste
der Form “Nachname, Vorname”. Bsp.:

`["Harry Potter", "Albus Dumbledore", "Severus Snape"]` wird zu

`['Potter, Harry', 'Dumbledore, Albus', 'Snape, Severus']`

``` python
namen = ["Harry Potter", "Albus Dumbledore", "Severus Snape"]

# Lösung:
aufgeteilt = [name.split() for name in namen]
tupel = [f"{name[1]}, {name[0]}" for name in aufgeteilt]

tupel
```

    ['Potter, Harry', 'Dumbledore, Albus', 'Snape, Severus']

##### Aufgabe 4

Erzeuge eine Liste mit den Zahlen des kleinen 5x5, also

\[1, 2, 3, 4, 5, 2, 4, 6, 8, 10, 3, 6, 9, 12, 15, 4, 8, 12, 16, 20, 5,
10, 15, 20, 25\]

``` python
# Lösung:
zahlen = [a*b for a in range(1, 6) for b in range(1, 6)]
print(zahlen)
```

    [1, 2, 3, 4, 5, 2, 4, 6, 8, 10, 3, 6, 9, 12, 15, 4, 8, 12, 16, 20, 5, 10, 15, 20, 25]

##### Aufgabe 5

Erzeuge noch einmal das 5x5, aber diesmal als Tabelle (verschachtelte
Liste), also

\[\[1, 2, 3, 4, 5\],  
\[2, 4, 6, 8, 10\],  
\[3, 6, 9, 12, 15\],  
\[4, 8, 12, 16, 20\],  
\[5, 10, 15, 20, 25\]\]

``` python
# Lösung:
[[a*b for a in range(1, 6)] for b in range (1,6)]
```

    [[1, 2, 3, 4, 5],
     [2, 4, 6, 8, 10],
     [3, 6, 9, 12, 15],
     [4, 8, 12, 16, 20],
     [5, 10, 15, 20, 25]]

##### Aufgabe 6

Finde mit einer List Comprehension alle Worte in folgendem Text.

<details>
<summary>
Hier klicken für Tipps:
</summary>
Benutze die String-Methoden split() und strip(). Die Konstante
string.punctuation (googlen!) könnte auch hilfreich sein…
</details>

``` python
TEXT = """
Habe nun, ach! Philosophie,
Juristerei und Medizin,
Und leider auch Theologie
Durchaus studiert, mit heißem Bemühn.
Da steh' ich nun, ich armer Tor,
Und bin so klug als wie zuvor!
Heiße Magister, heiße Doktor gar,
Und ziehe schon an die zehen Jahr'
Herauf, herab und quer und krumm
Meine Schüler an der Nase herum.
"""


# Lösung:
import string
worte = [wort.strip(string.punctuation) for wort in TEXT.split()]
print(worte)
```

    ['Habe', 'nun', 'ach', 'Philosophie', 'Juristerei', 'und', 'Medizin', 'Und', 'leider', 'auch', 'Theologie', 'Durchaus', 'studiert', 'mit', 'heißem', 'Bemühn', 'Da', 'steh', 'ich', 'nun', 'ich', 'armer', 'Tor', 'Und', 'bin', 'so', 'klug', 'als', 'wie', 'zuvor', 'Heiße', 'Magister', 'heiße', 'Doktor', 'gar', 'Und', 'ziehe', 'schon', 'an', 'die', 'zehen', 'Jahr', 'Herauf', 'herab', 'und', 'quer', 'und', 'krumm', 'Meine', 'Schüler', 'an', 'der', 'Nase', 'herum']

##### Aufgabe 7

Den gesamten Text von Goethes *Faust* findest du als Textdatei im
Internet (s. untenstehende URL). Schreibe ein Programm, das den Text
lädt (mit der Funktion `urlopen()`) und daraus eine Liste einzelner
Wörter erzeugt (wie in der vorigen Aufgabe).

Zur Kontrolle: Die Liste sollte 31161 Worte enthalten und wie folgt
beginnen:

\[‘Goethe’, ‘Faust’, ‘Johann’, ‘Wolfgang’, ‘von’, ‘Goethe’, ‘Faust’,
‘Eine’, ‘Tragödie’, ‘Erster’, ‘Theil’, ‘Einleitende’, ‘Angaben’,
‘Zueignung’, ‘Ihr’, ‘naht’, ‘euch’, ‘wieder’, ‘schwankende’,
‘Gestalten’, …\]

<details>
<summary>
Hier klicken für Tipps:
</summary>
Auf der genannten URL ist der Faust-Text in UTF-8 kodiert. Um eine Zeile
z im UTF-8 Format in einen Python-String umzuwandeln, kann man folgenden
Befehl verwenden: z.decode(“UTF-8”)
</details>

``` python
# Lösung 1: mit Schleifen

from urllib.request import urlopen
import string

URL = "https://math-inf.uni-greifswald.de/storages/uni-greifswald/fakultaet/mnf/mathinf/hellmuth/Teaching/AlgorDatastrWS1819/Goethe--Faust.txt"

# Lösung:
worte = []
for z in urlopen(URL):
    zeile = z.decode("UTF-8")
    for wort in zeile.split():
        worte.append(wort.strip(string.punctuation))

print("Der 'Faust' enthält", len(worte), "Wörter und beginnt so:")
print(worte[:20])
```

    Der 'Faust' enthält 31161 Wörter und beginnt so:
    ['Goethe', 'Faust', 'Johann', 'Wolfgang', 'von', 'Goethe', 'Faust', 'Eine', 'Tragödie', 'Erster', 'Theil', 'Einleitende', 'Angaben', 'Zueignung', 'Ihr', 'naht', 'euch', 'wieder', 'schwankende', 'Gestalten']

``` python
# Lösung 2: mit List Comprehension

from urllib.request import urlopen
import string

URL = "https://math-inf.uni-greifswald.de/storages/uni-greifswald/fakultaet/mnf/mathinf/hellmuth/Teaching/AlgorDatastrWS1819/Goethe--Faust.txt"

# Lösung: 
zeilen = [z.decode("UTF-8") for z in urlopen(URL)]
worte = [wort.strip(string.punctuation) for zeile in zeilen for wort in zeile.split()]

print("Der 'Faust' enthält", len(worte), "Wörter und beginnt so:")
print(worte[:20])
```

    Der 'Faust' enthält 31161 Wörter und beginnt so:
    ['Goethe', 'Faust', 'Johann', 'Wolfgang', 'von', 'Goethe', 'Faust', 'Eine', 'Tragödie', 'Erster', 'Theil', 'Einleitende', 'Angaben', 'Zueignung', 'Ihr', 'naht', 'euch', 'wieder', 'schwankende', 'Gestalten']

# Funktionen


Links: - [Erklärungen und interaktive Beispiele zu *Funktionen* bei
w3schools.com](https://www.w3schools.com/python/python_functions.asp)

#### Einfache Unterprogramme ohne Parameter und Rückgabewert

Das Schlüsselwort `def` leitet eine Funktionsdefinition ein. Der Körper
der Funktion muss eingerückt werden

``` python
def unterprogramm():
    print("Ein Hund lief in die Küche")
    print("und stahl dem Koch ein Ei.")
    print("Da nahm der Koch den Löffel")
    print("und schlug den Hund zu Brei.")
    print()
    
# Text wieder ausgerückt --> wir sind wieder außerhalb von der Funktion
unterprogramm()
```

    Ein Hund lief in die Küche
    und stahl dem Koch ein Ei.
    Da nahm der Koch den Löffel
    und schlug den Hund zu Brei.

``` python
for i in range(3):
    unterprogramm()
```

    Ein Hund lief in die Küche
    und stahl dem Koch ein Ei.
    Da nahm der Koch den Löffel
    und schlug den Hund zu Brei.

    Ein Hund lief in die Küche
    und stahl dem Koch ein Ei.
    Da nahm der Koch den Löffel
    und schlug den Hund zu Brei.

    Ein Hund lief in die Küche
    und stahl dem Koch ein Ei.
    Da nahm der Koch den Löffel
    und schlug den Hund zu Brei.

#### Unterprogramme mit Parameter

Auch Parameter müssen nicht mit Datentyp deklariert werden.

``` python
def begruesse(name):
    print("Hallo", name)
```

``` python
namen = ["Andrea", "Jürgen", "Michael"]
for name in namen:
    begruesse(name)
```

    Hallo Andrea
    Hallo Jürgen
    Hallo Michael

#### Funktionen mit Parameter und Rückgabewert

``` python
def verdopple(zahl):
    return zahl * 2

# Heutzutage auch mit Typangaben möglich
def verdopple(zahl: int) -> int:
    return zahl * 2
```

``` python
verdopple(21)
```

    42

##### Ein weiteres Beispiel zu Funktion mit Parameter und Rückgabewert

``` python
def max_liste(my_list):
    """liefert den größten in der Liste my_list enthaltenen Wert zurück.
    Achtung: Bisher wird der Spezialfall, dass my_list leer ist, nicht berücksichtigt."""
    max = my_list[0]
    for i in range(1,len(my_list)):
        if my_list[i] > max:
            max = my_list[i]
    return max

# Bsp:
liste_a = [1, 12, -5, -23, 19, 13, 0, -7]
print("Der größte Wert in der Liste ist: ", max_liste(liste_a))
```

    Der größte Wert in der Liste ist:  19

**Anmerkung:** Natürlich ist `max()` standardmäßig in Python bereits
vorhanden - schließlich sind bei Python für fast alle Bedürfnisse die
[“Batterien schon
dabei”](https://en.wikipedia.org/wiki/Batteries_Included#:~:text=Motto%20of%20the%20Python%20programming,parts%20required%20for%20full%20usability.).
Diese und viele weitere sogenannte “built-in function” findest du z.B.
auf [dieser
w3schools-Seite](https://www.w3schools.com/python/python_ref_functions.asp)
aufgelistet und erklärt.

``` python
max(liste_a)
```

    19

##### Dokumentation von Funktionen mit Docstrings

Alle Funktionen in der Python-Standardbibliotheken sind ausführlich
dokumentiert. Auf die Dokumentation kann man auf verschiedene Arten
zugreifen:

-   help()
-   in Jupyter: funktionsname?
-   in Jupyter: in der Kontexthilfe (Strg-i)

``` python
# Führe diese Zelle aus (Strg-Enter). Durch das Fragezeichen wird der 'Docstring' angezeigt
max_liste?
```

    Signature: max_liste(my_list)
    Docstring:
    liefert den größten in der Liste my_list enthaltenen Wert zurück.
    Achtung: Bisher wird der Spezialfall, dass my_list leer ist, nicht berücksichtigt.
    File:      d:\nextcloud\lehrerfortbildung-bw.de\python-vorstellung\jupyter-python-lfb-dez2020\<ipython-input-1-a1c84f06ac95>
    Type:      function

``` python
# Das funktioniert auch mit selbstdefinierten Funktionen, wenn diese einen Docstring definiert haben
help(max_liste)   # alternativ: max_liste?
```

    Help on function max_liste in module __main__:

    max_liste(my_list)
        liefert den größten in der Liste my_list enthaltenen Wert zurück.
        Achtung: Bisher wird der Spezialfall, dass my_list leer ist, nicht berücksichtigt.

#### Rekursion

``` python
def fakultaet(n):
    if n < 2:
        return 1
    else:
        return n * fakultaet(n-1)
```

``` python
fakultaet(6)
```

    720

### Einige Python-Besonderheiten

#### Default-Argumente für Parameter

``` python
def begruesse(nachname, anrede="Frau"):
    print("Hallo", anrede, nachname)
    
# Wenn die Reihenfolge der Parameter beim Aufruf beachtet wird, kann auf den Variablennamen verzichtet werden     
begruesse("Schmidt", "Herr")
begruesse("Meier")

begruesse(nachname="Müller", anrede="Präsident")

# Parameter können beim Aufruf von Unterprogrammen auch mit Variablennamen bedient werden
```

    Hallo Herr Schmidt
    Hallo Frau Meier
    Hallo Präsident Müller

#### Positionale vs Keyword-Argumente

*Beispiel:* Was passiert wohl beim folgenden Funktionsaufruf?  
`zeichne_kreis(100, 100, 50, 0, 100, 255)`?

Die Bedeutung dieses Aufrufs erschließt sich nur, wenn man weiß, welche
Parameter die Funktion `zeiche_kreis()` hat und in welcher *Reihenfolge*
diese erwartet werden. D.h. obwohl die Zahl 100 in diesem
Funktionsaufruf dreimal vorkommt, hat sie je nach *Position* in der
Argumentliste eine andere Bedeutung.

In Python kann man beim Aufruf von Funktionen nicht nur die *Werte*,
sondern auch die *Variablennamen* der Parameter angegeben (Fachbegriff:
Keyword-Arguments). Wenn eine Funktion *viele* Parameter hat, kann es
die Lesbarkeit des Codes deutlich erhöhen, nicht nur die Argumente,
sondern auch die zugehörigen Parameternamen zu nennen.

Mit Keyword-Argumenten sieht obige Aufruf so aus:  
`zeichne_kreis(x=100, y=100, radius=50, rot=0, gruen=100, blau=255)`

Damit bekommt der Leser des Codes schon einen viel besseren Hinweis
darauf, was der Funktionsaufruf bezweckt.

**Wichtig:** Da bei der Verwendung von Keyword-Argumenten immer klar
ist, welches Argument welchem Parameter zugewiesen werden soll, darf man
die Reihenfolge der Argumente sogar verändern!

``` python
def beschreibe_tier(name, tierart, ist_weiblich):
    pronomen = "Meine" if ist_weiblich else "Mein"    # if als Ausdruck, der einen Wert zurückliefert
    print(pronomen, tierart, "heißt", name)
    
beschreibe_tier("Struppi", "Hund", False)    # Was war nochmal die Bedeutung des bool-Parameters?
beschreibe_tier("Mimi", "Katze", ist_weiblich=True)   # Viel leichter verständlich!

beschreibe_tier(tierart="Giraffe", ist_weiblich=True, name="Gisela")   # Bei keyword-Arguments ist die Reihenfolge egal - der Parametername macht ja alles klar!
```

    Mein Hund heißt Struppi
    Meine Katze heißt Mimi
    Meine Giraffe heißt Gisela

##### Keyword- und Default-Argumente kombinieren

Besonders hilfreich ist die *Kombination* von Keyword- und
Default-Argumenten. Man kann beim Aufruf einer Funktion auf beliebige
Default-Argumente verzichten und gleichzeitig durch explizite
Keyword-Argument klar machen, welche Argumente gesetzt werden sollen.

Diese Vorgehensweise ersetzt einen Großteil der Anwendungsfälle für das
*Überladen* von Funktionen in anderen Programmiersprachen.

``` python
def beschreibe_kreis(x=0, y=0, radius=10, rot=0, gruen=0, blau=0):
    h = f"{rot:02X}{gruen:02X}{blau:02X}"  # just for fun: Umrechnen in Hexadezimalcode
    print(f"ein Kreis mit Mittelpunkt ({x}|{y}), Radius {radius}, RGB-Farbe: #{h}")
    
beschreibe_kreis(x=10, y=10, radius=20)
beschreibe_kreis(y=30, radius=100, blau=100)
beschreibe_kreis(x=30, radius=100, rot=100, gruen=200)
beschreibe_kreis(20, 30, gruen=133, radius=3)
beschreibe_kreis(20, 30, 100, 200, 0)   # Das kommt dir inzwischen furchbar unleserlich vor? Gut!
```

    ein Kreis mit Mittelpunkt (10|10), Radius 20, RGB-Farbe: #000000
    ein Kreis mit Mittelpunkt (0|30), Radius 100, RGB-Farbe: #000064
    ein Kreis mit Mittelpunkt (30|0), Radius 100, RGB-Farbe: #64C800
    ein Kreis mit Mittelpunkt (20|30), Radius 3, RGB-Farbe: #008500
    ein Kreis mit Mittelpunkt (20|30), Radius 100, RGB-Farbe: #C80000

Übrigens können wir in Jupyter solche Kreise auch direkt als SVG-Formen
zeichnen:

``` python
from IPython.display import SVG

def zeichne_kreis(x, y, radius=10, rot=0, gruen=0, blau=0):
    h = f"{rot:02X}{gruen:02X}{blau:02X}"  # just for fun: Umrechnen in Hexadezimalcode
    svg_str = f'''<svg width="600" height="80"> <circle cx="{x}" cy="{y}" r="{radius}" fill="#{h}"> </circle></svg>'''
    # print(svg_str)
    return SVG(svg_str)

# Ändere einige der folgenden Funktionsargumente. Was passiert bei der Ausführung?
zeichne_kreis(50, 40, blau=133, rot=200, radius=30)
```

![](05T%20-%20Funktionen_files/figure-markdown_strict/cell-17-output-1.svg)

#### Funktionen mit mehreren Rückgabewerten

Sehr nützlich: Python-Funktionen können *mehrere* Werte auf einmal
zurückliefern.

``` python
def div_and_mod(x,y):
    a = x // y
    b = x % y
    return a, b

z = 17
n = 5
ergebnis, rest = div_and_mod(z, n)  
print(f"{z} / {n} = {ergebnis} Rest {rest}")
```

    17 / 5 = 3 Rest 2

Wie das funktioniert sieht man in der untenstehenden Version desselben
Beispiels: - Die Rückgabewerte werden automatisch in (1) zu einem
**Tupel** zusammengefasst. (So gesehen gibt es eigentlich nur einen
Rückgabewert.) - Dieses Tupel wird in (2) *destrukturiert*, d.h. die
beiden im Tupel gespeicherten Werte werden den beiden neuen Variablen
zugewiesen

``` python
def div_and_mod(x,y):
    a = x // y
    b = x % y
    return (a,b)  # (1) a und b zu einem Tupel zusammenfassen

(ergebnis, rest) = div_and_mod(17,5)   # (2) Zurückgegebenes Tupel wird in zwei Variablen "destrukturiert"
print('17 / 5 = ',ergebnis, "R",rest )
```

    17 / 5 =  3 R 2

``` python
# Übrigens: Es gibt (natürlich!) bereits eine Funktion, die das Ergebnis einer Ganzzahldivision mit Rest liefert:
ergebnis, rest = divmod(17,5)
print(f"{z} / {n} = {ergebnis} Rest {rest}")
```

    17 / 5 = 3 Rest 2

### Teaser: Funktionen höherer Ordnung *(nicht Thema dieses Kurses)*

Funktionen sind in Python ganz normale *Objekte*, deshalb können sie in
Variablen gespeichert, in Listen gesammelt oder auch selbst als Argument
einer anderen Funktion verwendet werden.

``` python
# Beispiel: Zwei sehr einfache Funktionen

def sage_hallo():
    print("Hallo")
    
def begruesse_zufaellig():
    from random import choice
    begruessungen = "Hi Servus Tach Moin Mahlzeit Ciao".split()
    begruessung = choice(begruessungen)
    print(begruessung)
    
f1 = sage_hallo   # Eine andere Referenz auf dasselbe Funktionsobjekt
f2 = begruesse_zufaellig

f1()    # Klammern hinter dem Variablennamen = Aufrufen (funktioniert auch über die neue Referenz)

funktionen = [f1, f2]   # Eine Liste voller Funktionsreferenzen

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
    Tach

In Programmen müssen oft Befehle eine bestimmte Anzahl von Malen
wiederholt werden. Die meisten Programmiersprachen bieten dafür keinen
eigenen Schleifentyp. In Python z.B. muss man über ein `range`
iterieren - für Anfänger verwirrend wie die Schreibweise
`for(int i; i < n; i++` in von C abgeleiteten Sprachen.

Könnte man nicht eine Wiederholungsschleife *selbst* programmieren?

``` python
def wiederhole(anzahl, eine_funktion):    # Die Funktion erhält eine andere Funktion als Parameter
    for i in range(anzahl):
        eine_funktion()   # Hier wird die übergebene Funktion ausgeführt
        
wiederhole(3, sage_hallo)  
print("----------")
wiederhole(7, begruesse_zufaellig)
```

    Hallo
    Hallo
    Hallo
    ----------
    Hi
    Tach
    Moin
    Ciao
    Servus
    Hi
    Hi

``` python
import random

funktionen = [sage_hallo, begruesse_zufaellig]   # Eine Liste voller Funktionen
eine_funktion = random.choice(funktionen)   # Eine Variable, die eine Funktion enthält
n = random.randint(1, 6)
print(f"Die zufällig ausgewählte Funktion {eine_funktion.__name__} wird {n}-mal ausgeführt:")
wiederhole(n, eine_funktion)
```

    Die zufällig ausgewählte Funktion sage_hallo wird 3-mal ausgeführt:
    Hallo
    Hallo
    Hallo

# Vererbung


<img src="images/Vererbung1.png">

Da die Klasse `Vehicles` sehr weit gefasst ist müssen wir einige
speziellere Klassen definieren.  
Die spezialisierten Klassen sind die Unterklassen. Die Klasse `Vehicles`
wird eine Oberklasse für sie alle sein.

Alle existierenden Fahrzeuge (und solche, die es noch nicht gibt) sind
durch ein einziges, wichtiges Merkmal miteinander verbunden: die
Fähigkeit, sich zu bewegen.  
**Hinweis:**  
Die Hierarchie wächst von oben nach unten, wie Baumwurzeln, nicht wie
Äste. Die allgemeinste und umfangreichste Klasse befindet sich immer an
der Spitze (die Oberklasse auch Superklasse genannt), während sich ihre
Nachkommen darunter befinden (die Unterklassen auch Subklassen genannt).

**Noch ein Beispiel mit Vererbung:**

<img src="images/Vererbung2.png">

Alle Tiere (unsere Superklasse Animals) lassen sich in fünf Unterklassen
unterteilen: Säugetiere, Reptilien, Vögel, Fische und Amphibien.

Säugetiere lassen sich wiederum in wilde Säugetiere und domestizierte
Säugetiere einteilen.

**Das Konzept der Vererbung**

<img src="images/Vererbung3.png">

Jedes Objekt, das an eine bestimmte Ebene einer Klassenhierarchie
gebunden ist, erbt alle Eigenschaften und Fähigkeiten, die innerhalb
einer der Oberklassen definiert sind. Wird die Stammklasse erweitert,
dann wird dies auch an alle Unterklassen vererbt.  
Jede Unterklasse ist spezifischer als ihre Oberklasse.  
Umgekehrt ist jede Oberklasse allgemeiner als jede ihrer Unterklassen.

### Was hat ein Objekt

-   ein Objekt hat einen Namen (name), der es innerhalb seines
    Namesspace eindeutig identifiziert (obwohl es auch einige anonyme
    Objekte geben kann)
-   ein Objekt hat eine Reihe von individuellen Eigenschaften
    (properties), die es originell, einzigartig oder herausragend machen
    (obwohl es möglich ist, dass einige Objekte überhaupt keine
    Eigenschaften haben)
-   ein Objekt hat einen Satz von Fähigkeiten (activities), um bestimmte
    Aktivitäten durchzuführen, die das Objekt selbst oder einige der
    anderen Objekte verändern können.

<img src="images/Vererbung4.png">

## Vererbung - warum und wie?

Sehen wir uns nachfolgenden Code an. Beim Ausgeben der Referenz auf ein
Sonnen-Objekt wird die `__str__()` von Stern aufgerufen. Da diese nicht
existiert wird automatisch die von `Objekt` geerbte Methode genutzt.  
Wie Sie sehen können, ist der Ausdruck hier nicht wirklich nützlich, und
etwas Spezifischeres oder einfach Hübscheres wäre vielleicht besser.

``` python
class Stern:
    def __init__(self, name, galaxy):
        self.name = name
        self.galaxy = galaxy

sonne = Stern("Sonne", "Milchstraße")
print(sonne)
```

Deshalb sollte die Standardmethode `__str__()` in jeder Klasse sinnvoll
überschrieben werden.

``` python
class Stern:
    def __init__(self, name, galaxy):
        self.name = name
        self.galaxy = galaxy
    def __str__(self):
        return self.name + ' in der Galaxy ' + self.galaxy

sonne = Stern("Sonne", "Milchstraße")
print(sonne)
```

Der Begriff Vererbung ist älter als die Computerprogrammierung und
beschreibt die gängige Praxis,  
verschiedene Güter von einer Person auf eine andere zu übertragen, wenn
diese Person stirbt. Im Zusammenhang mit der Computerprogrammierung hat
der Begriff eine ganz andere Bedeutung. \## Das Konzept der Vererbung

Vererbung ist eine gängige Praxis (in der objektorientierten
Programmierung), Attribute und Methoden von bereits existierenden
Oberklasse an eine neu erstellte Klasse, die Unterklasse, weiterzugeben.

Mit anderen Worten: Vererbung ist ein Weg, eine neue Klasse zu
erstellen, und zwar nicht von Grund auf, sondern unter Verwendung eines
bereits definierten Repertoires von Merkmalen. Die neue Klasse erbt (und
das ist der Schlüssel) alle bereits existierenden Eigenschafte, ist aber
in der Lage, bei Bedarf einige neue hinzuzufügen.

Dadurch ist es möglich, spezialisiertere (konkretere) Klassen zu
erstellen, die vordefinierte allgemeine Methoden und Attribute (von der
Oberklasse) verwenden.

#### Ein einfaches Beispiel für eine zweistufige Vererbung

``` python
class Fahrzeug:
    pass

class LandFahrzeug(Fahrzeug):
    pass

class Kettenfahrzeug(LandFahrzeug):
    pass
```

Auch wenn die Klassen zunächst ohne Inhalt realisiert wurden können wir
folgendes aussagen: - Die Klasse Fahrzeug ist die Oberklasse für die
beiden Klassen LandFahrzeug und Kettenfahrzeug - Die Klasse LandFahrzeug
ist eine Unterklasse von Fahrzeug und gleichzeitig eine Oberklasse von
Kettenfahrzeug; - Die Klasse Kettenfahrzeug ist eine Unterklasse sowohl
der Klasse Fahrzeug als auch der Klasse LandFahrzeug.

Vererbung wird in Python verwirklicht, in dem die Oberklasse(n) dem
Klassen-Namen in Klammern hinten angestellt wird.

## Vererbungsbeziehung erkennen mit `issubclass(ClassOne, ClassTwo)`

Python bietet eine Funktion, mit der überprüft werden kann, ob eine
bestimmte Klasse eine Unterklasse einer anderen Klasse ist.  
Es gibt eine wichtige Beobachtung zu machen: **Jede Klasse wird als
Unterklasse von sich selbst betrachtet.**

``` python
class Fahrzeug:
    pass
class LandFahrzeug(Fahrzeug):
    pass
class Kettenfahrzeug(LandFahrzeug):
    pass

print("Fahrzeug ist Unterklasse von object:",issubclass(Fahrzeug,object))

classes = [Fahrzeug,LandFahrzeug,Kettenfahrzeug]
print("\t",[cName.__name__ for cName in classes])

for cls1 in classes:
    print(cls1.__name__,end="\t")
    for cls2 in classes:
        print(issubclass(cls1, cls2), end="\t")
    print()
```

## `isinstance(Objektname, Klassenname)`

Wie wir bereits wissen, werden Objekte mit dem Bauplan der Klasse
hergestellt.  
Es kann entscheidend sein, ob ein Objekt bestimmte Eigenschaften hat
(oder nicht hat). Mit anderen Worten, ob es ein Objekt einer bestimmten
Klasse ist oder nicht.  
Dies lässt sich durch Aufruf der eingebaute Funktion `isinstance()`
feststellen.’

Diese Funktion gibt True zurück, wenn das Objekt eine Instanz der Klasse
(oder eine Instanz von einer der Oberklassen) ist, andernfalls False.

``` python
class Fahrzeug:
    pass
class LandFahrzeug(Fahrzeug):
    pass
class Kettenfahrzeug(LandFahrzeug):
    pass

myFahrzeug = Fahrzeug()
myLandFahrzeug = LandFahrzeug()
myKettenfahrzeug = Kettenfahrzeug()

for obj in [myFahrzeug, myLandFahrzeug, myKettenfahrzeug]:
    for cls in [Fahrzeug,LandFahrzeug,Kettenfahrzeug]:
        print(isinstance(obj, cls), end="\t")
    print()
```

-   myFahrzeug ist Instanz von Fahrzeug; jedoch nicht von Landfahrzeug
    und auch nicht von Kettenfahrzeug
-   myLandFahrzeug ist Instanz von Fahrzeug und von Landfahrzeug; jedoch
    nicht von Kettenfahrzeug
-   myKettenfahrzeug ist Instanz von Fahrzeug, von Landfahrzeug und von
    Kettenfahrzeug

## Der `is`-Operator

Der is-Operator prüft, ob zwei Variablen (hier one und object_two) auf
dasselbe Objekt verweisen.  
Zur Erinnerung: Variablen speichern Objekte nicht selbst sondern sind
lediglich Verweise die auf den internen Python-Speicher zeigen. Das
Zuweisen eines Wertes einer Objektvariablen an eine andere Variable
kopiert nicht das Objekt, sondern nur dessen Verweis. Mit `is` kann
überprüft werden ob zwei Objektvariablen auf das gleiche Objekt zeigen.

#### Programmbeispiel mit dem `is` Operator

``` python
class Person:
    def __init__(self, name,alter):
        self.name = name
        self.alter = alter

tom = Person('Tom',20)
jerry = Person('Jerry',17)
other_tom = tom
other_tom.alter += 1

print(tom is jerry)
print(jerry is other_tom)
print(other_tom is tom)

print(tom.name, tom.alter)
print(jerry.name, jerry.alter)
print(other_tom.name, other_tom.alter)
```

## Noch ein Beispiel mit dem `is` Operator¶

Strings können identische Inhalte haben, müssen jedoch nicht gleich
sein.  
Im unten stehenden Beispiel gleichen sich zwar die Zeichenketten. Es
handelt sich jedoch um unterschiedliche Objekte.

``` python
string_1 = "Mary had a little "
string_1 += "lamb"
string_2 = "Mary had a little lamb"

print(string_1 == string_2, string_1 is string_2)
```

### Methoden aus der Oberklasse überschreiben

Passt eine geerbte Methode nicht, können wir diese in der Unterklasse
einfach überschreiben. Hierfür muss in der Unterklasse eine Methode mit
exakt dem gleichen Namen erzeugt werden! Diese überdeckt beim Aufruf die
Methode der Oberklasse und wird stattdessen ausgeführt.

Die Funktion `super()` erzeugt einen Kontext, in dem Sie das Argument
self nicht an die aufgerufene Methode übergeben müssen (und auch nicht
dürfen) - deshalb ist es möglich, den Konstruktor der Superklasse mit
nur einem Argument (der Name für die Person) zu bedienen.

Der Zugriff auf Methoden der Super-Klasse kann auch über den
Klassennamen der Superklasse erfolgen. Dann wird allerdings zusätzlich
als erster Parameter die Referenz auf `self` benötigt.

**Hinweis:** Sie können diesen Mechanismus nicht nur verwenden, um den
Konstruktor der Oberklasse aufzurufen, sondern auch, um Zugriff auf alle
in der Oberklasse verfügbaren Ressourcen zu erhalten.

``` python
class Person:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return "Mein Name Name ist " + self.name

class Student(Person):
    def __init__(self, name, studiengang):
        super().__init__(name)
        # alternativ:
        # Person.__init__(self, name)
        self.studiengang = studiengang
        
    def __str__(self):
        # return super().__str__() + " und ich studiere  " + self.studiengang
        # alternativ:
        return Person.__str__(self) + " und ich studiere  " + self.studiengang

obj = Student("Andy","Informatik")

print(obj)
```

### Zugriff auf Methoden und Attribute bei Vererbungsbeziehungen

Dies soll am unten stehenden Beispiel in einer dreistufigen
Vererbungslinie demonstriert werden.

Wenn wir auf Methoden oder Attribute eines Objekts zuzugreifen, wird
Python versuchen (in dieser Reihenfolge): - diese innerhalb des Objekts
selbst zu finden; - es in allen Klassen zu finden, die an der
Vererbungslinie des Objekts von unten nach oben beteiligt sind; - Wenn
beide Versuche fehlschlagen, wird eine Ausnahme (AttributeError)
ausgelöst.

Wir beziehen uns hier auf die Einfachvererbung, wenn eine Unterklasse
genau eine Oberklasse hat.  
Dies ist die häufigste Situation (und auch die empfohlene).

``` python
class Level1:
    variable_1 = 100
    def __init__(self):
        self.var_1 = 101
    def fun_1(self):
        return 102

class Level2(Level1):
    variable_2 = 200
    def __init__(self):
        super().__init__()
        self.var_2 = 201
    def fun_2(self):
        return 202

class Level3(Level2):
    variable_3 = 300
    def __init__(self):
        super().__init__()
        self.var_3 = 301
    def fun_3(self):
        return 302

obj = Level3()

print(obj.variable_1, obj.var_1, obj.fun_1())
print(obj.variable_2, obj.var_2, obj.fun_2())
print(obj.variable_3, obj.var_3, obj.fun_3())
```

## Mehrfachvererbung

Mehrfachvererbung tritt auf, wenn eine Klasse mehr als eine Oberklasse
hat. Syntaktisch wird eine solche Vererbung als kommagetrennte Liste von
Superklassen dargestellt, die in Klammern hinter dem neuen Klassennamen
steht - so wie hier:

Die Klasse Sub hat zwei Superklassen: SuperA und SuperB. Das bedeutet,
dass die Sub-Klasse alle Methoden und Attribute erbt, die sowohl von
SuperA als auch von SuperB angeboten werden.

``` python
class SuperA:
    var_a = 10
    def fun_a(self):
        return 11

class SuperB:
    var_b = 20
    def fun_b(self):
        return 21

class Sub(SuperA, SuperB):
    pass

obj = Sub()

print(obj.var_a, obj.fun_a())
print(obj.var_b, obj.fun_b())
```

## Welche Methoden und Attribute werden ausgewählt, wenn diese von mehreren Oberklassen angeboten werden?

In unten stehendem Beispiel erkennen wir, dass die Klasse `Left` und die
Klasse `Right` die Klassenvariable `var` und die Methode `fun()` haben.
Welche werden nun genutzt, wenn eine **`Sub`-Klasse von `Left` und von
`Right` erbt?**

Aus der Ausgabe des Programms lässt sich erkennen, dass die geerbten
Klassen von links nach rechts nach vorhandenden Variablen und Methoden
durchsucht werden.  
Welche Ausgabe ist zu erwarten bei `class Sub(Left, Right)`?

Es besteht kein Zweifel, dass die Klassenvariable var_right von der
Klasse Right stammt, und var_left von Left.

``` python
class Left:
    var = "L"
    var_left = "LL"
    def fun(self):
        return "Left"

class Right:
    var = "R"
    var_right = "RR"
    def fun(self):
        return "Right"

class Sub(Left, Right):
    pass

obj = Sub()

print(obj.var, obj.var_left, obj.var_right, obj.fun())
```

## Einfachvererbung vs. Mehrfachvererbung

Wie Sie bereits wissen, steht der Verwendung von Mehrfachvererbung in
Python nichts im Wege. Sie können jede neue Klasse von mehr als einer
zuvor definierten Klasse ableiten.

Es gibt nur ein “aber”. Die Tatsache, dass Sie es tun können, bedeutet
nicht, dass Sie es tun müssen.

**Vergessen Sie das nicht:** - Eine einzelne Vererbungsklasse ist immer
einfacher, sicherer und leichter zu verstehen und zu warten; -
Mehrfachvererbung ist immer riskant, da Sie viel mehr Möglichkeiten
haben, einen Fehler bei der Identifizierung der Teile der Oberklassen zu
machen, die die neue Klasse effektiv beeinflussen; - Mehrfachvererbung
kann das Überschreiben extrem kompliziert machen; außerdem wird die
Verwendung der super()-Funktion mehrdeutig; - Mehrfachvererbung verstößt
gegen das Prinzip der einzigen Verantwortung (mehr Details hier:
https://en.wikipedia.org/wiki/Single_responsibility_principle), da es
eine neue Klasse aus zwei (oder mehr) Klassen macht, die nichts
übereinander wissen; - Verwenden Sie Mehrfachvererbung als letzte aller
möglichen Lösungen - wenn Sie wirklich die vielen verschiedenen
Funktionalitäten benötigen, die von verschiedenen Klassen angeboten
werden, kann Komposition eine bessere Alternative sein.

## Komposition

Die Klasse `Vehicle` weiß eigentlich, wie zu drehen ist, aber das
eigentliche Drehen wird von einem spezialisierten Objekt durchgeführt,
das in einer Eigenschaft namens `controller` gespeichert ist. Der
Controller ist in der Lage, das Fahrzeug zu steuern, indem er die
entsprechenden Teile des Fahrzeugs manipuliert.

Es gibt zwei Klassen namens `Tracks` und `Wheels` - sie wissen, wie man
die Richtung des Fahrzeugs steuert. Außerdem gibt es eine Klasse namens
`Vehicle`, die jeden der verfügbaren Controller verwenden kann (die
beiden bereits definierten oder jeden anderen, der in Zukunft definiert
wird) - der Controller selbst wird der Klasse bei der Initialisierung
übergeben.

Auf diese Weise wird die Fähigkeit des Fahrzeugs, sich zu drehen, über
ein externes Objekt realisiert, das nicht innerhalb der Klasse `Vehicle`
implementiert ist.

Mit anderen Worten, wir haben ein universelles Fahrzeug und können es
entweder mit Ketten oder Rädern ausstatten.

``` python
import time

class Tracks: # Ketten
    def change_direction(self, left, on):
        print("tracks: ", left, on)

class Wheels: # Räder
    def change_direction(self, left, on):
        print("wheels: ", left, on)

class Vehicle:
    def __init__(self, controller):
        self.controller = controller

    def turn(self, left):
        self.controller.change_direction(left, True)
        time.sleep(0.25)
        self.controller.change_direction(left, False)


wheeled = Vehicle(Wheels())  # Fahrzeug mit Rädern
tracked = Vehicle(Tracks())  # Fahrzeug mit Ketten

wheeled.turn(True)
tracked.turn(False)
```

## Method Resolution Order (MRO)

MRO ist im Allgemeinen eine Methode (man kann es auch eine Strategie
nennen), mit der eine bestimmte Programmiersprache den oberen Teil der
Hierarchie einer Klasse durchsucht, um die Methode zu finden, die sie
gerade benötigt. Es ist erwähnenswert, dass verschiedene Sprachen leicht
(oder sogar komplett) unterschiedliche MROs verwenden. Python ist in
dieser Hinsicht jedoch ein einzigartiges Wesen, und seine
Gepflogenheiten sind ein wenig speziell.

Die Reihenfolge, die wir versucht haben zu erzwingen (Top, Middle) ist
inkompatibel mit dem Vererbungspfad, der sich aus der Struktur des Codes
ergibt. Python wird das nicht mögen. Was zu folgender Fehlermeldung
führt.

**TypeError: Cannot create a consistent method resolution order (MRO)
for bases Top, Middle**

Diese Fehlermeldung spricht für sich!!<br> Pythons MRO kann nicht
verändert oder missachtet werden, nicht nur, weil das die Art und Weise
ist, wie Python funktioniert, sondern auch, weil es eine Regel ist, die
Sie befolgen müssen.

``` python
class Top:
    def m_top(self):
        print("top")

class Middle(Top):
    def m_middle(self):
        print("middle")

# würde wie erwartet funktionieren
# class Bottom(Middle):
# so was geht auch noch
# class Bottom(Middle,Top):
# was macht aber ??
class Bottom(Top, Middle):
    def m_bottom(self):
        print("bottom")

object = Bottom()
object.m_bottom()
object.m_middle()
object.m_top()
```

## diamond problem

Das “Diamant Problem” ist ein klassisches Problem der Mehrfachvererbung,
welches sich in der Form des Vererbungsdiagramms verdeutlicht.

<img src="images/diamondproblem.png">

-   Es gibt die oberste Superklasse namens A;
-   es gibt zwei Unterklassen, die von A abgeleitet sind: B und C;
-   und es gibt auch die unterste Unterklasse namens D, die von B und C
    abgeleitet ist (oder C und B, da diese beiden Varianten in Python
    unterschiedliche Dinge bedeuten)

``` python
class A:
    pass

class B(A):
    pass

class C(A):
    pass

class D(B, C):
    pass

d = D()
```

#### Welche der beiden m_middle()-Methoden wird tatsächlich aufgerufen, wenn die folgende Zeile ausgeführt wird?

`object.m_middle()`

Sie brauchen sich nicht zu beeilen - denken Sie gut nach und behalten
Sie Pythons MRO im Hinterkopf!

<details>
<summary>
Hier klicken für Tipps:
</summary>
Die Erklärung ist einfach: Die Klasse Middle_Left ist in der
Vererbungsliste der Klasse Bottom vor Middle_Right aufgeführt.<br>Wenn
Sie sichergehen wollen, dass es keinen Zweifel gibt, versuchen Sie,
diese beiden Klassen in der Liste zu vertauschen und überprüfen Sie die
Ergebnisse.
</details>

``` python
class Top:
    def m_top(self):
        print("top")

class Middle_Left(Top):
    def m_middle(self):
        print("middle_left")

class Middle_Right(Top):
    def m_middle(self):
        print("middle_right")

class Bottom(Middle_Left, Middle_Right):
    def m_bottom(self):
        print("bottom")

object = Bottom()
object.m_bottom()
object.m_middle()
object.m_top()
```

## <font color=red >Übung: Realisieren Sie zwei Klassen mit Vererbungsbeziehung nach Wahl.</font>

-   Implementieren Sie in den Klassen sinnvoll die Methode
    `__str__(self)`
-   Testen Sie ihre Klassen

Optional: - Nutzen Sie in der `__init__()` Methode default-Parameter -
Kapseln Sie die Attribute - Schützen Sie die Attribute in den
setter-Methoden vor unzulässigen Werten

``` python
# Insert Code here
```

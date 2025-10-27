# Klassen und Objekte


## In Python ist alles ein Objekt!

Python ist eine durch und durch objektorientierte Sprache - allerdings
funktioniert manches bei einer *dynamischen* Sprache etwas anders, als
man es vielleicht von Java oder C# gewohnt ist.

``` python
# In Python ist alles ein Objekt! Hier ein paar Beispiele:

name = "Tina"  # Ein String ist ein Objekt
print(name.upper())  # Methode upper() des String-Objekts name wird aufgerufen

namen = ["Anna", "Berta", "Carla", "David"]   # Eine Liste ist ein Objekt
namen.append("Eva")  # Methode append() des Listen-Objekts namen wird aufgerufen
print(namen)


# Achtung: auch Zahlen sind Objekte
zahl = 0.375  # Eine Gleitkommazahl ist ein Objekt
zaehler, nenner = zahl.as_integer_ratio()  # Methode as_integer_ratio() des Integer-Objekts zahl wird aufgerufen
print(f"Zahl: {zahl} als Bruch: {zaehler}/{nenner}")
print(nenner.is_integer())  # auch zaehler und nenner sind Objekte


# Es wird noch besser: auch Funktionen sind Objekte!
def eine_funktion():
    """Diese Funktion kann nicht viel, aber immerhin ist sie gut dokumentiert"""
    print("Hallo Welt")

eine_funktion()  # So kennen wir das: Die Funktion wird aufgerufen
# Aber auch die Funktion ist ein Objekt und hat Attribute, zB speichert sie 
# ihren Docstring im Attribut __doc__
print(eine_funktion.__doc__)  
print(eine_funktion.__name__)  # und ihren Namen im Attribut __name__
print(eine_funktion.__repr__())  # Ganz irre: Wir rufen eine Methode des Funktion-Objekts auf!


# Nicht nur alleinstehende Funktionen sind Objekte, auch Methoden sind Objekte
eine_methode = namen.append  # Achtung: append wird hier nicht aufgerufen (deshalb fehlen die Klammern)
# sondern das Methoden-Objekt wird in der Variable eine_methode gespeichert
eine_methode("Frieda")  # Erst jetzt wird die Methode aufgerufen, d.h. Frieda wird an die Liste angehängt
print(namen[-1])  # Weil das letzte Element der Liste jetzt Frieda ist, wird "Frieda" ausgegeben

# Selbst Klassen sind Objekte!
class EineKlasse:
    """Eine Klasse, die nicht viel kann, aber immerhin gut dokumentiert ist"""
    ...   # Diese Klasse ist noch komplett leer

print(EineKlasse.__doc__)  # Der Docstring der Klasse
print(EineKlasse.__name__)  # Der Name der Klasse
print(EineKlasse.__module__)  # Der Name des Moduls, in dem die Klasse definiert wurde
print(EineKlasse.__bases__)  # Die Basisklassen (Oberklassen) der Klasse
```

    TINA
    ['Anna', 'Berta', 'Carla', 'David', 'Eva']
    Zahl: 0.375 als Bruch: 3/8
    True
    Hallo Welt
    Diese Funktion kann nicht viel, aber immerhin ist sie gut dokumentiert
    eine_funktion
    <function eine_funktion at 0x10b255d00>
    Frieda
    Eine Klasse, die nicht viel kann, aber immerhin gut dokumentiert ist
    EineKlasse
    __main__
    (<class 'object'>,)

## Eigene Klassen programmieren

-   Schlüsselwort `class`
-   Alles eingerückte gehört zur Klasse
-   Explizites self (vgl. this)
-   Empfehlung seit Python 3.5: Datentypen angeben!

### Eine einfache Klasse (noch ohne Attribute)

``` python
class Roboter:
    """Roboter-Klasse, noch ohne Attribute und Konstruktor"""

    def eine_methode(self) -> None:
        print("Hallo, ich bin ein Roboter")
        # return None

    def methode_mit_argument(self, text: str) -> None:
        print(f"Der Roboter sagt: {text}")

    def methode_mit_rueckgabewert(self) -> str:  # Diese Methode gibt einen String zurück
        return "Dieser Roboter ist sehr freundlich"
    
    def methode_mit_argument_und_rueckgabewert(self, text: str) -> str:  # Diese Methode gibt einen String zurück
        return text[::-1]  # Der Text wird umgedreht zurückgegeben
    
# Objekte erzeugen und Methoden aufrufen
roboter1 = Roboter()   # Achtung: kein `new` wie in Java!
roboter1.eine_methode()  # Methode wird aufgerufen: Punkt-Notation wie in den meisten objektorientierten Sprachen
roboter1.methode_mit_argument("Hallo Welt")  # Methode mit Argument
wert = roboter1.methode_mit_rueckgabewert()  # Methode mit Rückgabewert
print(wert)
wert = roboter1.methode_mit_argument_und_rueckgabewert("Hallo Welt")  # Methode mit Argument und Rückgabewert
print(wert)
```

    Hallo, ich bin ein Roboter
    Der Roboter sagt: Hallo Welt
    Dieser Roboter ist sehr freundlich
    tleW ollaH

### Attribute und Konstruktor

Das folgende Beispiel zeigt, wie in Python die **Attribute** einer
Klasse angelegt und in einem **Konstruktor** initialisiert werden.

``` python
class Roboter:
    def __init__(self, pName: str) -> None:  
        """Dies ist der Konstruktor der Klasse Roboter"""
        self.name: str = pName  # Attribut name wird auf den Wert des Parameters name gesetzt. Vgl. Java: this.name = name
        self.max_energie: int = 100  # Ein neues Attribut max_energie wird mit dem Wert 100 initialisiert
        self.energie = self.max_energie  # Angabe des Typs ist nicht notwendig, wird aber empfohlen

    def lade_energie(self, menge: int) -> None:
        self.energie += menge   # Attribute *müssen* mit self. angesprochen werden!
        if self.energie > self.max_energie:   # ja, immer!
            self.energie = self.max_energie   # Das ist evtl. etwas gewöhnungsbedürftig, hat aber seine Gründe
        print(f"Nach dem Laden habe ich {self.energie}/{self.max_energie} Energie.")  # s. Bemerkung 

    def verbrauche_energie(self, menge: int) -> None:
        self.energie -= menge
        if self.energie < 0:
            self.energie = 0
        print(f"Puh, das war anstrengend! Jetzt habe ich nur noch {self.energie}/{self.max_energie} Energie.")

    def stelle_dich_vor(self) -> None:
        print(f"Ich bin der Roboter {self.name} und habe gerade {self.energie}/{self.max_energie} Energie.")

# Objekte erzeugen und Methoden aufrufen
r2 = Roboter("R2D2")  # Nicht vergessen: kein `new`!
r2.stelle_dich_vor()
r2.verbrauche_energie(20)
r2.lade_energie(50)
```

    Ich bin der Roboter R2D2 und habe gerade 100/100 Energie.
    Puh, das war anstrengend! Jetzt habe ich nur noch 80/100 Energie.
    Nach dem Laden habe ich 100/100 Energie.

Die Rolle des Konstruktors aus anderen Sprachen übernimmt in Python die
Methode `__init__`. Sie wird automatisch aufgerufen, wenn ein neues
Objekt der Klasse erzeugt wird. D.h. der Aufruf
`roboter2 = Roboter("R2D2")` - erzeugt zuerst ein neues Objekt der
Klasse Roboter und - ruft dann die Methode `__init__` auf, wobei das neu
erzeugte Objekt als erstes Argument übergeben (d.h. dem Parameter *self*
zugeordnet) wird und das Argument “R2D2” als zweites (Parameter *name*).

Die Methode`__init__` kann dann z.B. die Attribute des Objekts
initialisieren oder andere Initialisierungsarbeiten durchführen - genau
wie der Konstruktor in anderen Sprachen.

## Randbemerkung für alle, die das explizite `self` stört!

Viele Umsteiger von Java & Co finden die Art und Weise, in der man in
Python Klassen definiert, zuerst “unschön”. Insbesondere werden häufig
diese Fragen gestellt:

> “Warum muss bei der Definitionen von (Instanzen-)Methoden `self` als
> erster Parameter explizit angegeben werden? Und warum muss man
> innerhalb einer Methode beim Zugriff auf Attribute und andere Methoden
> immer `self.attribut` bzw. `self.methode(...)` schreiben?”

Der Grund für das explizite `self` ist, dass Methoden auch als
Funktionen aufgerufen werden können! Und dann muss das Objekt als
Parameter der Funktion übergeben werden.

``` python
# 1. Möglichkeit: Klassischer Methodenaufruf: Das self-Argument steht "vor dem Punkt"
r2.stelle_dich_vor() # Das aufrufende Objekt wird automatisch als Argument übergeben und in self gespeichert

# 2. Möglichkeit: Methodenaufruf als Funktion
methode_als_funktion = Roboter.stelle_dich_vor  # Wir speichern die Methode in einer Variablen (noch kein Aufruf!)
methode_als_funktion(r2)  # Jetzt rufen wir die Methode auf, aber als Funktion mit einem Argument in Klammern
print(type(methode_als_funktion))  # <class 'function'>  d.h. Methoden sind auch nur Funktionen!
# Diesmal sieht man explizit, dass das Objekt als Argument übergeben und im self-Parameter gespeichert wird.

# 2b. Kurzfassung, in der die Methode direkt als Funktion aufgerufen wird
Roboter.stelle_dich_vor(r2)  # Hier wird der Methodenaufruf als Funktion aufgerufen

# Wir sehen: Methoden sind auch nur Funktionen und insb. auch Objekte! Damit wird vieles möglich, z.B.
# Methodenreferenzen (in Java wäre das Roboter::eineMethode (ab Java 8)).
# In Python brauchen wir diese Speziallösung nicht, weil Methoden sowieso Funktionen und damit auch Objekte sind,
# die wir in Variablen speichern, als Argumente übergeben und als Rückgabewerte verwenden können.

# Das ist aber in diesem Kurs noch nicht so wichtig, deshalb nur als Info am Rande!
```

    Ich bin der Roboter R2D2 und habe gerade 100/100 Energie.
    Ich bin der Roboter R2D2 und habe gerade 100/100 Energie.
    <class 'function'>
    Ich bin der Roboter R2D2 und habe gerade 100/100 Energie.

## Kapselung

Kapselung von Daten ist ein zentrales Element der objektorientierten
Programmierung. Python wird hier oft als weniger streng als andere
Sprachen wahrgenommen. Das ist durchaus richtig und hat mit der
Philosophie von Python zu tun, die oft durch den SattSatz “We are all
consenting adults here” beschrieben wird: Er drückt aus, dass Python
darauf vertraut, dass Programmierer verantwortungsbewusst handeln,
anstatt sie durch technische Einschränkungen oder strenge Regeln zu
zwingen.

Das steht tatsächlich in starkem Konstrast zu Sprachen wie Java, die
sehr “defensiv” sind, d.h. mit Mitteln der Syntax zu verhindern
versuchen, dass die Programmier bestimmte Dinge tun. Python stellt
ebenfalls diverse Möglichkeiten zur Kapselung von Daten bereit. *(Insb.
bieten Properties sowie Module (und andere *Namensräume*) hervorragende
Möglichkeiten, Daten nach außen unsichtbar zu machen. Auf diese
fortgeschrittenen Möglichkeiten gehen wir aber erst später ein.)* Vieles
Prinzipien sind aber eher Konventionen, d.h. sie können von
Programmierern in bestimmten Fällen auch bewusst durchbrochen werden.

Ein Beispiel für diese Philosophie sind die Zugriffsregeln für Attribut:
Im Gegensatz zu anderen Programmiersprachen kennt Python keine
Schlüsselwörter wie *private* und *public*.  
Ein Attribut wird in Python zu einem privaten Attribut, wenn der
Attributname mit \*\*zwei Unterstrichen \_\_\*\* beginnt und nicht mit
Unterstrichen endet.  
Alle Attribute und Methoden, die nicht mit einem doppelten Unterstrich
beginnen sind also öffentlich.

``` python
class Quadrat:
    def __init__(self, laenge: float) -> None:
        self.__laenge: float = laenge  # Das Attribut __laenge ist privat und kann nur innerhalb der Klasse verwendet werden

    def flaeche(self) -> float:
        return self.__laenge ** 2

    def umfang(self) -> float:
        return 4 * self.__laenge
    
    def get_laenge(self) -> float:  # Getter-Methode für das private Attribut __laenge
        return self.__laenge
    
    def set_laenge(self, laenge: float) -> None:  # Setter-Methode für das private Attribut __laenge
        if laenge > 0:
            self.__laenge = laenge
        else:
            print("Die Länge muss größer als 0 sein")
    
# Beispiel
q1 = Quadrat(5)
print(f"Fläche des Quadrats: {q1.flaeche()}")
print(f"Seitenlänge des Quadrats: {q1.get_laenge()}")

# Zugriff auf private Attribute führt zu einem Fehler
print("ACHTUNG: Zugriff auf private Attribute führt zu einem Fehler:")
print(q1.__laenge)  # AttributeError: 'Quadrat' object has no attribute '__laenge'
self.__laenge = 7  # AttributeError: 'Rechteck' object has no attribute '__laenge'
```

    Fläche des Quadrats: 25
    Seitenlänge des Quadrats: 5
    ACHTUNG: Zugriff auf private Attribute führt zu einem Fehler:

    AttributeError: 'Quadrat' object has no attribute '__laenge'

Als weiteres Beispiel modellieren wir eine Ampelschaltung. Der Zustand
der Ampel ist privat, denn der Wechsel zwischen den Zuständen soll nicht
beliebig geändert werden können, sondern nur durch die Methode
`schalten`, die die Reihenfolge *rot, gelb-grün, grün, gelb* durchläuft.

``` python
class Ampel:
    def __init__(self) -> None:
        self.__zustand: int = 0  # 0 = rot, 1 = gelb-rot, 2 = grün, 3 = gelb 
        # Dieses Attribut ist privat und kann nur innerhalb der Klasse verwendet werden. 
        # Wir stellen keinen setter und sogar nicht einmal einen getter zur Verfügung,
        # weil wir die Ampel nur schalten und die aktuelle Farbe anzeigen wollen.

    def schalten(self) -> None:
        # Die Ampel wird in den Folgezustand geschaltet.
        # Der Modulo-Operator % sorgt dafür, dass der Wertebereich von 0 bis 3 bleibt.
        self.__zustand = (self.__zustand + 1) % 4

    def aktuelle_farbe(self) -> str:
        farben = ["rot", "gelb-rot", "grün", "gelb"]
        return farben[self.__zustand]
    
# Beispiel
ampel = Ampel()
# Wir durchlaufen n Ampelphasen
n = 10
for i in range(n):
    print(f"Phase {i+1}: Die Ampel ist {ampel.aktuelle_farbe()}")
    ampel.schalten()
```

    Phase 1: Die Ampel ist rot
    Phase 2: Die Ampel ist gelb-rot
    Phase 3: Die Ampel ist grün
    Phase 4: Die Ampel ist gelb
    Phase 5: Die Ampel ist rot
    Phase 6: Die Ampel ist gelb-rot
    Phase 7: Die Ampel ist grün
    Phase 8: Die Ampel ist gelb
    Phase 9: Die Ampel ist rot
    Phase 10: Die Ampel ist gelb-rot

## <font color=red >Übung: Realisieren Sie eine Klasse nach Wahl</font>

-   Nutzen Sie in der `__init__()` Methode Parameter um die Attribute
    des neuen Objekts zu initialisieren
-   Verwenden Sie auch default-Parameter für Standardwerte
-   Kapseln Sie die Attribute und überlegen Sie, wo getter- und
    setter-Methoden sinnvoll sind
-   Schützen Sie die Attribute in den setter-Methoden vor unzulässigen
    Werten
-   Implementieren Sie die Methode `__str__(self)`
-   Testen Sie ihre Klasse

## Python-Besonderheiten

-   Bewusstes Durchbrechen der Kapselung ist möglich
-   Properties
-   Dunder-Methoden

### Durchbrechen der Kapselung

Wenn man unbedingt will, kann man die Kapselung durchbrechen. Das nutzen
z.B. Bibliotheken manchmal aus, um Klassen zu dokumentieren o.ä.

Wie das geht, sieht man im folgenden Beispiel:

``` python
ampel = Ampel()
ampel.schalten()
print(ampel.aktuelle_farbe())  

# Auf private Attribute kann nicht direkt zugegriffen werden:
# print(ampel.__zustand)  # AttributeError: 'Ampel' object has no attribute '__zustand'

# Allerdings...
dic = ampel.__dict__  # Gibt ein Dictionary mit den Attributen des Objekts zurück
print(dic)  # {'_Ampel__zustand': 0}, d.h. das private Attribut __zustand ist nicht wirklich verborgen, sondern nur umbenannt

# Das private Attribut kann trotzdem geändert werden
ampel._Ampel__zustand = 2  # Auf diese Weise kann man das private Attribut trotzdem ändern!
print(ampel.aktuelle_farbe())  # grün
```

    gelb-rot
    {'_Ampel__zustand': 1}
    grün

### Properties

Weil Python von “vernünftigen erwachsenen Programmierern” ausgeht, ist
die oben gezeigte Art des Umgangs mit privaten Attributen allgemein
akzeptiert. Mehr noch: In vielen unkritischen Fällen werden Attribute
einfach *öffentlich* gelassen. (Stattdessen wird häufig die ganze Klasse
hinter einem *Modul* oder einer *API* versteckt, so dass externe
“Benutzer” sie gar nicht kennen und erst recht nicht auf Attribute
zugreifen können.) Für die praktische Arbeit mit Klassen ist es oft viel
angenehmer, ihre Attribute direkt lesen und schreiben zu können. (Jeder
Java-Programmierer weiß, wie *nervig* die vielen Getter- und
Setter-Aufrufe sein können.) Außerdem bleiben die Klassen-Definition
deutlich übersichtlicher, wenn sie nicht durch viele (inhaltlich
triviale) get- und set-Methoden “zugemüllt” werden.

``` python
class RoboterÖffentlich:
    def __init__(self, pName: str) -> None:
        self.name: str = pName

# Beispiel
rob = RoboterÖffentlich("R2D2")
print(rob.name)  # R2D2
rob.name = "C3PO"  # Das Attribut name ist öffentlich und kann geändert werden
print(rob.name)  # C3PO

class RoboterPrivat:
    def __init__(self, pName: str) -> None:
        self.__name: str = pName  # Das Attribut __name ist privat und kann nur innerhalb der Klasse verwendet werden

    def get_name(self) -> str:
        return self.__name
    
    def set_name(self, name: str) -> None:
        if len(name) > 0:   # Beispiel für eine Validierung des setter-Arguments
            self.__name = name
        else:
            print("Der Name muss mindestens ein Zeichen lang sein")

# Beispiel
rob = RoboterPrivat("R2D2")
print(rob.get_name())  # R2D2
rob.set_name("C3PO")
```

    R2D2
    C3PO
    R2D2

Zusätzlich bietet Python aber auch eine elegante Methode, die einerseits
die sichere Kapselung von privaten Attributen gewährleistet,
andererseits aber einen syntaktisch einfacheren Zugriff ermöglicht: die
sogenannten **Properties**. Dabei verbindet man die Vorteile den beiden
vorigen Lösungen:

-   sichere Kapselung
-   aber einfacher Zugriff ohne Getter und Setter

``` python
# Roboter mit Property
class Roboter:
    def __init__(self, pName: str) -> None:
        self.__name: str = pName

    def get_name(self) -> str:
        return self.__name

    def set_name(self, name: str) -> None:
        if len(name) > 0:
            self.__name = name
        else:
            print("Der Name muss mindestens ein Zeichen lang sein")

    name = property(get_name, set_name)  # Property-Objekt wird erstellt und der Klasse als Attribut name hinzugefügt
    # Hinweis: Das geht auch einfacher mit dem Dekorator @property, siehe unten

# Beispiel
rob = Roboter("R2D2")
print(rob.name)  # Es sieht so aus, als ob wir auf ein Attribut zugreifen, aber in Wirklichkeit wird die Methode get_name() aufgerufen
rob.name = "C3PO"  # Auch hier wird in Wirklichkeit die Methode set_name() aufgerufen
print(rob.name)  # C3PO
rob.name = ""  # Weil hinter den Kulissen der Setter aufgerufen wird, wird die Validierung durchgeführt
print(rob.name)  # immer noch C3PO, weil der Setter die vorige Änderung verhindert hat
```

    R2D2
    C3PO
    Der Name muss mindestens ein Zeichen lang sein
    C3PO

``` python
# Roboter mit Property und Decorator
class Roboter:
    def __init__(self, pName: str) -> None:
        self.__name: str = pName

    @property   # Dekorator (nicht Thema dieses Kurses)
    def name(self) -> str:   # Das wird die Getter-Methode für das Property-Objekt name
        return self.__name

    @name.setter   # und das wird die Setter-Methode für das Property-Objekt name
    def name(self, name: str) -> None:
        if len(name) > 0:
            self.__name = name
        else:
            print("Der Name muss mindestens ein Zeichen lang sein")

# Beispiel
rob = Roboter("R2D2")
print(rob.name)  # R2D2
rob.name = "C3PO"
print(rob.name)  # C3PO
rob.name = ""  # Hier wird die Validierung des setters ausgeführt und die "Fehlermeldung" ausgegeben
print(rob.name)  # immer noch C3PO, weil der Setter die vorige Änderung verhindert hat
```

    R2D2
    C3PO
    Der Name muss mindestens ein Zeichen lang sein
    C3PO

**Vorteile von Properties**

1.  Kapselung: Direkter Zugriff auf private Attribute wird verhindert.
2.  Lesbarkeit: Properties erlauben es, Methoden wie Attribute aussehen
    zu lassen, was den Code klarer macht.
3.  Flexibilität: Sie ermöglichen es, die Implementierung zu ändern,
    ohne die öffentliche Schnittstelle der Klasse zu ändern.

Hier noch ein letztes Beispiel, das (hoffentlich) zeigt, wie Properties
den Übergang zwischen Attributen und Methoden bei Bedarf sehr fließend
gestalten können:

``` python
# Quadrat-Klasse, bei die Seitenlänge, aber auch Umfang und Fläche als Property definiert sind
# Der Clou: Alle drei Properties können nicht nur gelesen, sondern auch gesetzt werden - und
# verändern dann die anderen Properties entsprechend!
class Quadrat:
    def __init__(self, laenge: float) -> None:
        self.__laenge: float = laenge

    @property
    def laenge(self) -> float:
        return self.__laenge

    @laenge.setter
    def laenge(self, laenge: float) -> None:
        if laenge > 0:
            self.__laenge = laenge
        else:
            print("Die Länge muss größer als 0 sein")

    @property
    def umfang(self) -> float:
        return 4 * self.__laenge
    
    @umfang.setter
    def umfang(self, umfang: float) -> None:
        self.__laenge = umfang / 4

    @property
    def flaeche(self) -> float:
        return self.__laenge ** 2
    
    @flaeche.setter
    def flaeche(self, flaeche: float) -> None:
        self.__laenge = flaeche ** 0.5

# Beispiel
q = Quadrat(5)
print(f"Quadrat mit Seitenlänge {q.laenge}: Fläche = {q.flaeche}, Umfang = {q.umfang}")

q.laenge = 10
print(f"Wir setzen die Seitenlänge auf {q.laenge} => Fläche = {q.flaeche}, Umfang = {q.umfang}")

q.umfang = 16
print(f"Wir setzen den Umfang auf {q.umfang} => Seitenlänge = {q.laenge}, Fläche = {q.flaeche}")

q.flaeche = 25
print(f"Wir setzen die Fläche auf {q.flaeche} => Seitenlänge = {q.laenge}, Umfang = {q.umfang}")
```

    Quadrat mit Seitenlänge 5: Fläche = 25, Umfang = 20
    Wir setzen die Seitenlänge auf 10 => Fläche = 100, Umfang = 40
    Wir setzen den Umfang auf 16.0 => Seitenlänge = 4.0, Fläche = 16.0
    Wir setzen die Fläche auf 25.0 => Seitenlänge = 5.0, Umfang = 20.0

### Dunder-Methoden

In Python gibt es zahlreiche Spezialmethoden (oft auch als
“Dunder-Methoden” bezeichnet, da sie mit doppelten Unterstrichen
beginnen und enden), die Klassen bestimmte Verhaltensweisen verleihen
oder anpassen.

-   Initialisierung und Darstellung von Objekten: `__init__`,
    `__repr__`, `__str__`
-   Vergleichsmethoden: `__eq__`, `__lt__`, …
-   Iteration: `__iter__`, `__next__`
-   “Länge” eines Objekts definieren: , `__len__`, …
-   Operatoren überladen: `__add__`, `__mul__`, `__getitem__`, …
    -   insb. `__call__` um Objekte “aufrufbar” zu machen:
        `ein_objekt()`
-   …

Im Rahmen dieses Kurses können wir nicht alle diese Methoden vorstellen.
Hier aber zumindest eine Klasse, die einige dieser Möglichkeiten
demonstriert:

``` python
from __future__ import annotations  # nötig, damit wir innerhalb der Klasse Bruch schon den Typ Bruch verwenden können

# Beispielklasse mit einigen typischen Dunder-Methoden
class Bruch:
    def __init__(self, zaehler: int, nenner: int) -> None:
        self.zaehler: int = zaehler
        self.nenner: int = nenner

    def __str__(self) -> str:  # Wird aufgerufen, wenn das Objekt als String dargestellt werden soll
        return f"{self.zaehler}/{self.nenner}"

    def __repr__(self) -> str:  # Wird aufgerufen, wenn das Objekt als Repräsentation dargestellt werden soll
        # Der erzeugte String sollte Python-Code sein, der das Objekt erzeugen würde
        return f"Bruch({self.zaehler}, {self.nenner})"  
    
    def gekürzt(self) -> Bruch:
        from math import gcd   # größter gemeinsamer Teiler
        teiler = gcd(self.zaehler, self.nenner)
        return Bruch(self.zaehler // teiler, self.nenner // teiler)

    def __add__(self, other: Bruch) -> Bruch:  # Wird aufgerufen, wenn zwei Bruch-Objekte addiert werden
        neuer_zaehler = self.zaehler * other.nenner + other.zaehler * self.nenner
        neuer_nenner = self.nenner * other.nenner
        return Bruch(neuer_zaehler, neuer_nenner).gekürzt()
    
    def __sub__(self, other: Bruch) -> Bruch:  # Wird aufgerufen, wenn zwei Bruch-Objekte subtrahiert werden
        # other negieren und dann addieren
        return self + Bruch(-other.zaehler, other.nenner)
    
    def __mul__(self, other: Bruch) -> Bruch:  # Wird aufgerufen, wenn zwei Bruch-Objekte multipliziert werden
        return Bruch(self.zaehler * other.zaehler, self.nenner * other.nenner).gekürzt()
    
    def __eq__(self, other: object) -> bool:  # Wird aufgerufen, wenn zwei Bruch-Objekte auf Gleichheit geprüft werden
        if not isinstance(other, Bruch):
            return False
        return self.zaehler * other.nenner == other.zaehler * self.nenner
    
    def __lt__(self, other: object) -> bool:  # Wird aufgerufen, wenn ein Bruch-Objekt kleiner als ein anderes geprüft wird
        if not isinstance(other, Bruch):
            return False
        return self.zaehler * other.nenner < other.zaehler * self.nenner
    
    
# Beispiele
b1 = Bruch(1, 2)
b2 = Bruch(1, 3)

print(f"b1: {b1}")  # 1/2
print(f"b1 repr: {repr(b1)}")  # Bruch(1, 2)
print(f"b2: {b2}")  # 1/3
print(f"b2 repr: {repr(b2)}")  # Bruch(1, 3)

print(f"b1 + b2: {b1 + b2}")  # 5/6
print(f"b1 == b2: {b1 == b2}")  # False
print(f"b1 < b2: {b1 < b2}")  # False

brueche_unsortiert = [Bruch(1, 2), Bruch(3, 4), Bruch(1, 3), Bruch(2, 3), Bruch(1, 4)]
brueche_sortiert = sorted(brueche_unsortiert)  # funktioniert, weil die Klasse die Dunder-Methode __lt__ implementiert
print(f"Unsortiert: {brueche_unsortiert}")
print(f"Sortiert: {brueche_sortiert}")

# Noch ein Test mit anderen Brüchen
b3 = Bruch(1, 4)
b4 = Bruch(2, 4)
print(f"{b4} gekürzt: {b4.gekürzt()}")  # 1/2
print(f"{b3} + {b4} = {b3 + b4}")  # 3/4
print(f"{b3} - {b4} = {b3 - b4}")  # -1/4
print(f"{b3} * {b4} = {b3 * b4}")  # 1/8
```

    b1: 1/2
    b1 repr: Bruch(1, 2)
    b2: 1/3
    b2 repr: Bruch(1, 3)
    b1 + b2: 5/6
    b1 == b2: False
    b1 < b2: False
    Unsortiert: [Bruch(1, 2), Bruch(3, 4), Bruch(1, 3), Bruch(2, 3), Bruch(1, 4)]
    Sortiert: [Bruch(1, 4), Bruch(1, 3), Bruch(1, 2), Bruch(2, 3), Bruch(3, 4)]
    2/4 gekürzt: 1/2
    1/4 + 2/4 = 3/4
    1/4 - 2/4 = -1/4
    1/4 * 2/4 = 1/8

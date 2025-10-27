# Module und Pakete

Bei diesem Thema geht es um die Strukturierung größerer Python-Projekte
in Modulen (= Dateien) und Paketen (= Ordern). Dies lässt sich schlecht
in einem Jupyter-Notebook veranschaulichen. Wir verweisen daher auf die
Beispielprojekte und die Erklärungen im Online-Kurs:

-   Bitte melden Sie sich zuerst auf www.edube.org an.
-   [Einheit 1.1 (Module)](https://edube.org/learn/pe-2/modules-3)
    erklärt, wie man mit Modulen arbeitet, wie man zwischen der Nutzung
    eines Moduls als Hauptprogramm und als Bibliothek unterscheidet,
    usw.
-   [Einheit 1.2 (Ausgewählte
    Module)](https://edube.org/learn/pe-2/useful-modules-6) stellt
    beispielhaft die Module *math, random* und *platform* genauer vor.
-   [Einheit 1.3 (Module und
    Pakete)](https://edube.org/learn/pe-2/modules-and-packages-30)
    beschreibt Pythons Paketkonzept.
-   [Einheit 1.4
    (Paketmanagement)](https://edube.org/learn/pe-2/python-package-installer-pip-6)
    zeigt, wie man mit dem Paketmanager *pip* schnell auf Tausende von
    Python-Bibliotheken zugreifen kann.

Eine gute Zusammenfassung des Modul- und Paketkonzepts von Python finden
sie auch auf
[python-kurs.eu](https://www.python-kurs.eu/python3_modularisierung.php).

**Achtung:** Das Import-System von Python ist, sobald man sich im Detail
damit beschäftigt, leider ziemlich kompliziert. Im schulischen Kontext
wird man normalerweise auf diese Schwierigkeiten nicht stoßen. Insb.
kann man seit Python 3.3 beim Anlegen von Paketen die Datei
`__init__.py` im Normalfall sogar ganz *weglassen* - damit entfällt ein
großer Stolperstein.

Falls es aber doch Probleme gibt, kann es hilfreich sein, den Artikel
[“Traps for the Unwary in Python’s Import
System”](http://python-notes.curiousefficiency.org/en/latest/python_concepts/import_traps.html)
oder z.B. [diesen Eintrag auf
StackOverflow](https://stackoverflow.com/a/48804718) genau zu lesen.

### Aufgaben

#### Aufgabe 1

Die Python-Module *math* und *random* werden Sie im Unterricht
höchstwahrscheinlich immer wieder nutzen (*platform* wohl weniger).

Recherchieren Sie unter den folgenden Internetquellen, welche
interessanten Funktionen diese Module bieten:

math: - https://docs.python.org/3.9/library/math.html -
https://realpython.com/python-math-module/ -
https://www.programiz.com/python-programming/modules/math

random: - https://docs.python.org/3.9/library/random.html -
https://www.python-lernen.de/zufallszahlen-random.htm -
https://www.w3schools.com/python/module_random.asp

platform: - https://docs.python.org/3.9/library/platform.html

#### Aufgabe 2

Entwickeln Sie - eine Aufgabe, zu deren Lösung man das Modul *math*
benutzen könnte (sollte!), sowie - eine Aufgabe, zu deren Lösung man das
Modul *random* benutzen muss

Senden Sie die Aufgaben an die Kursleitung - wir erstellen daraus eine
Sammlung für den Unterricht.

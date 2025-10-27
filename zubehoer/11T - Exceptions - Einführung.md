# Errors, failures, and other plagues


Egal wie gut der Code ist, irgendwas geht immer schief. Schauen wir uns
ein erstes Programm an, bei in bestimmten Fällen Fehler auftreten
können.

``` python
import math
x = float(input('Gib eine Zahl ein:'))
y = math.sqrt(x)
print('Wurzel von', x, 'ist', y)
```

### Was kann hier schief laufen?

1.  Der Benutzer gibt eine Zeichenkette ein, die nicht in eine Zahl
    gewandelt werden kann.  
    ➽ **<font color=red>ValueError </font>**: could not convert string
    to float: ‘abc’
2.  Der Benutzer gibt eine negative Zahl ein. Davon lässt sich keine
    Wurzel berechnen.  
    ➽ **<font color=red>ValueError </font>**: math domain error

Jedes Mal, wenn Ihr Code versucht, etwas
Falsches/Dummes/Verantwortungsloses/Verrücktes/Unerzwingbares zu tun,
macht Python zwei Dinge: - das Programm wird zwangsweise beendet, - es
erzeugt eine spezielle Art von Daten, die Exception genannt wird.

Beide Aktivitäten werden als Auslösen einer Ausnahme (raising an
exception) bezeichnet. Wir können sagen, dass Python immer dann eine
Exception auslöst (oder dass eine Exception ausgelöst wurde), wenn es
keine Ahnung hat, was es mit Ihrem Code machen soll.

Python bietet effektive Werkzeuge, mit denen Sie Ausnahmen beobachten,
identifizieren und effizient behandeln können. Dies ist dadurch möglich,
dass alle potenziellen Ausnahmen ihre eindeutigen Namen haben, so dass
Sie sie kategorisieren und entsprechend reagieren können.

### weitere Exceptions

``` python
value = 1
value /= 0
```

➽ **<font color=red>ZeroDivisionError </font>**: division by zero

``` python
my_list = []
x = my_list[0]
```

➽ **<font color=red>IndexError </font>**: list index out of range

➽ **<font color=red>KeyboardInterrupt</font>**  
**Description**: a concrete exception raised when the user uses a
keyboard shortcut designed to terminate a program’s execution (Ctrl-C in
most OSs); if handling this exception doesn’t lead to program
termination, the program continues its execution.

➽ **<font color=red>LookupError</font>**  
**Description**: an abstract exception including all exceptions caused
by errors resulting from invalid references to different collections
(lists, dictionaries, tuples, etc.)

➽ **<font color=red>MemoryError </font>**  
**Description**: a concrete exception raised when an operation cannot be
completed due to a lack of free memory.

➽ **<font color=red>OverflowError </font>**  
**Description**: a concrete exception raised when an operation produces
a number too big to be successfully stored

➽ **<font color=red>ImportError </font>**  
**Description**: a concrete exception raised when an import operation
fails

➽ **<font color=red>KeyError </font>**  
**Description**: a concrete exception raised when you try to access a
collection’s non-existent element (e.g., a dictionary’s element)

#### siehe

-   https://edube.org/learn/pe-2/useful-exceptions-10

-   https://edube.org/learn/pe-2/useful-exceptions-11

-   https://docs.python.org/3.9/library/exceptions.html

### Aber wäre es nicht besser, erst alle Umstände zu prüfen und dann erst etwas zu tun, wenn es sicher ist?

Zugegeben, dieser Weg mag am natürlichsten und verständlichsten
erscheinen, aber in Wirklichkeit macht diese Methode das Programmieren
nicht einfacher. All diese Prüfungen können Ihren Code aufblähen und
unlesbar machen (**your code bloated and illegible**).

``` python
first_number = int(input("Enter the first number: "))
second_number = int(input("Enter the second number: "))

if second_number != 0:
    print(first_number / second_number)
else:
    print("This operation cannot be done.")
print("THE END.")
```

### Bessere Lösung mit try: except:

-   Das Schlüsselwort `try` beginnt einen Block des Codes, der korrekt
    ausgeführt werden kann oder auch nicht.
-   Als Nächstes versucht Python, die riskante Aktion auszuführen. Wenn
    sie fehlschlägt, wird eine Exception ausgelöst und Python beginnt,
    nach einer Lösung zu suchen.
-   Das `except`-Schlüsselwort startet ein Stück Code, das ausgeführt
    wird, wenn irgendetwas innerhalb des `try`-Blocks schief geht. Wenn
    eine Exception in einem vorherigen `try`-Block ausgelöst wurde, wird
    sie hier fehlschlagen. Also sollte der Code nach dem
    `except`-Schlüsselwort eine angemessene Reaktion auf die ausgelöste
    Exception bieten;
-   Die Rückkehr zur vorherigen Verschachtelungsebene beendet den
    `try`-`except`-Abschnitt.

``` python
try:
    first_number = int(input("Enter the first number: "))
    second_number = int(input("Enter the second number: "))
    print(first_number / second_number)
except:
    print("This operation cannot be done.")

print("THE END.")
```

### Nachfolgende Code-Sequenz verdeutlicht auch die Arbeitsweise von try-except.

Die Anweisungen innerhalb des try-Blockes werden ausgeführt bis ein
Fehler auftritt. Hier ist dies ein ZeroDivivionError. Die Bearbeitung
des try-Blockes wird abgebrochen und das Programm setzt seine
Bearbeitung im except-Block fort.

``` python
try:
    print("1")
    x = 1 / 0
    print("2")
except:
    print("Oh dear, something went wrong...")

print("3")
```

## Mehrere unterschiedliche Fehlermöglicheiten abfangen

``` python
try:
    x = int(input("Enter a number: "))
    y = 1 / x
    print(y)
except ZeroDivisionError:
    print("You cannot divide by zero, sorry.")
except ValueError:
    print("You must enter an integer value.")
except:
    print("Oh dear, something went wrong...")

print("THE END.")
```

Der Code erzeugt, wenn er ausgeführt wird, eine der folgenden vier
Varianten der Ausgabe: - Gibt der Benutzer einen gültigen ganzzahligen
Wert ein, der nicht Null ist (z. B. 5)  
`0.2`  
`THE END.` - Gibt der Benutzer die Zahl 0 ein.  
`You cannot divide by zero, sorry.`  
`THE END.` - Gibt der Benutzer eine beliebige nicht-ganzzahlige
Zeichenfolge ein `You must enter an integer value.`  
`THE END.` - Drückt der Benutzer (lokal auf seinem Rechner), die
Tastenkombination Strg-C, während das Programm auf die Eingabe wartet
wird ein KeyboardInterrupt auslöst.  
Im Jupyter Notebook, wird dieser Fehler durch ‘Interrupt Kernel’
ausgelöst.  
`Oh dear, something went wrong...`  
`THE END.`

## Wichtiges Merkmale zu Exceptions

-   Except-Zweige werden in der gleichen Reihenfolge gesucht, wie sie im
    Code erscheinen;
-   Sie dürfen nicht mehr als einen except-Zweig mit einem bestimmten
    Ausnahmenamen verwenden;
-   Die Anzahl der verschiedenen except-Zweige ist beliebig - die
    einzige Bedingung ist, dass Sie, wenn Sie try verwenden, mindestens
    ein except (mit oder ohne Namen) dahinter setzen müssen.
-   Das except-Schlüsselwort darf nicht ohne ein vorangehendes try
    verwendet werden;
-   Wenn einer der except-Zweige ausgeführt wird, werden keine anderen
    Zweige besucht;
-   Wenn keiner der angegebenen except-Zweige auf die ausgelöste
    Exception passt, bleibt die Exception unbehandelt.
-   Wenn ein unbenannter except-Zweig existiert (einer ohne
    Exception-Namen), muss er als letzter angegeben werden.  
    Sie können auch nicht mehr als einen anonymen (unbenannten)
    Ausnahmezweig nach den benannten Zweigen hinzufügen.
-   Ein unbenannter except-Zweig ist gleichwertig zu
    `except BaseException`.

``` python
try:
    x = int(input("Enter a number: "))
    y = 1 / x
    print(y)
except ZeroDivisionError:
    print("You cannot divide by zero, sorry.")
except ValueError:
    print("You must enter an integer value.")
except:
    print("Oh dear, something went wrong...")

print("THE END.")
```

## Eine Übersicht von Exceptions

<img src="images/except1.png">

-   ZeroDivisionError erbt von der Klasse ArithmeticError
-   ArithmeticError erbt wiederum von der Klasse Exception
-   Exception ist von BaseException abgeleitet

Wir können sagen, dass eine Ausnahme umso allgemeiner ist, je näher sie
sich an der Wurzel befindet. Im Gegenzug sind die Ausnahmen, die sich an
den Enden der Zweige (wir können sie Blätter nennen) befinden
spezieller.

## Exceptions mit `raise` selbst erzeugen

``` python
def bad_fun(n):
    raise ZeroDivisionError

try:
    bad_fun(0)
except ArithmeticError:    # ZeroDivisionError ist eine Subklasse von ArithmeticError
    print("What happened? An error?")

print("THE END.")
```

#### Die Anweisung raise kann auch auf eine weitere Weise verwendet werden.

-   Beachten Sie hier das Fehlen des Namens der Ausnahme.
-   Diese Art von raise-Anweisung darf nur innerhalb der
    except-Verzweigung verwendet werden. Die Verwendung in jedem anderen
    Kontext führt zu einem Fehler.
-   Die Anweisung löst die gleiche Ausnahme, die gerade behandelt wird,
    sofort wieder aus.
-   Dank dieser Anweisung können Sie die Behandlung von Ausnahmen auf
    verschiedene Teile des Codes verteilen.

Der ZeroDivisionError wird zweimal ausgelöst: - Zuerst innerhalb des
try-Teils des Codes (dies wird durch die tatsächliche Null-Division
verursacht) - und dann noch innerhalb des except-Teils durch die
raise-Anweisung.

``` python
def bad_fun(n):
    try:
        return n / 0
    except:
        print("I did it again!")
        raise

try:
    bad_fun(0)
except ArithmeticError:
    print("I see!")

print("THE END.")
```

## Die optionale else-Klausel

Das `try... except` Sprachkonstrukt hat eine optionale `else`-Klausel.
Diese steht - falls vorhanden nach allen `except`-Klauseln. Dort
befindet sich Code, der ausgeführt wird, wenn die `try`-Klausel keine
Ausnahme auslöst.

``` python
while True:
    filename = input("Dateiname")
    try:
        f = open(filename,"r")
    except IOError as ioe:
        print(ioe.args)
        print(filename,"lässt sich nicht öffnen")
    else:
        print(filename,'hat',len(f.readlines()),'Zeilen')
        f.close()
        break
```

    Dateiname Jekyll.txt
    Dateiname Jekyll.txt

    (2, 'No such file or directory')
    Jekyll.txt lässt sich nicht öffnen
    Jekyll.txt hat 5 Zeilen

## Die optionale finally-Klausel

Anweisungen die im finaly-Block aufgeführt sind, werden unter allen
Umständen ausgeführt (unabhängig davon ob im try-Block eine Ausnahme
aufgetreten ist). Wird finaly verwendet kann auf die Ausnahmebehandlung
(except-Zweige) verzichtet werden .

``` python
try:
    x = float(input("Deine Zahl:"))
    y = 1/x
    print("Kehrwert:",y)
except:
    print("Es ist ein Fehler aufgetreten")
finally:
    print("ich werde immer ausgegeben, ob Fehler oder nicht!")
```

## Annahmen treffen mit `assert`

Wenn der assert Ausdruck True, einen numerischen Wert ungleich Null,
eine nicht leere Zeichenkette oder einen anderen Wert als None ergibt,
wird nichts weiter getan. Andernfalls wird automatisch und sofort ein
`AssertionError` ausgelöst (in diesem Fall sagen wir, dass die Assertion
fehlgeschlagen ist)

``` python
import math

x = float(input("Enter a number: "))
assert x >= 0.0

x = math.sqrt(x)

print(x)
```

    Enter a number:  -10

    AssertionError: 

## Detailiertere Informationen zu aufgetretenen Exceptions können mit der Methode exc_info() aus dem Modul sys auslesen werden

-   https://docs.python.org/3/library/sys.html

``` python
import sys
sys.exc_info?
```

    Signature: sys.exc_info()
    Docstring:
    Return current exception information: (type, value, traceback).

    Return information about the most recent exception caught by an except
    clause in the current stack frame or in an older stack frame.
    Type:      builtin_function_or_method

``` python
import sys

def strToInt(var):
    try:
        x = int(var)
        return x
    except: 
        print('Error in function strToInt')
        raise 
    
try:
    i = strToInt("Hallo")
except:
    (type,value,traceback) = sys.exc_info()
    print("Unexpected Error out off function")
    print("Type: ", type)
    print("Value: ", value)
#    print("Value: ", sys.exc_info()[1])    
    print("Traceback: ", traceback)   
```

    Error in function strToInt
    Unexcpected Error out off function
    Type:  <class 'ValueError'>
    Value:  invalid literal for int() with base 10: 'Hallo'
    Traceback:  <traceback object at 0x000002688B751340>

# Motivation


Wie kann ein Reporter bei der anstehenden Fußballeuropameisterschaft
sehr *schnell* den Spielernamen ermitteln, wenn er die Rückennummer
sieht.

``` python
# Erster Versuch: Zwei "parallele" Listen
mannschaft = ["Neuer", "Hummels", "Süle", "Tah", "Brandt", "Müller", "Gosens", "Havertz", "Musiala", "Kimmig"]
nummern = [1, 5, 15, 4, 11, 13, 20,  7, 14, 6]

print(mannschaft[nummern.index(13)])   # unschön und ineffizient: die ganze Liste muss durchsucht werden

# Zweiter Versuch: Elegant und blitzschnell mit einem Dictionary:
mannschaft = {1:"Neuer", 5:"Hummels", 15:"Süle", 4:"Tah", 11:"Brandt", 13:"Müller", 20:"Gosens", 7:"Havertz", 14:"Musiala", 6:"Kimmig"}
print(mannschaft[13])
```

# Dictionaries

#### Anlegen eines Dictionaries und Zugriff auf die Elemente

``` python
namen = {}    # erzeugt ein leeres dictionary. Alternativ: dict()

# Werte in das dict eintragen: ähnlich wie bei Listen mit eckigen Klammern
namen["Potter"] = "Harry"   # Schlüssel: Nachname, Wert: Vorname
namen["Granger"] = "Hermine"
namen["Weasley"] = "Ron"
namen["Dumbledore"] = "Albus"
```

#### Den Value passend zu einem bekannten Key auslesen

Dies kann auf zwei unterschiedliche Arten erfolgen.

``` python
# Auf Werte zugreifen: ebenfalls wie bei Listen
vorname = namen["Potter"]
print(vorname)

vorname = namen.get("Potter")
print(vorname)
```

#### Natürlich kann man Einträge auch überschreiben und löschen:

``` python
nn = "Weasley"
namen[nn] = "Percy"
print(namen[nn], nn)
del namen[nn]  # hier wird Weasley aus dem Dictionary entfernt
print(namen.get(nn, f"Ich kenne niemanden mehr mit Namen {nn}"))
```

#### Wie kann festgestellt werden, ob es einen Eintrag zu einem Key gibt?

``` python
name = "Meier"
if name in namen:
    print(namen[name], name)
else:
    print("NN", name)
```

Es lassen sich auch gleich eine Menge von Namen aus einer Liste
überprüfen ob diese im Dictionary vorhanden sind

``` python
for name in ["Weasley", "Potter", "Longbottom", "Voldemort"]:
    if name in namen:
        print(namen[name], name)
    else:
        print("NN", name)
```

#### Was passiert, wenn kein Eintrag zum Key (Schlüssel) gefunden wird?

Es wird eine sogenannte KeyError-Exception geworfen, da zu dem Key kein
passender Value gefunden wird.  
(Der Schlüssel passt in kein kein Schloss)

``` python
key = "Meier"
print(namen[key])
# print(key, namen.get(key)) # gleiches Problem
```

Diese Exception kann umgangen werden, in dem der Abfrage ein
Default-Value mitgegeben wird.

``` python
key = "Meier"
print(key, namen.get(key,"gibt es nicht bei Harry Potter."))
```

#### Einige weitere nützliche Funktionen, welche das Arbeiten mit einem Dictionary erleichtern (Scan aus Westermann Buch):

<img src="images/DictMethoden.png" width="60%">

### Iteration über Dicts: Verschiedene Varianten

Ein Dictionary speichert sowohl *Schlüssel* als auch *Werte*. Was meinen
wir also damit, wenn wir über ein dict zu iterieren bzw. es mit einer
Schleife zu durchlaufen?

Tatsächlich gibt es, je nach Anwendungsfalls, verschiedene Varianten für
Schleifen über dicts:

#### Iteration über alle *Schlüssel*

Die Methode keys() liefert alle im Dictionary enthaltenen Keys als Liste
zurück. Diese können in einer Schleife durchlaufen werden.

``` python
for key in namen.keys():
    print(key,"heißt mit Vornamen",namen[key])
```

#### Schleife nur mit den gespeicherten *Werten* (ohne die Schlüssel)

``` python
for vn in namen.values():
    print(f"Jemand heißt mit Vornamen {vn}.")
```

#### Iteration über Schlüssel und Werte *gleichzeitig*

Wenn man alle key-value-Paare durchlaufen will, dann nutzt man
`items()`:

``` python
for nachname, vorname in namen.items():
    print(f"{vorname} {nachname}")
```

#### Wieviel Einträge gibt es im Dictionary?

Hierzu kann wie bei anderen Datenstrukturen die Buildin Funktion `len()`
verwendet werden.

``` python
print("Es wurden",len(namen), "Harry Potter Figuren mit Name und Vorname erfasst")
```

#### Wenn die Keys Strings sind, kann man zur Vereinfachung den praktischen Konstruktor `dict()` verwenden

``` python
preise = {"Eis": 2, "Kuchen": 1.5}
preise = dict(Eis=2, Kuchen=1.5, Kaffee=1, Tee=1)

bestellung = "Kuchen"
preis = preise[bestellung]
print(bestellung, "kostet", preis, "EUR.")
```

## Verschachtelte Dictionaries

Dictionaries können ohne Probleme als Daten wiederum weitere koplexe
Datentypen wie Dictionaries, Listen, Objekte, Tupels… enthalten.  
Der Zugriff erfolgt wie gewohnt über die eckigen Klammern.

**a) Beispiel mit Dict**

<img src="images/Dict1.png" width="60%"></br>

**b) Beispiel mit Liste**

<img src="images/Dict2.png" width="60%"></br>

**c) Beispiel mit mehreren Dicts**

<img src="images/Dict3.png" width="60%"></br>

**d) Noch ein Beispiel mit geschachtelten Dictionaries**  
So ist z.B. Beim Key “Milch” ein Dictionary als Value hinterlegt, indem
der Lagerbestand und der aktuelle Preis eingetragen sind.

``` python
supermarket = { "milk": {"quantity": 20, "price": 1.19},
               "biscuits":  {"quantity": 32, "price": 1.45},
               "butter":  {"quantity": 20, "price": 2.29},
               "cheese":  {"quantity": 15, "price": 1.90},
               "bread":  {"quantity": 15, "price": 2.59},
               "cookies":  {"quantity": 20, "price": 4.99},
               "yogurt": {"quantity": 18, "price": 3.65},
               "apples":  {"quantity": 35, "price": 3.15},
               "oranges":  {"quantity": 40, "price": 0.99},
               "bananas": {"quantity": 23, "price": 1.29}}
```

##### Kassenzettel mit `items()` und f-Strings

``` python
total_value = 0
for article, numbers in supermarket.items():
    quantity = numbers["quantity"]
    price = numbers["price"]
    product_price = quantity * price
    print(f"{article:15s} {product_price:8.2f}")
    total_value += product_price
print("="*24)   
print(f"Total sum:      {total_value:8.2f}")
```

### Dictionaries schön darstellen

``` python
print("Ziemlich unübersichtlich:")
print(supermarket)


print("\nBesser:")
from pprint import pprint
pprint(supermarket)

print("\nNoch besser mit Hilfe der json-Bibliothek:")
import json
print(json.dumps(supermarket, indent=4))
```

# JSON encoder and decoder


Nähere Informationen zu JSON
https://de.wikipedia.org/wiki/JavaScript_Object_Notation  
Zugriff mittels Python siehe https://docs.python.org/3/library/json.html

``` python
bundesligaVereine = {"FC Bayern München":{"Trainer":"Julian Nagelsmann",
                                          "Tormann":["Manuel Neuer","Sven Ulreich","Christian Früchtel"],
                                          "Abwehr":["Dayot Upamecano","Niklas Süle","Benjamin Pavard","Alphonso Davies","Chris Richards"],
                                          "Mittelfeld":["Joshua Kimmich","Leon Goretzka","Corentin Tolisso","Marc Roca"],
                                          "Sturm":["Serge Gnabry","Robert Lewandowski","Leroy Sané","Kingsley Coman","Jamal Musiala"]}
                    }
```

## Umwandlung von Dictionaries in JSON

Dictionaries lassen sich sehr leicht in JSON Strings umwandeln. Hierzu
muss allerdings die Library `json` eingebunden werden. Die darin
hinterlegte Funktion `dumps()` wird im einfachsten Fall mit einem
Dictionary als Parameter aufgerufen und liefert als Ergebnis einen
JSON-String zurück.  
Dieser wird in unserem Beispiel zur Kontrolle auf der Konsole
ausgegeben.

``` python
import json  
# Serializing json   
json_object = json.dumps(bundesligaVereine)  
print(type(json_object))
print(json_object) 
```

    <class 'str'>
    {"FC Bayern M\u00fcnchen": {"Trainer": "Julian Nagelsmann", "Tormann": ["Manuel Neuer", "Sven Ulreich", "Christian Fr\u00fcchtel"], "Abwehr": ["Dayot Upamecano", "Niklas S\u00fcle", "Benjamin Pavard", "Alphonso Davies", "Chris Richards"], "Mittelfeld": ["Joshua Kimmich", "Leon Goretzka", "Corentin Tolisso", "Marc Roca"], "Sturm": ["Serge Gnabry", "Robert Lewandowski", "Leroy San\u00e9", "Kingsley Coman", "Jamal Musiala"]}}

### Schreiben von JSON-Daten in eine Datei.

Im folgenden Beispiel wird eine neue Datei mit dem Namen
“bundesliga.json” erzeugt. Das Programm erhält hierauf
Schreibberechtigung (Parameter “w” von write). Durch das Öffnen der
Datei mit `with` wird diese Datei am Ende des Dateizugriffs auch wieder
ordenlich geschlossen.  
Wird die Funktion `dump()` aus der Library `json` mit zwei Parameter
aufgerufen, muss es sich bei dem zweiten Parameter um eine Datei mit
Schreibberechtigung handeln.

``` python
with open("data/bundesliga.json", "w") as outfile: 
    json.dump(bundesligaVereine, outfile)
```

### Lesen von JSON-Daten aus einer Datei

Die Funktion `open()` öffnet eine Datei. In unserer Anwendung Lesend,
gekennzeichnet durch den Parameter “r”. In der Library `json` gibt es
eine Funktion `load()` mit der eine JSON-Datei gelesen werden kann.
Diese liefert als Ergebnis ein Dictionary. Darauf können alle bereits
erlernden Operationen ausgeführt werden.

``` python
with open("data/bundesliga.json", "r") as json_file: 
    bundesligaVereine = json.load(json_file)

print(type(bundesligaVereine))
print(bundesligaVereine)
```

    <class 'dict'>
    {'FC Bayern München': {'Trainer': 'Julian Nagelsmann', 'Tormann': ['Manuel Neuer', 'Sven Ulreich', 'Christian Früchtel'], 'Abwehr': ['Dayot Upamecano', 'Niklas Süle', 'Benjamin Pavard', 'Alphonso Davies', 'Chris Richards'], 'Mittelfeld': ['Joshua Kimmich', 'Leon Goretzka', 'Corentin Tolisso', 'Marc Roca'], 'Sturm': ['Serge Gnabry', 'Robert Lewandowski', 'Leroy Sané', 'Kingsley Coman', 'Jamal Musiala']}}

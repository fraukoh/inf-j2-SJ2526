# Lösungen: Dictionaries


#### Aufgabe 1 - Telefonbuch

1.  Erweitere das Telefonbuch um weitere Personen/Nummern.
2.  Finde die Telefonnummer einer Person im Telefonbuch heraus.
3.  Gib eine sinnvolle Meldung aus, wenn nach einer unbekannten Person
    gesucht wird.

``` python
telefonbuch = {}
telefonbuch["Tick"] = "12345"
telefonbuch["Trick"] = "23456"

# Lösung:
telefonbuch["Track"] = "34567"
print("Trick: ", telefonbuch.get("Trick", "kenn ich nicht"))
print("Truck: ", telefonbuch.get("Truck","kenn ich nicht"))
```

    Trick:  23456
    Truck:  kenn ich nicht

#### Aufgabe 2 - Vereinsverwaltung

Gegeben ist eine Zusammenstellung von Bundesligavereinen mit den
dazugehörenden Trainer.

``` python
bundesligaVereine= {"FC Bayern München":"Thomas Tuchel",
                    "VFL Wolfsburg":"Ralph Hasenhüttl",
                    "RB Leipzig":"Marco Rose",
                    "Borussia Dortmund":"Edin Terzic",
                    "Eintracht Frankfurt":"Dino Topmöller",
                    "Bayer Leverkusen":"Xabi Alonso",
                    "Borussia Mönchengladbach":"Gerardo Seoane",
                    "VFB Stuttgart":"Sebastian Hoeneß",
                    "FC Köln":"Timo Schultz"
                   }
```

1.  Der SC Freiburg wird von Christian Streich trainiert.

``` python
# insert code here
bundesligaVereine["SC Freiburg"] = "Christian Streich"
```

1.  Geben Sie den Trainer des FC Bayern auf zwei unterschiedliche Arten
    aus.

``` python
# insert code here
print(bundesligaVereine["FC Bayern München"]["Trainer"])
print(bundesligaVereine.get("FC Bayern München").get("Trainer"))
```

    Thomas Tuchel
    Thomas Tuchel

1.  Erstellen Sie eine Übersicht, welche Vereine von welchen Trainern
    trainiert werden.

``` python
# insert code here
for verein, trainer in bundesligaVereine.items():
    print(verein, "wird trainiert von", trainer)
```

    FC Bayern München wird trainiert von Thomas Tuchel
    VFL Wolfsburg wird trainiert von Ralph Hasenhüttl
    RB Leipzig wird trainiert von Marco Rose
    Borussia Dortmund wird trainiert von Edin Terzic
    Eintracht Frankfurt wird trainiert von Dino Topmöller
    Bayer Leverkusen wird trainiert von Xabi Alonso
    Borussia Mönchengladbach wird trainiert von Gerardo Seoane
    VFB Stuttgart wird trainiert von Sebastian Hoeneß
    SC Freiburg wird trainiert von Christian Streich

1.  Borussia Dortmund entlässt seinen Trainer und stellt “Pep Guardiola”
    ein.

``` python
# insert code here
bundesligaVereine["Borussia Dortmund"] = "Pep Guardiola"
```

1.  Prüfen Sie ob der “Offenburger FV” ein Bundesliga-Verein ist.

``` python
# insert code here
if "Offenburg FV" in bundesligaVereine:
    print("Offenburg FV spielt in der Bundesliga")
```

1.  Wie viel Einträge sind in der Trainerverwaltung für die Bundesliga
    hinterlegt.

``` python
# insert code here
print("Anzahl von Einträgen:",len(bundesligaVereine))
```

    Anzahl von Einträgen: 9

1.  “FC Köln” steigt aus der Bundesliga ab. “Holstein Kiel” mit Trainer
    “Marcel Rapp” schafft den erhofften Aufstieg.

``` python
# insert code here
del bundesligaVereine["FC Köln"]
bundesligaVereine["Holstein Kiel"] = "Marcel Rapp"
```

1.  Die Vereinsverwaltung für die Bundesliga soll um Spielerdaten
    ergänzt werden. Erfassen Sie die Daten hierfür in einem
    geschachtelten Dictionary. Hinterlegen Sie bei den Mannschaften
    neben den Trainern auch Listen mit Tormännern, Abwehrspielern,
    Mittelfeldspielern und Stürmern. (Es reicht, wenn Sie hierfür die
    Daten des FC Bayern erfassen)

``` python
# insert code here
bundesligaVereine = {"FC Bayern München":{"Trainer":"Thomas Tuchel",
                                          "Tormann":["Manuel Neuer","Sven Ulreich","Daniel Peretz"],
                                          "Abwehr":["Matthijs de Ligt","Min-jae Kim","Dayot Upamecano","Eric Dier","Tarek Buchmann","Alphonso Davies","Raphael Guerreiro","Joshua Kimmich"],
                                          "Mittelfeld":["Leon Goretzka","Konrad Laimer","Jamal Musiala","Kingsley Coman", "Mathy Tel"],
                                          "Sturm":["Leroy Sané","Serge Gnabry","Thomas Müller","Harry Kane","Eric-Maxim Choupo-Moting"]
                                         }
                    }
```

1.  Geben Sie alle Abwehrspieler des FCB aus.

``` python
# insert code here
del bundesligaVereine["FC Bayern München"]["Abwehr"][3]
print(len(bundesligaVereine["FC Bayern München"]["Abwehr"]))
```

    7

1.  Wieviel Stürmer hat der FCB aktuell in seinem Kader. Welche?

``` python
# insert code here
print(len(bundesligaVereine["FC Bayern München"]["Sturm"]))
```

    5

1.  Der FCB verkauft seinen Stürmerstar “Harry Kane”. Geben Sie alle
    verbliebenen Stürmer aus.  
    Ermitteln Sie hierfür zunächst die Position an der sich Robert in
    der Liste der Stürmer befindet.

``` python
# insert code here
print(del bundesligaVereine["FC Bayern München"]["Sturm"]
print(len(bundesligaVereine["FC Bayern München"]["Sturm"]))
```

#### Aufgabe 3 - Nachfahren und Vorfahren

1.  Finde mithilfe des gegebenen Dictionary `tochter_mutter` die
    Vorfahren mütterlicherseits einer Frau aus der Liste heraus.
    Beispielausgabe für “Lilli”:

*Lilli ist die Tochter von Anne.  
Anne ist die Tochter von Ursula.  
Ursula ist die Tochter von Lydia.  
Die Mutter von Lydia ist nicht bekannt.* an.

``` python
tochter_mutter = dict(Nicole="Gabi", Anne="Ursula", Margret="Anneliese", Matilda="Anne", 
                      Lilli="Anne", Cornelia="Margret", Marlene="Nicole", Ursula="Lydia")
gesucht = "Lilli"

# Lösung Teil 1:
aktuell = gesucht
while aktuell in tochter_mutter:
    tochter = aktuell
    aktuell = tochter_mutter[tochter]
    print(f"{tochter} ist die Tochter von {aktuell}.")
print(f"Die Mutter von {aktuell} ist nicht bekannt.")
```

    Lilli ist die Tochter von Anne.
    Anne ist die Tochter von Ursula.
    Ursula ist die Tochter von Lydia.
    Die Mutter von Lydia ist nicht bekannt.

Ein dict kann man nicht einfach invertieren, da für verschiedene
Schlüssel derselbe Wert gespeichert sein kann.

1.  Wie könnte man trotzdem aus `tochter_mutter` (s. vorige Aufgabe)
    trotzdem `mutter_toechter` machen?
2.  Zeige alle weiblichen Nachfahren von “Lydia” an.

``` python
# Lösung Teil 2:
mutter_toechter = {}
for tochter in tochter_mutter:
    mutter = tochter_mutter[tochter]
    if mutter not in mutter_toechter:
        mutter_toechter[mutter] = []
    mutter_toechter[mutter].append(tochter)
mutter_toechter
```

    {'Gabi': ['Nicole'],
     'Ursula': ['Anne'],
     'Anneliese': ['Margret'],
     'Anne': ['Matilda', 'Lilli'],
     'Margret': ['Cornelia'],
     'Nicole': ['Marlene'],
     'Lydia': ['Ursula']}

``` python
# Lösung Teil 3:
def alle_nachfahren(mutter):
    ergebnis = []
    if mutter in mutter_toechter:
        for tochter in mutter_toechter[mutter]:
            ergebnis = ergebnis + [tochter] + nachfahren(tochter)
    return ergebnis        

print(alle_nachfahren("Lydia"))
```

    ['Ursula', 'Anne', 'Matilda', 'Lilli']

#### Aufgabe 4 - Analyse von Goethes Faust

In den Aufgaben zu Listen hast du sämtliche Wörter von Goethes *Faust*
in einer Liste gespeichert. Erweitere diese Lösung (s.u.) nun so, dass
die Häufigkeiten für jedes Wort gezählt und in einem Dictionary
`zaehler` gespeichert werden. Gib dann die zehn häufigsten Wörter aus.

Zur Kontrolle hier die zu erwartende Ausgabe:

\[(507, ‘und’), (474, ‘Faust’), (465, ‘die’), (461, ‘ich’), (454,
‘der’), (412, ‘Und’), (395, ‘nicht’), (368, ‘zu’), (312, ‘ist’), (296,
‘ein’)\]

``` python
from urllib.request import urlopen
import string

URL = "https://math-inf.uni-greifswald.de/storages/uni-greifswald/fakultaet/mnf/mathinf/hellmuth/Teaching/AlgorDatastrWS1819/Goethe--Faust.txt"
zeilen = [z.decode("UTF-8") for z in urlopen(URL)]
worte = [wort.strip(string.punctuation) for zeile in zeilen for wort in zeile.split()]

#print(worte)

# Lösungsmöglichkeit 1:
zaehler = {}
for wort in worte:
    if wort not in zaehler:
        zaehler[wort] = 1  # neuer Eintrag mit Wert 1
    else:
        zaehler[wort] += 1 # bestehnder Wert um 1 erhöhen   
    

# Lösungsmöglichkeit 2:
zaehler = {}
for wort in worte:
    zaehler[wort] = zaehler.get(wort, 0) + 1
        
haeufigkeiten = [(zaehler[wort], wort) for wort in zaehler]   # Wichtig: Häufigkeit steht zuerst im Tupel
haeufigkeiten.sort(reverse=True)   # Da Häufigkeit zuerst, wird nach dieser sortiert, und zwar absteigend
print(haeufigkeiten[:10])   # die 10 häufigsten Wörter

# Anmerkung: Es geht sogar noch einfacher, wenn man die Klassen defaultdict oder Counter aus 
# der Python-Standardbibliothek verwendet. 

# Lösungsmöglichkeit 3:
from collections import Counter
zaehler = Counter()
for wort in worte:
    zaehler[wort] += 1  # keine Fallunterscheidung für Initialisierung notwendig
    
print("Lösung mit Klasse Counter:")
print(zaehler.most_common(10))   # praktische Methode!

# Lösungsmöglichkeit 4:
# Die allerallerallerkürzeste Lösung ist dieser Einzeiler:
zaehler = Counter(worte)

print("Lösung mit dem praktischen Konstruktor von Counter:")
print(zaehler.most_common(10))  

#Zum Einlesen:
# https://towardsdatascience.com/python-pro-tip-start-using-python-defaultdict-and-counter-in-place-of-dictionary-d1922513f747
```

    [(507, 'und'), (474, 'Faust'), (465, 'die'), (461, 'ich'), (454, 'der'), (412, 'Und'), (395, 'nicht'), (368, 'zu'), (312, 'ist'), (296, 'ein')]
    Lösung mit Klasse Counter:
    [('und', 507), ('Faust', 474), ('die', 465), ('ich', 461), ('der', 454), ('Und', 412), ('nicht', 395), ('zu', 368), ('ist', 312), ('ein', 296)]
    Lösung mit dem praktischen Konstruktor von Counter:
    [('und', 507), ('Faust', 474), ('die', 465), ('ich', 461), ('der', 454), ('Und', 412), ('nicht', 395), ('zu', 368), ('ist', 312), ('ein', 296)]

#### Aufgabe 5 - Mehrsprachige Anwendungen

Stellen Sie sich vor, wir wollen in einem Programm die Bezeichnungen für
ein Dateimenü internationalisieren, also z.B: in Deutsch, Englisch,
Französisch und Italienisch anbieten.  
Wir wollen ein verschachteltes Dictionary verwenden, in dem wir die
Übersetzung für die Menuüpunkte zum Speichern, Speichern unter neuem
Namen, Neue Datei öffnen, Öffnen und Drucken angeben.

Zum Übersetzen der Begriffe:  
Englisch - Deutsch - Französisch - Italienisch  
File - Datei - Fichier - File  
New - Neu - Nouveau - Nuovo  
Open - Öffnen - Ouvrir - Apri Save - Speichern - Enregister - Salva  
Save as - Speichern unter - Enregistrer sous - Salva come  
Print preview - Druckansicht - Apercu avant impressioner - Anteprima di
stampa Print - Drucken - Imprimer - Stampa  
Close - Schließen - Fermer - Chiudi  
Exit - Verlassen - Quitter - Esci

``` python
menu = {"english":{"file":"File","new":"New","open":"Open","save":"Save","save as":"Save as","print preview":"Print preview","print":"Print","close":"Close","exit":"Exit"},
        "deutsch":{"file":"Datei","new":"Neu","open":"Öffnen","save":"Speichern","save as":"Speichern unter","print preview":"Druckansicht","print":"Drucken","close":"Schließen","exit":"Verlassen"},
        "französisch":{"file":"Fichier","new":"Nouveau","open":"Ouvrir","save":"Enregister","save as":"Enregistrer sous","print preview":"Apercu avant impressioner","print":"Imprimer","close":"Fermer","exit":"Quitter"},
        "italienisch":{"file":"File","new":"Nuovo","open":"Apri","save":"Salva","save as":"Salva come","print preview":"Anteprima di stampa","print":"Stampa","close":"Chiudi","exit":"Esci"}
       }
language = input("Which Language?").lower()
current_dict = menu[language]
print(current_dict)
```

    Which Language? Deutsch

    {'file': 'Datei', 'new': 'Neu', 'open': 'Öffnen', 'save': 'Speichern', 'save as': 'Speichern unter', 'print preview': 'Druckansicht', 'print': 'Drucken', 'close': 'Schließen', 'exit': 'Verlassen'}

#### Aufgabe 6 - Weitere Übung für die ganz Schnellen

Gegeben sei folgendes Dictionary: Finden Sie passende Python-Ausdrücke
mit denen unten stehende Fragestellungen aus dem Dictionary
herausgelesen werden.

``` python
json_data = {
"SuS":[
{"vorname": "Armin",
"nachname": "Gips",
"alter": 21,
"geimpft": True,
"raum": ["G320", "G328", "F403"],
"noten": {
"BFK": 1.5,
"Deutsch": 2,
"GK": 1.8
}},
{"vorname": "Anna",
"nachname": "Bolika",
"alter": 19,
"geimpft": False,
"raum": ["G321", "G326", "F403"],
"noten": {
"BFK": 1.8,
"Deutsch": 1.3,
"GK": 2.7
}},
{"vorname": "Andy",
"nachname": "Tür",
"alter": 22,
"geimpft": True,
"raum": ["G320", "G326", "F405"],
"noten": {
"BFK": 2.1,
"Deutsch": 2.6,
"GK": 3.2
}},
{"vorname": "Rosa",
"nachname": "Wolke",
"alter": 18,
"geimpft": False,
"raum": ["G318", "G326", "F405"],
"noten": {
"BFK": 2.2,
"Deutsch": 2.4,
"GK": 2.1
}},
{"vorname": "Marion",
"nachname": "Nette",
"alter": 23,
"geimpft": True,
"raum": ["G320", "G328", "F405"],
"noten": {
"BFK": 1.1,
"Deutsch": 1.3,
"GK": 1.4
}}
]
}
```

``` python
#a) Wie viele Schüler sind bereits geimpft? Geben Sie Anzahl und Nachnamen der SuS aus. 
geimpfte=0
for s in json_data["SuS"]:
    if s["geimpft"]:
        geimpfte+=1
print("Anzahl geimpfte: ",geimpfte)

#b) Wie viele Schüler sind unter 20 Jahre alt? Geben Sie Anzahl und Nachnamen der SuS aus. 
unter18=0
for s in json_data["SuS"]:
    if s["alter"] < 20:
        unter18+=1
print("Schüler unter 18: ",unter18)

#c) Bestimmen sie das durchschnittliche Alter aller SoS.
alterSumme=0
for s in json_data["SuS"]:
    alterSumme += s["alter"]
durchschnitt = alterSumme / len(json_data["SuS"])
print("Durschnittsalter: ",durchschnitt)

#d) Ein SoS hatte angerufen, leider hat das Seki den Namen nicht vollständig verstanden. 
#   Der Nachnamen endet mit „ika“ – wie lautet der vollständige Namen des SoS? Geben Sie alle Daten aus.
for s in json_data["SuS"]:
    if s["nachname"].endswith("ika"):
        print(s["vorname"],s["nachname"],s["alter"], "ist geimpft:",s["geimpft"])

#e) Welche SoS werden im Unterrichtsraum G328 beschult?
for s in json_data["SuS"]:
    if "G328" in s["raum"]:
        print(s["vorname"],s["nachname"],"wird in G328 beschult")

#f) Welcher SoS hat die beste BFK Note?
bfkNoten=[]
for s in json_data["SuS"]: 
    bfkNote = s["noten"]["BFK"]
    bfkNoten.append(bfkNote)
besteBfkNote = min(bfkNoten)
for s in json_data["SuS"]:
    bfkNote = s["noten"]["BFK"]
    if bfkNote == besteBfkNote:
        print(s["vorname"],s["nachname"], "hat die beste BFK-Note",round(bfkNote,2))

#g) Welchen Notendurchscnitt haben die Schüler im Fach GK erreicht?
gkSumme=0
for s in json_data["SuS"]:
    gkSumme += s["noten"]["GK"]
durchschnitt = gkSumme / len(json_data["SuS"])
print("Durchschnitt in GK: ",durchschnitt)

#h) Welcher SoS hat den besten Gesamtnotendurchschnitt?
mwNoten = []        
for s in json_data["SuS"]:
    noten = s["noten"].values()
    mwNoten.append(sum(noten)/len(noten))
besteNote = min(mwNoten)
for s in json_data["SuS"]:
    noten = s["noten"].values()
    mwNote = sum(noten)/len(noten)
    if mwNote == besteNote:
        print(s["vorname"],s["nachname"], "war der beste Schüler mit einem Schnitt von",round(mwNote,2))
```

    Anzahl geimpfte:  3
    Schüler unter 18:  2
    Durschnittsalter:  20.6
    Anna Bolika 19 ist geimpft: False
    Armin Gips wird in G328 beschult
    Marion Nette wird in G328 beschult
    Marion Nette hat die beste BFK-Note 1.1
    Durchschnitt in GK:  2.24
    Marion Nette war der beste Schüler mit einem Schnitt von 1.27

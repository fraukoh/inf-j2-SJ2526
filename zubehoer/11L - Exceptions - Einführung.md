# Übungen zu Exceptions


1.  Optimieren Sie den Code mithilfe eines finally-Blocks

``` python
try: 
   schalteZündungEin()
   fahreLos()
except MotorFehlerException e:
   logProblem (e)     
finally:
   schalteZündungAus() 
   gangRein() 
   handbremseAnziehen()    
```

1.  Das nachfolgende Programm soll 10 Zahlen über die Tastatur einlesen
    und diese in die Datei ausgabe.txt schreiben. Fangen Sie mögliche
    Fehler sinnvoll ab.

``` python
try:
    file = open("ausgabe.txt",mode='w')
    i=0
    while i<10:
        try:
            zahl = int(input("Zahl: "))
            file.write(str(zahl)+"\n")
            i+=1
        except ValueError as ve: 
            print("Fehlerhafte Eingabe")
            print(ve)
except PermissionError as pe:
    print(pe)
finally:
    file.close()
```

1.  Das folgende Programm soll mögliche Exceptions außerhalb der
    Funktion listeAusgeben() abfangen. Werfen Sie eventuell auftretende
    Exceptions an die aufrufende Stelle.

``` python
def listeAusgeben(filename="test.txt",maxWert=10):
    try:
        file = open(filename,mode="w")
        for i in range(maxWert):
            file.write(str(i)+"\n")
        file.close()
    except:
        raise
try:
    listeAusgeben()
except Exception as e:
    print(e)
```

1.  Das folgende Programm soll vervollständigt werden. Implementieren
    Sie dazu die noch fehlende Methode reverseString(), die den ihr
    übergebenen String in der Reihenfolge dreht und zurückgibt.  
    Wenn der Methode statt einem gültigen String ein None-Zeiger
    übergeben wird, soll ein TypeError mit der Message “ungültiger Text”
    geworfen werden.

``` python
def reverseString(s):
    try:
        rs = s[::-1]
    except TypeError as te:
        raise TypeError("ungültiger Text")
    return rs

try:
    einString = "Dreh mich um"
    print(reverseString(einString))
    einString = None
    print(reverseString(einString))
except TypeError as te:
    print("Fehler: ",te)
```

1.  Fangen Sie mögliche Fehler, die bei der Ausführung auftreten
    könnnen, so differenziert wir möglich ab. Geben Sie die
    Default-Message der Exception aus.

``` python
try:
    file = open("data/zahl.txt",mode="x")
    z = int(input("Zahl: "))
    kw = 1/z
    file.write(str(z))
    file.close()
except ZeroDivisionError as ze:
    print(type(ze))
    print(ze)
except TypeError as e:
    print(type(e))
    print(e)
except FileExistsError as fee:
    print(type(fee))
    print(fee)
except ValueError as ve:
    print(type(ve))
    print(ve)
finally:
    file.close()
```

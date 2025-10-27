# Zeichenketten (Strings)


Neben numerischen Datentypen kennt Python auch Zeichenketten, die häufig
mit dem englischen Ausdruck “Strings” bezeichnet werden. Zeichenkette
bestehen aus einer **unveränderlichen** Folge - also Sequenz von
beliebigen Zeichen.

-   https://www.w3schools.com/python/python_strings.asp

``` python
s1 = 'Ein String mit einfachen Quotes'
s2 = "Nachbar's Dackel heißt Waldi"
s3 = '''Er sagte "Herr Meier's Dackel bellt immer!" '''
print(s1)
print(s2)
print(s3)
```

    Ein String mit einfachen Quotes
    Nachbar's Dackel heißt Waldi
    Er sagte "Herr Meier's Dackel bellt immer!" 

``` python
s4 = "Ein String \
kann auch über \
mehrere Zeilen \
geschrieben werden \
und funktioniert auch mit ' '"
print(s4)
print(len(s4))
```

    Ein String kann auch über mehrere Zeilen geschrieben werden und funktioniert auch mit ' '
    89

## Operationen mit Strings

**Beachte:** Alle String-Funktionen geben neue Werte zurück. Sie ändern
die ursprüngliche Zeichenfolge nicht. - weitere Operationen siehe
https://www.w3schools.com/python/python_strings.asp

``` python
a = " Hallo," + " Welt! " # Strings verketten mit +
print(a)           # " Hallo, Welt! "
b = a.strip()     
print(b)           # "Hallo, Welt!"
c = b.lower()
print(c)           # "hallo, welt!"
d = b.upper()
print(d)           # "HALLO, WELT!"
f = ", " in b      # gibt es auch mit not in
print(f)           # True

e = b.replace(",","").replace("!","")
print(e)           # "Hallo Welt"
splittet = e.split(" ") # Trenne am Trennzeichen " "
print(splittet)    # ['Hallo', 'Welt']
```

     Hallo, Welt! 
    Hallo, Welt!
    hallo, welt!
    HALLO, WELT!
    True
    Hallo Welt
    ['Hallo', 'Welt']

### Strings formatieren

-   siehe https://www.w3schools.com/python/ref_string_format.asp

``` python
txt1 = "Sonderangebot: Nur {price:.2f} Euro!"
txt2 = txt1.format(price = 49.8976) 
print(txt2)
```

### Bei Strings handelt es sich um einen sequenziellen Datentyp

Die einzelnen Zeichen können infolgedessen wie bei einer Liste
angesprochen werden.

``` python
s = "Hallo Welt!"
# Zeichen mittels Index auslesen
for i in range(len(s)):
    print(s[i])
```

``` python
# mit foreach-Schleife durchlaufen
for c in s:
    print(c)
```

``` python
# List Slicing funktioniert auch bei Strings
print(s[6:])     # Welt!
print(s[6:-1])   # Welt
```

### Wie man eine Zeichenfolge in Python in der Reihenfolge umdrehen kann

Angenommen s1 ist eine Zeichenkette. Die Slice-Notation in Python hat
die Syntax `list[<start>:<stop>:<step>]`  
Wenn Sie die Liste also mit `s1[::-1]` durchgehen, wird die Liste vom
Ende zum Anfang durchlaufen, wobei jedes Element genommen wird. Dies
funktioniert auch mit Listen/Tupel.

``` python
s1 = "Hello World"
s2 = s1[::-1]
print(s2)
print(s1==s2)  # Pallindrom?
```

### Was funktioniert nicht!!

``` python
# str und int können nicht mit dem + Operator verküpft werden
age = 17
s = "Hallo"
txt = "My name is John, I am " + age
print(txt)
# wenn dann so!!
#txt = "My name is John, I am " + str(age)
#print(txt)
```

``` python
# Eine Zeichenkette ist unveränderlich (immutable)
# Es können also auch keine einzelnen Zeichen in der Zeichenkette ersetzt werden.
s = "Hello Welt"
s[1] = "a"
```

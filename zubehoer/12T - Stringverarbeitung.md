# Stringverarbeitung


### Der Unterschied zwischen Characters and Strings

Für das Verständis von Characters und Strings ist es wichtig zu wissen,
dass jeder Character mit einer eindeutigen Nummer abgespeichert wird.
Diese Nummer wird auch **code point** genannt. Dier ersten 128 Zeichen
sind im ASCII-Standard definiert, die darüberliegenden code points
werden für nationale Zeichen, wie zum Beispiel das ç. Die Übersetzung
für die verschiedenen Sprachen nennt man **code page**. Nachteil der
code pages ist die Abhängigkeit von der entsprechenden Sprache. So kann
der gleiche code point in verschiedenen code pages ein anderes Zeichen
bedeuten. Der Unicode löst dieses Problem. Python selbst unterstützt
Unicode und UTF-8, dadurch können alle interationalen Zeichen sowohl in
Variablen, Einheiten und Inhalten verwendet werden.

Strings in Python sind unveränderbar (immutable).

``` python
str1 = 'a'
str2 = "b"
# Mehrzeiliger Text
str3 = '''0123456789\n0012345678'''
print(str3)

# der + und *-Operator
print(str1+str2)
print(str1*5)
print(4*str2)

#Character in Zahl, Zahl in Character
z1 = 'z'
codepoint = ord(z1)  # 122 dec -> 7A hex
z2 = chr(codepoint)

print("Der code point von",z1,"ist",codepoint)
print("Das Zeichen mit dem codepoint",codepoint,"ist ",z2)

# Die Funktion len()
print(len(str1))
print(len(str3)) # hier ist zu beachten, dass das Steuerzeichen für den Zeilenumbruch als Zeichen mitgezählt wird
```

    0123456789
    0012345678
    ab
    aaaaa
    bbbb
    Der code point von z ist 122
    Das Zeichen mit dem codepoint 122 ist  z
    1
    21

### String als Liste

Ein String verhält sich wie eine Liste. Dadurch kann an einer bestimmten
Stelle zugegriffen werden und bestimmte Zeichenfolgen ausgeschnitten
werden

``` python
alphabet = "abcdefghijklmnopqrstuvwxyz"

# Das Alphabet auseinandergerückt
for ix in range(len(alphabet)):
    print(alphabet[ix], end=' ')
print()   

# Das Ganze rückwärts
print(alphabet[::-1])

#Slicing [start,stop,schrittweite]
print("Die ersten 10 Zeichen:",alphabet[:10])
print("Vom 10. bis zum 20. Zeichen:",alphabet[9:20])
print("vom 2. bis zum 10. Zeichen immer nur jedes zweite:",alphabet[1:10:2])

# Überprüfen eines Zeichens im String
print("q" in alphabet)
print("1" in alphabet)
print("ghi" not in alphabet)
print("ABC" not in alphabet)

# Nicht erlaubt sind del, insert, append - String is immutable!

# weitere Funktionen, die sich auf den code point beziehen
print(min("abcABC"))
print(max("abcABC"))

# Index des ersten Vorkommens von "A"
print("abcABC".index("A")) 
# Anzahl des Vorkommens von "A"
print("abcABCA".count("A"))
```

### String-Methoden

Übersicht der relevanten Methoden finden Sie unter
https://docs.python.org/3.4/library/stdtypes.html#string-methods

``` python
str = "Hallo Welt, hallo Erde"
# Umwandeln in Großbuchstaben
print(str.upper())
# Umwandeln in Kleinbuchstaben
print(str.lower())
# Umwandeln des ersten Zeichen in Großbuchstaben und die restlichen Zeichen in Kleinbuchstaben
print(str.capitalize())
# wortweises Umwandeln wie bei capitalize()
print(str.title())
# Umwandeln von klein in groß und umgekehrt
print(str.swapcase())
```

``` python
#Zentrieren einer Zeichenfolge durch Einpacken mit Blanks
print("["+str.center(30)+"]")
```

``` python
# Überprüfen, ob eine Zeichenfolge mit einer bestimmten Zeichenfolge endet
print("Guten Morgen".endswith("gen"))
# oder anfängt
print("Guten Morgen".startswith("Gu"))
```

``` python
# Finden des ersten Vorkommens einer Zeichenfolge (Zeichenfolge, Start, Stop)
gruss = "Guten Morgen"
print(gruss.find("n"))
# beginnend ab dem 5. Zeichen
print(gruss.find("n",5))
# beginnend ab dem 5. Zeichen bis vor das 11. Zeichen
print(gruss.find("n",5,11))

#von rechts suchen
print("Narri Narro".rfind("rr"))
print("Narri Narro".rfind("rr",9))
print("Narri Narro".rfind("rr",0,9))
```

``` python
# Überprüfen, ob eine Zeichenfolge ausschließlich Ziffern und alphabetische Zeichen enthält
print("Hallo".isalnum())
print("123".isalnum())
print("Hallo3".isalnum())
print("Hallo3&".isalnum())
print("".isalnum())
```

    True
    True
    True
    False
    False

``` python
# Überprüft, ob ein String nur aus Buchstaben besteht.
print("Hallo".isalpha())    # True
print("Hallo123".isalpha()) # False
```

``` python
# Überprüft, ob ein String nur aus numerischen Zeichen besteht, 
# einschließlich Ziffern (0-9) und anderen numerischen Zeichen wie 
# z.B. Unicode-Zeichen für Brüche oder Exponenten
print("123".isnumeric())    # True
print("②".isnumeric())      # True
print("²".isnumeric())      # True
print("₀".isnumeric())      # True
print("Ⅲ".isnumeric())     # True
print("¼".isnumeric())      # True
print("1/2".isnumeric())    # Achtung: False
```

    True
    True
    True
    True
    True
    True
    False

``` python
# Überprüft, ob ein String nur aus Ziffern besteht.
print("123".isdigit())      # True
print("123abc".isdigit())   # False
print("②".isdigit())        # True
print("²".isdigit())        # True
print("₀".isdigit())        # True
print("Ⅲ".isdigit())       # False
print("¼".isdigit())        # False
```

``` python
# Überprüft, ob ein String eine gültige Dezimalzahl ist.
print("123".isdecimal())   # True
print("123.45".isdecimal())# False
print("123,45".isdecimal())# False
print("Hallo".isdecimal()) # False
print("123abc".isdecimal())# False
print("¼".isdecimal())     # False
print("②".isdecimal())     # False
print("²".isdecimal())     # False
print("₀".isdecimal())     # False
print("Ⅲ".isdecimal())    # False
```

``` python
# Überprüft, ob ein String nur aus alphabetische Zeichen und aus numerischen Zeichen besteht.
print("Hallo".isalnum())    # True
print("123".isalnum())      # True
print("Hallo123".isalnum()) # True
print("HalloⅢ②¼".isalnum())# True
print("Hallo 123".isalnum())# False
print("Hallo3&".isalnum())  # False
print("".isalnum())         # False
```

``` python
# Überprüft, ob ein String nur aus Leerzeichen besteht.
print(" ".isspace())        # True
print("".isspace())         # False
print(" ,. ".isspace())     # False
```

``` python
#andere Überprüfungsroutinen
print("Hallo Welt".islower()) # False
print("hallo welt".islower()) # True
print("HALLO WELT".isupper()) # True
print("Hallo Welt".istitle()) # True
```

``` python
#Verknüpfung mit separator.join(liste) und wieder in eine Liste wandeln mit text.split(separator)
listeA = ["Hallo","wie","geht's"]
zeile = ":".join(listeA)
listeB = zeile.split(":")
print(listeA)
print(zeile)
print(listeB)
```

``` python
#Trim-Methoden: strip(), lstrip(), rstrip()
print("["+"  Hallo!   ".strip()+"]")
print("["+"  Hallo!   ".lstrip()+"]")
print("["+"  Hallo!   ".rstrip()+"]")
print("www.cisco.com".lstrip("www.")) # statt führende Lehrzeichen, werden jetzt führende www. entfernt (es würde auch w. reichen)
print("www.tagesschau.de".rstrip(".de"))
```

``` python
#Replace-Methode:
print("Narri Narro".replace("a","aa"))
print("Narri Narro".replace("a","aa",1)) # maximal eine Ersetzung
```

``` python
# Vergleiche von Strings
# Dabei wird immer von links nach rechts verglichen. 
print("Abcde">"b") # False, da der code point von "A" kleiner ist als von "b"
print("abc">"ab")  # True, da bei gleichlautenden Strings der längere größer ist
```

### String in action

``` python
# Sortieren von Listen mit Texten
liste = ["eins","zwei","drei"]
listesortiert = sorted(liste)
print(liste)
print(listesortiert)
liste.sort()
print(liste)
```

# Lösungen: Funktionen


### Listen

##### Aufgabe 1a

Schreibe eine Funktion `schreibe_hoch3`, die als Argument eine Zahl *x*
übergeben bekommt, daraus den Wert *x*<sup>3</sup> berechnet und diesen
**ausgibt**.

##### Lösung

``` python
def schreibe_hoch3(x):
    print(x**3)
    
schreibe_hoch3(4)
```

    64

##### Aufgabe 1b

Schreibe eine Funktion `hoch3`, die als Argument eine Zahl *x* übergeben
bekommt, daraus den Wert *x*<sup>3</sup> berechnet und diesen
**zurückliefert**.

##### Lösung

``` python
def hoch3(x):
    return x**3
```

##### Aufgabe 1c

Teste in der folgenden Zelle, ob deine Implementation von `hoch3()`
korrekt funktioniert.

``` python
testdaten = [(-2, -8),  (-1.5, -3.375),  (-1, -1),  (-0.5, -0.125),  (0, 0),  (0.5, 0.125),  (1, 1),  (1.5, 3.375),  (2, 8),  (2.5, 15.625),  (3, 27)]

for x, x_hoch_3 in testdaten:
    assert x_hoch_3 == hoch3(x), "Irgend etwas stimmt mit deine Funktion hoch3() noch nicht!"
```

##### Aufgabe 2

Schreibe eine Funktion, die Vorname, Nachname und evtl. den zweiten
Vornamen einer Person übergeben bekommt und den vollständigen Namen
zurückliefert (d.h. einen einzigen String, in dem alle Teile des Namens
durch Leerzeichen getrennt sind

<details>
<summary>
Hier klicken für Tipps
</summary>
<p>
Nutze ein Default-Argument.
</p>
<p>
Nutze die String-Methode join().
</p>
</details>

##### Lösung

``` python
def name_vollstaendig(vorname, nachname, vorname2=""):
    teile = [vorname, vorname2, nachname]
    return " ".join(n for n in teile if n != "")


# Tests für deine Lösung:
assert name_vollstaendig("Guido", "van Rossum") == "Guido van Rossum", "Irgend etwas stimmt mit deiner Funktion name_vollstaendig() noch nicht!"
assert name_vollstaendig("Wolfgang", "Mozart", vorname2="Amadeus") == "Wolfgang Amadeus Mozart", "Irgend etwas stimmt mit deiner Funktion name_vollstaendig() noch nicht!"
```

##### Aufgabe 3

Das folgende Programm zeichnet ein Quadrat der Seitenlänge 6. (Aus
optischen Gründen wird in der Horizontalen nach jedem Sternchen ein
Leerzeichen eingefügt.)

``` python
for _ in range(6):
    print("* ", end="")
print()
for _ in range(4):
    print("*", end="")
    for _ in range(9):
        print(" ", end="")
    print("*")
for _ in range(6):
    print("* ", end="")
print()
```

    * * * * * * 
    *         *
    *         *
    *         *
    *         *
    * * * * * * 

##### a) Schreibe eine Funktion `quadrat(n)`, die ein Quadrat mit beliebiger Seitenlänge `n` zeichnet.

``` python
def quadrat(n):
    print("* " * n)
    for _ in range(n-2):
        print("* " + "  " * (n-2) + "*")
    print("* " * n)

quadrat(6)  # sollte die gleichen Ausgabe erzeugen wie das Originalprogramm
```

    * * * * * * 
    *         *
    *         *
    *         *
    *         *
    * * * * * * 

##### b) Ändere `quadrat()` so ab, dass für dem Rand und das Innere des Quadrats auch andere Zeichen gewählt werden können. Z.B. so:

    # # # # # # # # 
    # - - - - - - #
    # - - - - - - #
    # - - - - - - #
    # - - - - - - #
    # - - - - - - #
    # - - - - - - #
    # # # # # # # # 

``` python
def quadrat(n, rand="*", innen=" "):
    print(f"{rand} " * n)
    for _ in range(n-2):
        print(f"{rand} " + f"{innen} " * (n-2) + rand)
    print(f"{rand} " * n)

#quadrat(8,innen="o")    
quadrat(8, innen="-", rand="#")
```

    # # # # # # # # 
    # - - - - - - #
    # - - - - - - #
    # - - - - - - #
    # - - - - - - #
    # - - - - - - #
    # - - - - - - #
    # # # # # # # # 

##### Aufgabe 4

In einem Schachprogramm wird wie in der folgenden Abbildung jedes Feld
des Schachbretts durch eine Zahl zwischen 0 und 63 codiert:

<img src="images/chessboard01.png" width="20%">

Schreibe eine Funktion `koordinaten(pos)`, die eine Position `pos` in
die übliche Koordinatenform (A1 bis H8) umrechnet.

<img src="images/chessboard02.png" width="20%">

Dabei sollen die Koordinaten als “Paar”, d.h. als *Tupel* mit zwei
Elementen, zurückgeliefert werden.

Bsp. `koordinaten(0)` liefert das Tupel `("a", 8)`, denn das Feld links
oben hat die Position 0 bzw die Koordinate a8.

##### Lösung

``` python
def koordinaten(pos):
    zeile, spalte = divmod(pos, 8)    # entspricht: zeile // 8, spalte % 8
    return chr(spalte + ord('a')), 8 - zeile
#    return chr(spalte + 97), 8 - zeile

# Tests zur Selbstkontrolle:
tests = [(0, ('a', 8)), (1, ('b', 8)), (2, ('c', 8)), (3, ('d', 8)), (4, ('e', 8)), (5, ('f', 8)), (6, ('g', 8)), (7, ('h', 8)), 
         (8, ('a', 7)), (9, ('b', 7)), (10, ('c', 7)), (11, ('d', 7)), (12, ('e', 7)), (13, ('f', 7)), (14, ('g', 7)), (15, ('h', 7)), 
         (16, ('a', 6)), (17, ('b', 6)), (18, ('c', 6)), (19, ('d', 6)), (20, ('e', 6)), (21, ('f', 6)), (22, ('g', 6)), (23, ('h', 6)), 
         (24, ('a', 5)), (25, ('b', 5)), (26, ('c', 5)), (27, ('d', 5)), (28, ('e', 5)), (29, ('f', 5)), (30, ('g', 5)), (31, ('h', 5)), 
         (32, ('a', 4)), (33, ('b', 4)), (34, ('c', 4)), (35, ('d', 4)), (36, ('e', 4)), (37, ('f', 4)), (38, ('g', 4)), (39, ('h', 4)), 
         (40, ('a', 3)), (41, ('b', 3)), (42, ('c', 3)), (43, ('d', 3)), (44, ('e', 3)), (45, ('f', 3)), (46, ('g', 3)), (47, ('h', 3)), 
         (48, ('a', 2)), (49, ('b', 2)), (50, ('c', 2)), (51, ('d', 2)), (52, ('e', 2)), (53, ('f', 2)), (54, ('g', 2)), (55, ('h', 2)), 
         (56, ('a', 1)), (57, ('b', 1)), (58, ('c', 1)), (59, ('d', 1)), (60, ('e', 1)), (61, ('f', 1)), (62, ('g', 1)), (63, ('h', 1))]

for pos, erwartet in tests:
    ergebnis = koordinaten(pos)
    assert ergebnis == erwartet, f"Erwartetes Tupel: {erwartet}  != dein Ergebnis: {ergebnis}"
```

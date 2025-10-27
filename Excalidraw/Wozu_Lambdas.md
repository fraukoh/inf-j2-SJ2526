### **Was sind Lambda-Funktionen in Python?**

Lambda-Funktionen in Python sind **anonyme Funktionen**, die keine Namen haben und direkt definiert werden können. Sie werden mit dem Schlüsselwort `lambda` erstellt und sind besonders nützlich, wenn du eine Funktion nur einmal oder für eine kurze Aufgabe benötigst. Die Syntax ist kompakt und sieht so aus:

python

```python
lambda argumente: ausdruck
```

Ein Beispiel:

python

```python
square = lambda x: x * x
print(square(5))  # Ausgabe: 25
```

Hier wird eine Lambda-Funktion erstellt, die eine Zahl quadriert. Sie ist kürzer als eine reguläre Funktion, die mit `def` definiert wird.

---

### **Wann und wozu verwendet man Lambda-Funktionen?**

Lambda-Funktionen sind besonders nützlich in folgenden Szenarien:

#### **1. Inline-Funktionen für kurze Aufgaben**

Wenn du eine Funktion nur einmal benötigst, z. B. als Argument für eine andere Funktion, kannst du eine Lambda-Funktion verwenden. Das spart Platz und macht den Code übersichtlicher. Beispiel:

python

```python
nums = [1, 2, 3, 4]
squared = list(map(lambda x: x * x, nums))
print(squared)  # Ausgabe: [1, 4, 9, 16]
```

Hier wird `map` verwendet, um eine Lambda-Funktion auf jedes Element der Liste anzuwenden.

#### **2. Verwendung mit Funktionen wie `map`, `filter` und `sorted`**

Lambda-Funktionen sind ideal für Funktionen, die andere Funktionen als Argumente akzeptieren, wie `map`, `filter` oder `sorted`

[](https://codegree.de/python-lambda-anonyme-funktionen-in-python/)

. Beispiel mit `filter`:

python

```python
nums = [1, 2, 3, 4, 5]
even_nums = list(filter(lambda x: x % 2 == 0, nums))
print(even_nums)  # Ausgabe: [2, 4]
```

#### **3. Kürzere und lesbare Code-Snippets**

Lambda-Funktionen können den Code kompakter machen, besonders wenn die Funktion einfach ist und nur eine Zeile umfasst

. Beispiel mit `sorted`:

python

```python
pairs = [(1, 'one'), (2, 'two'), (3, 'three')]
sorted_pairs = sorted(pairs, key=lambda x: x[1])
print(sorted_pairs)  # Ausgabe: [(1, 'one'), (3, 'three'), (2, 'two')]
```

---

### **Wann sollte man Lambda-Funktionen vermeiden?**

Obwohl Lambda-Funktionen praktisch sind, gibt es Situationen, in denen sie nicht ideal sind:

1. **Komplexe Logik**: Wenn die Funktion mehr als eine Zeile oder komplexe Logik enthält, ist es besser, eine reguläre Funktion mit `def` zu verwenden, da dies die Lesbarkeit erhöht.
2. **Wiederverwendbarkeit**: Lambda-Funktionen sind anonym und können nicht wiederverwendet werden, was sie für umfangreichere Aufgaben ungeeignet macht.

---

### **Zusammenfassung**

Lambda-Funktionen sind eine großartige Möglichkeit, **kurze und einmalige Funktionen** zu erstellen. Sie sind besonders nützlich in Kombination mit Funktionen wie `map`, `filter` und `sorted`, um den Code kompakter und lesbarer zu machen. Für komplexere Aufgaben oder wiederverwendbare Funktionen solltest du jedoch reguläre benannte Funktionen verwenden.
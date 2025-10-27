# File Processing


### Zugriff auf Dateien

**open(filename,modus\[,codierung\])**<br> Die open-Funktion bietet dem
Programmierer verschiedene Öffnen-Modi. Dabei wird die Art der zu
öffnenden Datei (Text oder Bytearray) sowie der Zugriffsmodus
mitgegeben:

<img src="images/openmodus.png" width=300>

Da t für Text-File der Standard ist, kann das das t auch weggelassen
werden.<br> Der Standard für die Codierung hängt vom eingesetzten
Betriebssystem ab. Um hier auf Nummer sicher zu gehen, kann man hier
**encoding=‘UTF8’** angeben.

``` python
datei = open('data/adressen.txt','r', encoding='UTF8') #nur lesen
for zeile in datei:
    print(zeile.strip())
datei.close()    
    
print(40 *'*')

#Alternative 
with open('data/adressen.txt','r') as datei:
    for zeile in datei:
        strzeile = zeile.strip()
        datenzeile = strzeile.split(';')
        for wert in datenzeile:
            print(wert,end=' ')
        print('\n'+40 * '*')    
```

    Frank;Meyer;Radolfzell;07732/43452
    Peter;Rabe;Konstanz;07531/70021
    Otmar;Huber;Rosenheim;08031/7877-0
    Anna;Rabe;Radolfzell;07732/2343
    Oskar;Lindner;Konstanz;07531/890
    Anna;List;München;089/3434544
    Franziska;Huber;Rosenheim;08031/787878
    Sarah;Rabe;Konstanz;07531/343454
    ****************************************
    Frank Meyer Radolfzell 07732/43452 
    ****************************************
    Peter Rabe Konstanz 07531/70021 
    ****************************************
    Otmar Huber Rosenheim 08031/7877-0 
    ****************************************
    Anna Rabe Radolfzell 07732/2343 
    ****************************************
    Oskar Lindner Konstanz 07531/890 
    ****************************************
    Anna List München 089/3434544 
    ****************************************
    Franziska Huber Rosenheim 08031/787878 
    ****************************************
    Sarah Rabe Konstanz 07531/343454 
    ****************************************

# Dateien beschreiben oder Werte anhängen

``` python
#Schreiben-Modus
with open('data/zahlen.txt','w') as datei:
    liste = [1,2,3,4,5]
    for wert in liste:
        datei.write(str(wert)+' ')
        
with open('data/zahlen.txt','r') as datei:                    
    for zeile in datei:
        print(zeile.strip())
```

    1 2 3 4 5

``` python
#Anhängen-Modus
with open('data/zahlen.txt','a') as datei:
    liste = [6,7,8,9]
    for wert in liste:
        datei.write(str(wert)+' ')

with open('data/zahlen.txt','r') as datei:
    for zeile in datei:
        print(zeile.strip())

                    
        
```

    1 2 3 4 5 6 7 8 9 6 7 8 9

## Fehlerbehandlung bei der Dateiverarbeitung

Typische Fehler, wie “Datei nicht vorhanden” sollten in einer
Fehlerbehandlung abgefangen werden.

``` python
try:
    with open('data/adresssen.txt','r') as datei:
        for zeile in datei:
            print(zeile.strip())
except Exception as exc:
    print("Cannot open the file:", exc)           
```

    Cannot open the file: [Errno 2] No such file or directory: 'data/adresssen.txt'

``` python
from os import strerror
try:
    with open("data/adresssen.txt", "r") as datei:
        print(datei.read())
except Exception as exc:
    print("The file could not be opened:", strerror(exc.errno));
```

    The file could not be opened: No such file or directory

#### Fehlercodes

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>errno</th>
<th>strerrno</th>
<th>description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>errno.EACCES</td>
<td>Permission denied</td>
<td>The error occurs when you try, for example, to open a file with the
read only attribute for writing.</td>
</tr>
<tr class="even">
<td>errno.EBADF</td>
<td>Bad file number</td>
<td>The error occurs when you try, for example, to operate with an
unopened stream.</td>
</tr>
<tr class="odd">
<td>errno.EEXIST</td>
<td>File exists</td>
<td>The error occurs when you try, for example, to rename a file with
its previous name.</td>
</tr>
<tr class="even">
<td>errno.EFBIG</td>
<td>File too large</td>
<td>The error occurs when you try to create a file that is larger than
the maximum allowed by the operating system.</td>
</tr>
<tr class="odd">
<td>errno.EISDIR</td>
<td>Is a directory</td>
<td>The error occurs when you try to treat a directory name as the name
of an ordinary file.</td>
</tr>
<tr class="even">
<td>errno.EMFILE</td>
<td>Too many open files</td>
<td>The error occurs when you try to simultaneously open more streams
than acceptable for your operating system.</td>
</tr>
<tr class="odd">
<td>errno.ENOENT</td>
<td>No such file or directory</td>
<td>The error occurs when you try to access a non-existent
file/directory.</td>
</tr>
<tr class="even">
<td>errno.ENOSPC</td>
<td>No space left on device</td>
<td>The error occurs when there is no free space on the media.</td>
</tr>
</tbody>
</table>

## bytearrays

Dateien können auch als sogenannte bytearrays geöffnet werden. Unter
einem bytearray kann man einen Container mit lauter bytes verstehen. Sie
werden zum Beispiel für Bilder benutzt. Um einen bytearray zu erzeugen,
benutzt man dessen Konstruktor. Der Parameter gibt die Anzahl der Felder
an, die auch gleich mit 0 initialisiert werden.

``` python
data = bytearray(10)
print(data)
```

    bytearray(b'\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00')

Wie man sieht, werden die Werte als Hexadezimalen abgebildet. Bei der
Belegung der Inhalte ist nur der Wertebereich 0-255 gültig. Alles andere
führt zu einem Typenfehler

``` python
data = bytearray(10)

for i in range(len(data)):
    data[i] = i

for b in data:
    print(hex(b))
```

    0x0
    0x1
    0x2
    0x3
    0x4
    0x5
    0x6
    0x7
    0x8
    0x9

Jetzt noch den bytearray in die Datei schreiben

``` python
from os import strerror

#Bytearray erzeugen und belegen
data = bytearray(10)

for i in range(len(data)):
    data[i] = 10 + i

#Datei beschreiben    
try:
    with open('file.bin', 'wb') as bf:
        bf.write(data)
except IOError as e:
    print("I/O error occurred:", strerr(e.errno))

#Datei lesen    
try:
    with open('file.bin', 'rb') as bf:
        bf.readinto(data)
        for b in data:
            print(hex(b),end=' ')
            
except IOError as e:
    print("I/O error occurred:", strerr(e.errno))
```

    0xa 0xb 0xc 0xd 0xe 0xf 0x10 0x11 0x12 0x13 

Um eine Binärdatei zu lesen, kann man auch den read()-Befehl benutzen.
Dieser liest den kompletten Inhalt der Datei aus, der dann direkt über
den bytearray über den Konstruktor befüllen kann. Diese Methode sollte
man nur anwenden, wenn man sicher ist, dass diese Menge auch im Speicher
Platz hat. Um nur eine bestimmte Anzahl bytes einzulesen, kann man die
Anzahl der bytes als Parameter mitgeben.

``` python
data = bytearray(5)
try:
    with open('file.bin', 'rb') as bf:
        data = bytearray(bf.read())

    for b in data:
        print(hex(b), end=' ')

except IOError as e:
    print("I/O error occurred:", strerr(e.errno))
```

    0xa 0xb 0xc 0xd 0xe 

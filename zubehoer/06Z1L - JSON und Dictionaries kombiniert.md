# Übungsaufaufgaben zu JSON und Dictionaries


**1. Erzeugen Sie ein geschachteltes Dictionary für einen Sensorwert,
der wie folgt aufgebaut sein könnte.**

`{'Sensor': 'DHT12', 'Messwert': {'Temperatur': {'Wert': 27.5, 'Einheit': 'Grad'}, 'Feuchtigkeit': {'Wert': 65.5, 'Einheit': '%'}}}`

Speichern Sie den Sensorwert in der Datei *sensorwert.json*.

``` python
import json

temperaturwert = 27.5
feuchtigkeitswert = 65.5
# Variante 1: Dicts schachteln
temperatur = {"Wert":temperaturwert,"Einheit":"Grad"}
feuchtigkeit = {"Wert":feuchtigkeitswert,"Einheit":"%"}
messwert = {"Temperatur":temperatur,"Feuchtigkeit":feuchtigkeit}
sensorwert = {"Sensor":"DHT12","Messwert":messwert}

# Variante 2: Gleich ein geschachteltes Dict aufbauen
sensorwert = {
   "Sensor":"DHT12",
    "Messwert": {
        "Temperatur":{
            "Wert":temperaturwert,
            "Einheit":"Grad"
        }, 
        "Feuchtigkeit":{
            "Wert":feuchtigkeitswert,
            "Einheit":"%"
        }
    } 
}
print(sensorwert)
with open("data/sensorwert.json", "w") as outfile: 
    json.dump(sensorwert, outfile)
```

    {'Sensor': 'DHT12', 'Messwert': {'Temperatur': {'Wert': 27.5, 'Einheit': 'Grad'}, 'Feuchtigkeit': {'Wert': 65.5, 'Einheit': '%'}}}

**2. Im IOT-Umfeld wurde folgende Nachricht als JSON-String
verschickt.**  
a) Welche Helligkeit hat der BH1750 Sensor gemessen?  
b) Welche Temperatur wurde von den beiden Sensoren im Mittel gemessen?  
c) Wie ist der Luftdruck zum Zeitpunkt der Messung?  
d) Wie ist die gemessene Feuchtigkeit?  
e) Geben Sie den Taupunkt mit Einheit aus.  
f) Wann wurde der Messwert erfasst (Datum und Uhrzeit).

``` python
import json 
json_string = """{"Time":"2021-09-02T16:04:21",
       "BMP180":{"Temperature":30.7,"Pressure":1005.0},
       "BH1750":{"Illuminance":190},
       "SHT3X":{"Temperature":29.1,"Humidity":46.3,"DewPoint":16.4},
       "PressureUnit":"hPa",
       "TempUnit":"C"}"""
json_dict = json.loads(json_string)
#print(json_dict)

#a) Welche Helligkeit hat der BHT1750 Sensor gemessen? 
print(json_dict["BH1750"]["Illuminance"])
#b) Welche Temperatur wurde von den beiden Sensoren im Mittel gemessen?  
print((json_dict["BMP180"]["Temperature"]+json_dict["SHT3X"]["Temperature"])/2,json_dict["TempUnit"])
#c) Wie ist der Luftdruck zum Zeitpunkt der Messung?   
print(json_dict["BMP180"]["Pressure"],json_dict["PressureUnit"])
#d) Wie ist die gemessene Feuchtigkeit? 
print(json_dict["SHT3X"]["Humidity"])
#e) Geben Sie den Taupunkt mit Einheit aus.
print(json_dict["SHT3X"]["DewPoint"])
#f) Wann wurde der Messwert erfasst (Datum und Uhrzeit).
s_Time = json_dict["Time"]
sa_Time = s.split("T")
print("Datum: ", sa_Time[0])
print("Uhrzeit: ", sa_Time[1])
```

**3. Zugriff auf Openweather-Map**  
Unten stehende Programmsequenz tätigt einen Zugriff auf
https://openweathermap.org/. Bei dieser http-Anfrage wird als Ergebnis
das aktuelle Offenburger Wetter als JSON-String zurück geliefert.  
a) Verschaffen Sie sich zunächst einen eigenen API key bei
Openweather-Map https://home.openweathermap.org/users/sign_in  
b) Tragen Sie diesen in der unten stehenden Programm-Sequenz ein. Führen
Sie das Programm aus.  
c) Ermitteln Sie den Längen- und Breitengrad für Offenburg aus dem
JSON-String.  
d) Lesen Sie aus dem JSON-String die aktuelle Temperatur,
Luftfeuchtigkeit und Luftdruck aus.

``` python
import requests
import json

APPID = "API KEY"
owmUrl = "http://api.openweathermap.org/data/2.5/weather?q=Offenburg,de&units=metric&APPID="+APPID
res = requests.get(url=owmUrl)
raw = json.loads(res.text)
print(raw)
lon = raw.get('coord').get('lon')
lat = raw.get('coord').get('lat')

print("Längengrad:",lon)
print("Breitengrad:",lat)

t = raw.get('main').get('temp')
h = raw.get('main').get('humidity')
p = raw.get('main').get('pressure')

print("Temperatur:",t,"°C")
print("Luftfeuchtigkeit:",h,"%")
print("Luftdruck:",p,"mbar")
```

    {'coord': {'lon': 7.9333, 'lat': 48.4833}, 'weather': [{'id': 803, 'main': 'Clouds', 'description': 'broken clouds', 'icon': '04d'}], 'base': 'stations', 'main': {'temp': 10.3, 'feels_like': 9.32, 'temp_min': 8.82, 'temp_max': 11.25, 'pressure': 1020, 'humidity': 74}, 'visibility': 10000, 'wind': {'speed': 4.12, 'deg': 190}, 'clouds': {'all': 75}, 'dt': 1699436713, 'sys': {'type': 2, 'id': 19903, 'country': 'DE', 'sunrise': 1699424671, 'sunset': 1699459169}, 'timezone': 3600, 'id': 2857798, 'name': 'Offenburg', 'cod': 200}
    Längengrad: 7.9333
    Breitengrad: 48.4833
    Temperatur: 10.3 °C
    Luftfeuchtigkeit: 74 %
    Luftdruck: 1020 mbar

``` python
# Zur Sicherheit eine mögliche Antwort der Anfrage
res_text = """
{"coord": {"lon": 7.9333, "lat": 48.4833}, "weather": [{"id": 800, "main": "Clear", "description": "clear sky", "icon": "01d"}], "base": "stations", "main": {"temp": 25.84, "feels_like": 25.79, "temp_min": 24.82, "temp_max": 27.16, "pressure": 1015, "humidity": 50}, "visibility": 10000, "wind": {"speed": 2.06, "deg": 10}, "clouds": {"all": 0}, "dt": 1631104089, "sys": {"type": 1, "id": 1317, "country": "DE", "sunrise": 1631076930, "sunset": 1631123805}, "timezone": 7200, "id": 2857798, "name": "Offenburg", "cod": 200}
"""
```

**4. Wetter vorher sagen mit Openweather-Map**  
Nutzen Sie folgende Url zum Zugriff auf Openweather-Map. Damit kann eine
Wettervorhersage für die nächsten 5 Tage für Offenburg abgerufen werden.
Lesen Sie aus der Antwort ein paar Daten aus.

``` python
import datetime
owmUrl = "http://api.openweathermap.org/data/2.5/forecast?q=Offenburg&mode=json&lang=de&units=metric&APPID="+APPID
res = requests.get(url=owmUrl)
raw = json.loads(res.text)
with open("forecast.json","w") as outFile:
    json.dump(raw,outFile)
#print(raw)
data_list = raw["list"]
#print(data_list)
for data_set in data_list:
    date_time = datetime.datetime.fromtimestamp( data_set["dt"] )  
    print(f"Temperatur: {data_set['main']['temp']:4.1f} - Pressure: {data_set['main']['pressure']} bar - Humidity: {data_set['main']['humidity']}%")
```

    2023-11-08 13:00:00
    Temperatur: 11.1 - Pressure: 1020 bar - Humidity: 68%
    2023-11-08 16:00:00
    Temperatur: 10.7 - Pressure: 1018 bar - Humidity: 67%
    2023-11-08 19:00:00
    Temperatur:  7.2 - Pressure: 1016 bar - Humidity: 79%
    2023-11-08 22:00:00
    Temperatur:  6.8 - Pressure: 1015 bar - Humidity: 79%
    2023-11-09 01:00:00
    Temperatur:  6.5 - Pressure: 1013 bar - Humidity: 74%
    2023-11-09 04:00:00
    Temperatur:  6.5 - Pressure: 1011 bar - Humidity: 68%
    2023-11-09 07:00:00
    Temperatur:  9.2 - Pressure: 1010 bar - Humidity: 64%
    2023-11-09 10:00:00
    Temperatur:  9.0 - Pressure: 1012 bar - Humidity: 79%
    2023-11-09 13:00:00
    Temperatur:  9.9 - Pressure: 1010 bar - Humidity: 78%
    2023-11-09 16:00:00
    Temperatur:  9.3 - Pressure: 1009 bar - Humidity: 85%
    2023-11-09 19:00:00
    Temperatur:  9.1 - Pressure: 1008 bar - Humidity: 88%
    2023-11-09 22:00:00
    Temperatur:  9.6 - Pressure: 1007 bar - Humidity: 80%
    2023-11-10 01:00:00
    Temperatur:  9.5 - Pressure: 1006 bar - Humidity: 80%
    2023-11-10 04:00:00
    Temperatur:  8.7 - Pressure: 1005 bar - Humidity: 88%
    2023-11-10 07:00:00
    Temperatur:  8.1 - Pressure: 1006 bar - Humidity: 84%
    2023-11-10 10:00:00
    Temperatur:  9.0 - Pressure: 1007 bar - Humidity: 74%
    2023-11-10 13:00:00
    Temperatur: 10.6 - Pressure: 1006 bar - Humidity: 62%
    2023-11-10 16:00:00
    Temperatur:  9.0 - Pressure: 1005 bar - Humidity: 75%
    2023-11-10 19:00:00
    Temperatur:  8.2 - Pressure: 1005 bar - Humidity: 78%
    2023-11-10 22:00:00
    Temperatur:  6.9 - Pressure: 1003 bar - Humidity: 85%
    2023-11-11 01:00:00
    Temperatur:  7.3 - Pressure: 1004 bar - Humidity: 86%
    2023-11-11 04:00:00
    Temperatur:  6.1 - Pressure: 1007 bar - Humidity: 90%
    2023-11-11 07:00:00
    Temperatur:  6.2 - Pressure: 1010 bar - Humidity: 79%
    2023-11-11 10:00:00
    Temperatur:  6.4 - Pressure: 1011 bar - Humidity: 85%
    2023-11-11 13:00:00
    Temperatur:  6.3 - Pressure: 1011 bar - Humidity: 90%
    2023-11-11 16:00:00
    Temperatur:  7.2 - Pressure: 1012 bar - Humidity: 83%
    2023-11-11 19:00:00
    Temperatur:  7.0 - Pressure: 1012 bar - Humidity: 86%
    2023-11-11 22:00:00
    Temperatur:  6.4 - Pressure: 1012 bar - Humidity: 88%
    2023-11-12 01:00:00
    Temperatur:  5.7 - Pressure: 1010 bar - Humidity: 89%
    2023-11-12 04:00:00
    Temperatur:  4.5 - Pressure: 1008 bar - Humidity: 89%
    2023-11-12 07:00:00
    Temperatur:  4.1 - Pressure: 1007 bar - Humidity: 87%
    2023-11-12 10:00:00
    Temperatur:  6.5 - Pressure: 1006 bar - Humidity: 76%
    2023-11-12 13:00:00
    Temperatur:  8.4 - Pressure: 1005 bar - Humidity: 67%
    2023-11-12 16:00:00
    Temperatur:  5.8 - Pressure: 1005 bar - Humidity: 93%
    2023-11-12 19:00:00
    Temperatur:  5.0 - Pressure: 1004 bar - Humidity: 94%
    2023-11-12 22:00:00
    Temperatur:  5.5 - Pressure: 1002 bar - Humidity: 94%
    2023-11-13 01:00:00
    Temperatur:  6.1 - Pressure: 1003 bar - Humidity: 96%
    2023-11-13 04:00:00
    Temperatur:  5.8 - Pressure: 1007 bar - Humidity: 96%
    2023-11-13 07:00:00
    Temperatur:  5.7 - Pressure: 1009 bar - Humidity: 96%
    2023-11-13 10:00:00
    Temperatur:  6.0 - Pressure: 1013 bar - Humidity: 94%

# Weitere Übungen mit der Fruit Shop API

Unter https://www.predic8.de/rest-api-public-sample.htm stellt predic8
zu Schulungszwecken eine frei zugängliche Rest API zur Verfügung.

Folgendes Beispiel ließt alle Produkte des Fruit-Shop’s aus:

``` python
import requests

response = requests.get('https://fruitshop2-predic8.azurewebsites.net/shop/v2/products/')
res_data = response.json()
print(res_data)
```

    {'meta': {'count': 17, 'start': 1, 'limit': 10, 'next_link': '/shop/v2/products?start=11&limit=10'}, 'products': [{'id': 17, 'name': 'Pineapple-Slice', 'self_link': '/shop/v2/products/17'}, {'id': 16, 'name': 'Pineapple', 'self_link': '/shop/v2/products/16'}, {'id': 15, 'name': 'Physalis', 'self_link': '/shop/v2/products/15'}, {'id': 14, 'name': 'Persimmon', 'self_link': '/shop/v2/products/14'}, {'id': 13, 'name': 'Papaya', 'self_link': '/shop/v2/products/13'}, {'id': 12, 'name': 'Rambutan', 'self_link': '/shop/v2/products/12'}, {'id': 11, 'name': 'Orange', 'self_link': '/shop/v2/products/11'}, {'id': 10, 'name': 'Lychee', 'self_link': '/shop/v2/products/10'}, {'id': 9, 'name': 'Horn-Cucumber', 'self_link': '/shop/v2/products/9'}, {'id': 8, 'name': 'Grapes', 'self_link': '/shop/v2/products/8'}]}

**1. Ausgabe der Kategorien**

Geben Sie alle Produktnamen untereinander aus:

``` python
# insert code here
for r in res_data["products"]:
    print(r["name"])
```

    Pineapple-Slice
    Pineapple
    Physalis
    Persimmon
    Papaya
    Rambutan
    Orange
    Lychee
    Horn-Cucumber
    Grapes

**2. Ein bestimmtes Produkt auslesen**

Lesen Sie nun das Produkt mit der ID 8 aus. Geben Sie den Namen sowie
die zugehörigen Verkäufer aus. Welchen Preis hat das Produkt?

``` python
# insert code here
response = requests.get('https://fruitshop2-predic8.azurewebsites.net/shop/v2/products/8')
res_data = response.json()
print(res_data['name'])
print("Verkäufer:")
for v in res_data["vendors"]:
    print(v["name"])
    
print("Preis:", res_data['price'])
```

    Grapes
    Verkäufer:
    Max Obsthof GmbH
    Preis: 4.5

**4. Verkäufer hinzufügen und ändern**

Die Fruit-Shop-API ermöglicht auch neue Datensätze zu ergänzen, zu
ändern oder zu löschen.

Einen Verkäufer können Sie mit der HTTP-Post-Methode hinzufügen.

Mit folgendem Code lässt sich beispielsweise eine HTTP-Post-Anfrage zu
realisieren: <code> r = requests.post(‘https://httpbin.org/post’,
json={‘key’: ‘value’}) </code>

Analysieren Sie mit Hilfe von Swagger unter
https://api.predic8.de/shop/v2/swagger-ui/index.html#/Vendors/createVendor,
wie Sie einen Verkäufer anlegen und implementieren Sie den Python-Code
hierfür.

``` python
# Verkäufer anlegen
# insert code here
response = requests.post(f'https://fruitshop2-predic8.azurewebsites.net/shop/v2/vendors', json={"name": "GSOG Obsthof GmbH"})
res_data = response.json()
print("Ergebnis der Post-Anfrage")
print(res_data)
```

    Ergebnis der Post-Anfrage
    {'id': 5, 'name': 'GSOG Obsthof GmbH', 'self_link': '/shop/v2/vendors/5'}

Um einen Datensatz zu ändern bietet die API Anfragen auf Basis der
HTTP-Put-Methode. HTTP-Put ermöglicht es (ähnlich wie HTTP-Post),
größere Datenmengen zwischen Client und Server zu übertragen (siehe auch
https://wiki.selfhtml.org/wiki/HTTP/Anfragemethoden).

Mit folgendem Code lässt sich beispielsweise eine HTTP-Put-Anfrage zu
realisieren: <code> r = requests.put(‘https://httpbin.org/post’,
json={‘key’: ‘value’}) </code>

Daten, die per Patch an den Webserver httpbin.org übertragen werden
sollen, müssen im Parameter data spezifiziert werden.

Eine Dokumentation aller HTTP-Methoden, die Requests bietet finden Sie
hier: https://www.w3schools.com/python/module_requests.asp

Ändern Sie nun den Namen des vorher angelegten Verkäufers.

``` python
# insert code here
vendor_id = 5

# Verkäufer vor der Änderung laden.
response = requests.get(f'https://fruitshop2-predic8.azurewebsites.net/shop/v2/vendors/{vendor_id}')
res_data = response.json()
print(res_data)
print("Name vor der Änderung")
print(res_data["name"])

# Verkäufer ändern
response = requests.put(f'https://fruitshop2-predic8.azurewebsites.net/shop/v2/vendors/{vendor_id}', json={"name": "Offenburger Obsthof GmbH"})
res_data = response.json()
print("Ergebnis der Put-Anfrage")
print(res_data)

# Verkäufer nach der Änderung laden.
response = requests.get(f'https://fruitshop2-predic8.azurewebsites.net/shop/v2/vendors/{vendor_id}')
res_data = response.json()
print(res_data)
print("Name nach der Änderung")
print(res_data["name"])
```

    {'id': 5, 'name': 'GSOG Obsthof GmbH', 'products_link': '/shop/v2/vendors/5/products'}
    Name vor der Änderung
    GSOG Obsthof GmbH
    Ergebnis der Put-Anfrage
    {'id': 5, 'name': 'Offenburger Obsthof GmbH', 'self_link': '/shop/v2/vendors/5'}
    {'id': 5, 'name': 'Offenburger Obsthof GmbH', 'products_link': '/shop/v2/vendors/5/products'}
    Name nach der Änderung
    Offenburger Obsthof GmbH

**5. Löschen eines Produkts**

Die API lässt das Löschen eines Verkäufers nicht zu, warum?

Produkte können aber gelöscht werden. Legen Sie nun ein Produkt an und
löschen Sie es anschließend wieder.

Wenn der delete Erfolgreich war, liefert die API den status_code 200.
Werten Sie diesen aus.

``` python
# insert code here

#Produkt anlegen
response = requests.post(f'https://fruitshop2-predic8.azurewebsites.net/shop/v2/products', json={"name": "Mangos", "price":3.14})
res_data = response.json()
print("Ergebnis der Post-Anfrage")
print(res_data)

# Produkt wieder löschen
response = requests.delete(f'https://fruitshop2-predic8.azurewebsites.net/shop/v2/products/{res_data["id"]}')
print("Ergebnis des deletes")
if response.status_code == 200:
    print("Produkt wurde gelöscht")
else:
    print("Löschen war leider nicht erfogreich")
```

    Ergebnis der Post-Anfrage
    {'id': 23, 'name': 'Mangos', 'price': 3.14, 'self_link': '/shop/v2/products/23'}
    Ergebnis des deletes
    Produkt wurde gelöscht

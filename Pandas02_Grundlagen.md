## Pandas

### Datentypen

```python
import pandas as pd

df = pd.read_csv("../data/Temperature/GlobalLandTemperaturesByMajorCity.csv.bz2")
df.head()

#dt 	AverageTemperature 	AverageTemperatureUncertainty   City 	Country Latitude 	Longitude
#0 	1849-01-01 	26.704 	1.435 	Abidjan 	Côte D'Ivoire   5.63N 	3.23W
#1 	1849-02-01 	27.434 	1.362 	Abidjan 	Côte D'Ivoire 	5.63N 	3.23W
#2 	1849-03-01 	28.101 	1.612 	Abidjan 	Côte D'Ivoire 	5.63N 	3.23W
#3 	1849-04-01 	26.140 	1.387 	Abidjan 	Côte D'Ivoire 	5.63N 	3.23W
#4 	1849-05-01 	25.427 	1.200 	Abidjan 	Côte D'Ivoire 	5.63N 	3.23W
```

Die **AverageTemperature** ergibt einen float64-Datentyp
```python
df["AverageTemperature"]

# ...
# 239176       NaN
# Name: AverageTemperature, Length: 239177, dtype: float64
```

**City** ergibt einen object-Datentyp
```python
df["City"]

# ...
# 239176       Xian
# Name: City, Length: 239177, dtype: object
```

Nan:
```python
x = float("nan")

print(x)
print(x + 5)
# mit nan kann man nicht so einfach vergleichen - man braucht eigene Funktionen
print(x == x)

# nan
# nan
# False
```

Auf nan-Wert prüfen
```python
import math

print(math.isnan(x))

# True
```

Löschen von NaN-Werten
```python
len(df)
# 239177

df = df[~pd.isna(df["AverageTemperature"])]
len(df)
# 228175
```

Um alle NaN-Werte zu entfernen
```python
df.dropna()
```

### Strings verarbeiten

Pandas-Series unterstützen den + Operator
```python
# City und Country zusammenführen
df["City"] + ", " + df["Country"]
mit zurückschreiben
df["City"] = df["City"] + ", " + df["Country"]
```

Eine Spalte löschen
```python
df = df.drop(["Country"], axis=1)
# df.drop(["Country"], axis=1, inplace=True)
```

Aufteilen eines Spalteninhalts in mehrere Spalten (str-Funktion auf eine Series)
```python
#df["City"].str.replace(",", ",,,")
df["City"].str.split(",", 1)  # es entsteht eine Series mit Listenelementen - müsste mit der map-Funktion weiter bearbeitet werden --> eleganter die expand-Option

#0         [Abidjan,  Côte D'Ivoire]
#1         [Abidjan,  Côte D'Ivoire]
#2         [Abidjan,  Côte D'Ivoire]
```
```python
df["City"].str.split(",", 1, expand=True)

#       	0 	            1
#0 	Abidjan 	Côte D'Ivoire
#1 	Abidjan 	Côte D'Ivoire
#2 	Abidjan 	Côte D'Ivoire
```

```python
df_city = df["City"].str.split(",", 1, expand=True)

# auf numerische Spaltennamen zugreifen
df["City"] = df_city[0]
df["Country"] = df_city[1]
```

### Datentypen umwandeln

z.B. den Längengrad (z.B. 3.23W) in eine Kommazahl umwandeln

```python
df["Longitude"].astype("float")
# ValueError --> da im String noch der Buchstabe (W,...) steht
```
```python
"3.23W"[:-1]
# '3.23'
df["LongitudeDir"] = df["Longitude"].str[-1]
```

```python
df["Longitude"] = df["Longitude"].str[:-1].astype("float")
```

```python
df.loc[df["LongitudeDir"] == "W", "Longitude"] = df["Longitude"] * -1
# eventuell die LongitudeDir-Spalte wieder entfernen
df.drop(["LongitudeDir"], axis=1, inplace=True)
```

Lösung ohne eigene Spalte (über eine eigene Variable)
```python
longitudeDir = df["Longitude"].str[-1]
df["Longitude"] = df["Longitude"].str[:-1].astype("float")
df.loc[longitudeDir == "W", "Longitude"] = df["Longitude"] * -1
```

### Zeitreihen abfragen

z.B. Frage: War es im Jahr 2012 im Schnitt wärmer als im Jahr 2010?, und um wieviel war es dann wärmer

```python
df["dt"]
# liefert die Datensätze als string (object)

pd.to_datetime("2019-05-05")
# Timestamp('2019-05-05 00:00:00')
pd.to_datetime("05.06.2021", format="%d.%m.%Y")
```

```python
df["dt"] = pd.to_datetime(df["dt"])
```

Es gibt noch die **dt-Funktion**
```python
df["dt"].dt.year
df["dt"].dt.month
```

```python
df.loc[df["dt"].dt.year == 2012, "AverageTemperatur"]
df.loc[df["dt"].dt.year == 2012, "AverageTemperatur"].mean()
# 19.66823916666667
```

```python
print(df.loc[df["dt"].dt.year == 2010, "AverageTemperatur"].mean())
print(df.loc[df["dt"].dt.year == 2012, "AverageTemperatur"].mean())
```

### Daten sortieren

z.B. nach der durchschnittlichen Temperatur aufsteigend sortieren
```python
df.sort_values(by=["AverageTemperature"])
df.sort_values?
# inplace, ascending, ...
# auch nach mehreren Spalten sortieren
```

### Daten gruppieren

z.B. Durchschnittswerte pro Jahr für alle Jahre

#### über eine pandas-Methode
```python
import numpy as np
import pandas as pd

df = pd.read_csv("../data/Temperature/GlobalLandTemperaturesByMajorCity.csv.bz2")
df["dt"] = pd.to_datetime(df["dt"])
df["dtYear"] = df["dt"].dt.year

r = df.groupby("dtYear")[["AverageTemperature","AverageTemperatureUncertainty"]].mean()
r.loc[1980:2014]
# r.loc[1980:2014, "AverageTemperature"]
```

#### über eine übergebene numpy-Funktion
```python
import numpy as np
# df.groupby(by=["dt"])  # dem Befehl fehlt noch was
df.groupby(by=["dt"]).agg(avgTmp=("AverageTemperature", np.mean))  # jetzt für jeden Tag gruppiert
```

```python
df["dtYear"] = df["dt"].dt.year
df.groupby(by=["dtYear"]).agg(avgTmp=("AverageTemperature", np.mean))
```

```python
df["dtYear"] = df["dt"].dt.year
res = df.groupby(by=["dtYear"]).agg(avgTmp=("AverageTemperature", np.mean))

res.loc[1980:2014, "avgTmp"]
```

## Aufgaben

### Aufgabe1

In Äquatornähe ist es tendenziell wärmer als weiter nördlich bzw. weiter südlich.

- Was ist die durchschnittliche "AverageTemperature" für alle Messwerte zwischen einem Breitengrad ("Latitude") von -10 und 10 Grad?
- Und was ist die durchschnittliche "AverageTemperature" für alle Messwerte außerhalb dieses Bereiches?

Hinweis: Beantworte beide Fragen mit jeweils nur einer (wenn auch komplexen) Zeile Python-Code. Ggf wirst du hierfür die .loc-Schreibweise benötigen.

### Aufgabe2

In welchem Land wurde im Schnitt die höchste "AverageTemperature" gemessen?

### Aufgabe3

Filtere die Daten (in einer neuen Variable), sodass nur noch die Jahre 1990-2012 (bis zum 31.12.2012) betrachtet werden.

Erstelle anschließend eine Auflistung, bei der für jedes Jahr der Durchschnittswert der Spalte "AverageTemperature" berechnet wird! Welches dieser Jahre war das wärmste Jahr?

**Hinweis**: Du kannst Datumswerte einfach miteinander vergleichen. Dies funktioniert auch, wenn auf der rechten bzw. auf der linken Seite eine Series steht, hier in diesem Beispiel wird also dann True ausgegeben:
```python
print(pd.to_datetime("1990-01-01") < pd.to_datetime("1995-01-01"))
```

## Merkblätter

- [Merkblatt_NaN](pdfs/Merkblatt_NaN.pdf)
- [Merkblatt_Sortieren_und_Gruppieren](pdfs/Merkblatt_Sortieren_und_Gruppieren.pdf)
- [Merkblatt_Strings_in_Dataframes](pdfs/Merkblatt_Strings_in_Dataframes.pdf)
- [Merkblatt_Timestamp_in_Dataframes](pdfs/Merkblatt_Timestamp_in_Dataframes.pdf)





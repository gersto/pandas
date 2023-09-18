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
df = df.drop(["Conutry"], axis=1)
# df.drop(["Conutry"], axis=1, inplace=True)
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


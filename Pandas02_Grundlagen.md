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

print(x + 5)
print(x == x)

# nan
# False
```

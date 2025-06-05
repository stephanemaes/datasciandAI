
# Cheat Sheet DSAI

## Basics
```python
import numpy as np                                  # "Scientific computing"
import scipy.stats as stats                         # Statistical tests

import pandas as pd                                 # Data Frame
from pandas.api.types import CategoricalDtype

import matplotlib.pyplot as plt                     # Basic visualisation
from statsmodels.graphics.mosaicplot import mosaic  # Mosaic diagram
import seaborn as sns                               # Advanced data visualisation
```

```python
df = pd.read_csv('data.csv')                        # Load data
df.head()                                           # Show first 5 rows
df.describe()                                       # Show summary statistics
df.info()                                           # Show data types
df.query('column == value')                         # Filter data
df.count()                                          # Count non-NA cells
df = df.fillna(value={'column': value})             # Fill NA values
df['column'] = df['column'].astype('category')      # Change data type
df['column'] = pd.to_datetime(df['column'])         # Change column type to datetime

data.mean()                                         # mean
np.var(array)                                       # populatie variance
np.var(array, ddof=1)                               # sample variance
array.std() of np.std(array)                        # populatie standard deviation
np.std(array, ddof=1)                               # sample standard deviation   
stats.iqr(array)                                    # interkwartielafstand
stats.kurtosis(array)                               # kurtosis
np.ptp(array)                                       # range
np.cov(x, y, ddof=1)[0][1]                          # covariance
np.cor(x, y)[0][1]                                  #correlation coefficient
```

| **Quantitative** | **Betekenis** |
| :--- | :--- |
| Nominal | Categories: gender, land, vorm |
| Ordinal | Order/Rank: educatieniveau, militaire rang |

| **Qualitative** | **Betekenis** |
| :--- | :--- |
| Interval | Geen vast nulpunt: temperatuur, datum |
| Ratio | Vast nulpunt: lengte, gewicht, leeftijd |



## Tests & Values
### Algemeen

| **Onafhankelijke** | **Afhankelijke** | **Test** |
| :--- | :--- | :---|
| Kwalitatief | Kwalitatief | Chi-kwadraat & Cramers V (H4) |
| Kwalitatief | Kwantitatief | t-test & cohens d (H5) |
| Kwantitatief | Kwantitatief | Lineaire regressie & correlatie (H6) | 

### Chapter 3
### T-test
De t-test of t-verdeling is een variant op de normale verdeling, maar deze wordt gebruikt voor kleinere steekproeven, waarbij de variantie onbekend is.
| **Function**    | **Purpose** |
| :---                     | :--- |
| `stats.t.pdf(x, df=d)`   | Probability density for $x$    |
| `stats.t.cdf(x, df=d)`   | Left-tail probability 𝑃(𝑋 < x) |
| `stats.t.sf(x, df=d)`    | Right-tail probability 𝑃(𝑋 > x)    |
| `stats.t.isf(1-p, df=d)` | p% of observations are expected to be lower than this value    | 

### Z-test
Een Z-score geeft aan hoeveel standaarddeviaties een observatie van het gemiddelde af zit. Je krijgt dus je plek ten opzichte van het gemiddelde, uitgedrukt in een standaard maat. 
| **Function**    | **Purpose** |
| :---                     | :--- |
| `stats.norm.pdf(x, loc=m, scale=s)`   | Probability density for $x$    |
| `stats.norm.cdf(x, loc=m, scale=s)`   | Left-tail probability 𝑃(𝑋 < x) |
| `stats.norm.sf(x, loc=m, scale=s)`    | Right-tail probability 𝑃(𝑋 > x)    |
| `stats.norm.isf(1-p, loc=m, scale=s)` | p% of observations are expected to be lower than this value    |

### P-value
De p-waarde is de kans dat de nulhypothese waar is. Hoe lager de p-waarde, hoe onwaarschijnlijker de nulhypothese. Wanneer de p-waarde kleiner is dan het gekozen significantieniveau kun je stellen dat dat de gevonden uitkomst extreem genoeg is om je nulhypothese te verwerpen.
| **Function**    | 
| :---                     |
| `stats.norm.cdf(sample_m, loc=m, scale=sample_s)`  |
| `stats.norm.sf(sample_m, loc=m, scale=sample_s)`   |

### G-value / Critical value
De G-waarde is een maat voor de mate waarin de nulhypothese wordt verworpen. Hoe groter de G-waarde, hoe sterker de nulhypothese wordt verworpen. 
| **Function**    | **Purpose** |
| :---                     | :--- |
| `stats.norm.isf(1-a, loc=m, scale=s)` | linkergrens (1-a)    |
| `stats.norm.isf(a, loc=m, scale=s)`  | rechtergrens a    |
| `stats.norm.isf(1-a/2, loc=m, scale=s)` | tweezijdig     |
| `stats.norm.isf(a/2, loc=m, scale=s)`  | tweezijdig     |

### Chapter 4
### Chi-square test
#### Chi-square test for independence
De chi-kwadraattoets voor onafhankelijkheid wordt gebruikt om te bepalen of er een significant verband is tussen twee categorische variabelen.

#### Chi-square test for goodness of fit
De chi-kwadraattoets voor goedheid van fit wordt gebruikt om te bepalen of er een significant verschil is tussen de verwachte frequenties en de geobserveerde frequenties in één enkele categorische variabele.

### Cramér's V
Cramér's V is een statistische maat die wordt gebruikt om de sterkte van de associatie tussen twee categorische variabelen te meten na het uitvoeren van een chi-kwadraattoets voor onafhankelijkheid.

### Chapter 5
### T-Test independent samples
De t-toets voor onafhankelijke steekproeven wordt gebruikt om te bepalen of er een significant verschil is tussen de gemiddelden van twee onafhankelijke groepen.

### T-Test paired samples
De t-toets voor gepaarde steekproeven wordt gebruikt om te bepalen of er een significant verschil is tussen de gemiddelden van twee gerelateerde groepen.

### Cohen's d
Cohen's d is een statistische maat die wordt gebruikt om de effectgrootte van een verschil tussen twee groepen te meten.

## Plots
### Algemeen
| **Onafhankelijke** | **Afhankelijke** | **Graf** |
| :--- | :--- | :---|
| Kwalitatief | Kwalitatief | Clustered staaf, mozaïek |
| Kwalitatief | Kwantitatief | Boxplot, staaf met errorbars |
| Kwantitatief | Kwantitatief | Spreidingsdiagram, regressierechte | 


| **Graf**    | **Code** |
| :---                     | :--- |
| Gewone graf | `df.plot(x= , y= )`    |
| Barchart | `sns.catplot(data= , kind=x, y=)` |
| Barchart + error | `sns.barplot(data=df, x=, y=, errorbar='sd')` |
| Clustered barchart | `sns.catplot(data=df, x=, hue=, kind=y)` hue komt uit crosstab |
| Boxplot | `sns.boxplot(data= , x=)`|
| Histogram | `sns.displot(x=df['column])` |
| Kernel density | `sns.kdeplot(x=df['column])` |
| His + Kernel | `sns.displot(x=df['column], kde=True)` |
| Violinplot | `sns.violinplot(data=df, x=)` |
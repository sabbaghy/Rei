---
title: "The Wealth of Nations: A Data Visualized Look at Life Expectancy and Daily Wages"
date: 2019-04-19
categories: [data-science]
tags: [data-visualization, data-exploration, python]
header:
    image: "/images/lifeexpect/LifeExpect.jpg"
excerpt: "Is the world getting better or worse? This is the question that Steven Pinker, a professor and writer, addressed in a TED talk given in April 2018. Pinker's conclusion? A resounding yes, the world is indeed getting better. Given this question, I began my own investigation. Suffice to say, I am skeptical...often, especially of overtly optimistic claims." 
---

# A Data Visualized Look at Life Expectancy and Daily Wages

Is the world getting better or worse? This is the question that Steven Pinker, a professor and writer, addressed in a TED talk given in April 2018. Pinker's conclusion? A resounding yes, the world is indeed getting better. Given this question, I began my own investigation. Suffice to say, I am skeptical...often, especially of overtly optimistic claims. 

## Methodology 

To manage the scope of this question, I focused on two variables: life expectancy by country and gross domestic product by day by country. I picked these two variables to measure because they offer a generalized view of health and prosperity in each country. To affirm the null hypothesis, the world is getting better, I need only to look at the data from 1965 to 2015 decade by decade and analyze the progression or regression of the data. If the scatter-plot moves to the right and goes upward, progress, if it moves to the left and downward, regression. Fool-proof...or so I thought.

## Considerations

There are a few problems with the methodology that I chose. Utilizing gross domestic product by day is an unreliable indicator of prosperity and progress over time. A country could produce more goods and services as a population increases,since there are more people, more economic activity occurs. This does not inherently mean that the population is more wealthy or prosperous as a result from this increase in economic activity. When in doubt, remember, correlation does not equal causation. 

Another problem is the difference between nominal GDP and GDP per capita at purchasing power parity (PPP). Nominal GDP is fine, only if I'm not using it as a measure to investigate the relative prosperity of a countries inhabitants over a period of time. I am doing exactly that. In my case, GDP at PPP is a better measure to use since it factors in cost of living and inflation. The problem is, the data set used does not specify whether or not it is nominal GDP or GDP at PPP. When in doubt, avoid data sets without data dictionary. 

Life expectancy on the otherhand, is a workable indicator of health. There are problems with using this variable as the lone indicator of progress or regression in health, like if a country undergoes a war or if the inhabitants have longer than average life expectancies, then the results could be skewed. 

With the problems and pitfalls of my methodology addressed, let's move onto the code. 

## Getting Started

This code is written in Python and ran in Jupyter Notebooks. To follow along, I will post the data set and Notebook session on my github: [Alex FM on GitHub)(https://github.com/atalexfm)

## Code

```python
import numpy as np
import scipy.stats
import pandas as pd
```


```python
import matplotlib
import matplotlib.pyplot as pp

from IPython import display 

%matplotlib inline
```


```python
import csv
```


```python
minder = pd.read_csv("gapminder.csv")
```


```python
minder.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 14740 entries, 0 to 14739
    Data columns (total 9 columns):
    country             14740 non-null object
    year                14740 non-null int64
    region              14740 non-null object
    population          14740 non-null float64
    life_expectancy     14740 non-null float64
    age5_surviving      14740 non-null float64
    babies_per_woman    14740 non-null float64
    gdp_per_capita      14740 non-null float64
    gdp_per_day         14740 non-null float64
    dtypes: float64(6), int64(1), object(2)
    memory usage: 1.0+ MB



```python
minder.loc[0:260:20]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>year</th>
      <th>region</th>
      <th>population</th>
      <th>life_expectancy</th>
      <th>age5_surviving</th>
      <th>babies_per_woman</th>
      <th>gdp_per_capita</th>
      <th>gdp_per_day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>1800</td>
      <td>Asia</td>
      <td>3280000.0</td>
      <td>28.21</td>
      <td>53.142</td>
      <td>7.00</td>
      <td>603.0</td>
      <td>1.650924</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Afghanistan</td>
      <td>1955</td>
      <td>Asia</td>
      <td>8270024.0</td>
      <td>29.27</td>
      <td>60.193</td>
      <td>7.67</td>
      <td>1125.0</td>
      <td>3.080082</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Afghanistan</td>
      <td>1975</td>
      <td>Asia</td>
      <td>12582954.0</td>
      <td>39.61</td>
      <td>72.060</td>
      <td>7.67</td>
      <td>1201.0</td>
      <td>3.288159</td>
    </tr>
    <tr>
      <th>60</th>
      <td>Afghanistan</td>
      <td>1995</td>
      <td>Asia</td>
      <td>16772522.0</td>
      <td>49.40</td>
      <td>84.770</td>
      <td>7.83</td>
      <td>872.0</td>
      <td>2.387406</td>
    </tr>
    <tr>
      <th>80</th>
      <td>Afghanistan</td>
      <td>2015</td>
      <td>Asia</td>
      <td>32526562.0</td>
      <td>53.80</td>
      <td>90.890</td>
      <td>4.47</td>
      <td>1925.0</td>
      <td>5.270363</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Albania</td>
      <td>1954</td>
      <td>Europe</td>
      <td>1382881.0</td>
      <td>56.59</td>
      <td>84.829</td>
      <td>6.31</td>
      <td>2108.0</td>
      <td>5.771389</td>
    </tr>
    <tr>
      <th>120</th>
      <td>Albania</td>
      <td>1974</td>
      <td>Europe</td>
      <td>2358467.0</td>
      <td>69.35</td>
      <td>90.082</td>
      <td>4.54</td>
      <td>4177.0</td>
      <td>11.436003</td>
    </tr>
    <tr>
      <th>140</th>
      <td>Albania</td>
      <td>1994</td>
      <td>Europe</td>
      <td>3140634.0</td>
      <td>73.60</td>
      <td>96.540</td>
      <td>2.77</td>
      <td>3457.0</td>
      <td>9.464750</td>
    </tr>
    <tr>
      <th>160</th>
      <td>Albania</td>
      <td>2014</td>
      <td>Europe</td>
      <td>2889676.0</td>
      <td>77.90</td>
      <td>98.560</td>
      <td>1.78</td>
      <td>10160.0</td>
      <td>27.816564</td>
    </tr>
    <tr>
      <th>180</th>
      <td>Algeria</td>
      <td>1953</td>
      <td>Africa</td>
      <td>9405445.0</td>
      <td>43.96</td>
      <td>73.758</td>
      <td>7.65</td>
      <td>4077.0</td>
      <td>11.162218</td>
    </tr>
    <tr>
      <th>200</th>
      <td>Algeria</td>
      <td>1973</td>
      <td>Africa</td>
      <td>15804428.0</td>
      <td>53.91</td>
      <td>77.660</td>
      <td>7.55</td>
      <td>7581.0</td>
      <td>20.755647</td>
    </tr>
    <tr>
      <th>220</th>
      <td>Algeria</td>
      <td>1993</td>
      <td>Africa</td>
      <td>27785977.0</td>
      <td>71.20</td>
      <td>95.580</td>
      <td>3.97</td>
      <td>9279.0</td>
      <td>25.404517</td>
    </tr>
    <tr>
      <th>240</th>
      <td>Algeria</td>
      <td>2013</td>
      <td>Africa</td>
      <td>38186135.0</td>
      <td>76.30</td>
      <td>97.480</td>
      <td>2.80</td>
      <td>12893.0</td>
      <td>35.299110</td>
    </tr>
    <tr>
      <th>260</th>
      <td>Angola</td>
      <td>1952</td>
      <td>Africa</td>
      <td>4529381.0</td>
      <td>31.59</td>
      <td>60.428</td>
      <td>6.98</td>
      <td>3281.0</td>
      <td>8.982888</td>
    </tr>
  </tbody>
</table>
</div>




```python
def plotyear(year):
    data = minder[minder.year == year]
    area = 5e-6 * data.population
    colors = data.region.map({'Africa': 'red', 'Europe': 'skyblue', 'America':'green', 'Asia':'orange'})
    
    data.plot.scatter('life_expectancy', 'gdp_per_day', s = area, c = colors,
                      linewidth =1, edgecolors = 'k', figsize = (12,9))
    
    pp.axis(ymin = -20, ymax = 300, xmin = 20, xmax = 90)
    pp.xlabel('Life Expectancy')
    pp.ylabel('GDP Per Day')
```


```python
plotyear(1965) 
```

![png](/images/lifeexpect/output_7_0.jpg)



```python
plotyear(1975)
```

![png](/images/lifeexpect/output_8_0.jpg)



```python
plotyear(1985)
```

![png](/images/lifeexpect/output_9_0.jpg)



```python
plotyear(1995)
```

![png](/images/lifeexpect/output_10_0.jpg)



```python
plotyear(2005)
```

![png](/images/lifeexpect/output_11_0.jpg)



```python
plotyear(2015)
```

![png](/images/lifeexpect/output_12_0.jpg)


## Sources:

1. Gapminder. [https://www.gapminder.org/data/](https://www.gapminder.org/data/)

2. TED. Steven Pinker: Is the World Getting Better or Worse? A Look at the Numbers. [https://www.ted.com/talks/steven_pinker_is_the_world_getting_better_or_worse_a_look_at_the_numbers?language=en#t-370688](https://www.ted.com/talks/steven_pinker_is_the_world_getting_better_or_worse_a_look_at_the_numbers?language=en#t-370688)

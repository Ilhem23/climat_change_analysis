# management_project

Link to notebook colab: https://drive.google.com/file/d/1dUf3bJBA_p0JMtyB_NvzfX0yHimhKYRE/view?usp=sharing

## **Climate Change**
#### **Global warming analysis & predictions**

---
Huge fires raged this summer on the island of Evia and elsewhere in Greece, Turkey, Morocco, Algeria, Spain, Italy, Siberia, Scandinavia and California, among others, have also been hit hard by forest fires. Because of the drought and rising temperatures, there are more and more mega-fires destroying entire regions and millions of hectares of forests.Many scientists assume that this fires is clearly related to climate change, and these conditions will result in more vegetation drying out, and therefore more intense and harder to control fires. After this giant fires that devastated various regions in the world, and destroyed thousands of hectares of forests, I decided to take a look to the global temperatures and how exaclty are they evolving and have been evolving during the years.

##### **Questions**
- Is there a global warming?
- When did Global Warming Started?
- What is the trend of temperature change in the world?
- What are the most countries that suffer from temperature increasing ?
-  Interactive Map of the countries - Temperature increase over the years

In this project i will analyse The Climate Change Open Data from Kaggle to study the Earth's temperature.

#### **Dataset** 
I used a open data set (Climate Change: Earth Surface Temperature Data) from Kaggle website, you can find the link below: 
- https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data?select=GlobalTemperatures.csv
- https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data?select=GlobalLandTemperaturesByCity.csv

I used also the data set of country and continents code (Country Mapping - ISO, Continent, Region)
https://www.kaggle.com/andradaolteanu/country-mapping-iso-continent-region?select=continents2.csv

<a id="import"></a> <br> 
#### **Import libraries**
Go to colab website https://colab.research.google.com/ , login with your Google account, and create new notebook File -> new Notebook, after that click + Code , and write the line of code below to import libraries.

# Import library
```
import pandas as pd # library to load data 
import numpy as np # library to run blazing fast computation
import seaborn as sns # library to make interactive graph
import matplotlib.pyplot as plt # library to visualize data
%matplotlib inline
```
# import library Plotly 
```
import plotly.offline as py
py.init_notebook_mode(connected=True)
import plotly.graph_objs as go
import plotly.tools as tls
import plotly.express as px
from plotly.subplots import make_subplots
import time
import warnings
warnings.filterwarnings('ignore')
```

#### **Load Dataset** 
- Download the dataset from Kaggle website with links listed above ( in Dataset section).
- Install Drive by clicking into install drive icon in right sidebar of your colab notebook: Files -> install drive icon (in top of sidebar).
- Upload your data under Colab notebooks folder in your drive.

# load data to dataframe
```
data = pd.read_csv('GlobalTemperatures.csv') # Store csv in DataFrame with Pandas
data2 = pd.read_csv('GlobalLandTemperaturesByCity.csv') # Store csv in DataFrame with Pandas
```
#### **Data processing** 
##### Let check the missing value
```
data.isna().sum() # there are 1200 missing values for Max, Min and Land&Ocean Average Temp
```
##### Assumed that , the missing values are not signeficant in our dataset
- Because data is missing in chucks
- We are dealing with time series data
- we will drop all rows that have at least one missing value
```
data.dropna(axis = 0, inplace = True)
```
##### Convert dt column elements to datetime object
```
data.dt = pd.to_datetime(data.dt, format='%Y-%m-%d')  # converted all dates to the same format 
```
##### Take a Yearly data as average to simplify the analysis process
```
data['year'] = data['dt'].dt.year # take a year date from dt date of data
 # take a average (mean() function)  of all columns groupe by year and reset the index of data
global_temperature = data.groupby(by = 'year')[['LandAverageTemperature', 'LandAverageTemperatureUncertainty',
       'LandMaxTemperature', 'LandMaxTemperatureUncertainty',
       'LandMinTemperature', 'LandMinTemperatureUncertainty',
       'LandAndOceanAverageTemperature',
       'LandAndOceanAverageTemperatureUncertainty']].mean().reset_index() 
global_temperature.head(5)
```
### Data analysis
### I. Is there a global warming?
We began with variable **Land Average Temperature**, this variable is going so far in time, it helps us to show the change of temperature in years. I extract the year from the date, after that I plot the the land average temperature and i fill the average uncertainly temperature to the top line and the bot line.
![alt text](https://github.com/Ilhem23/management_project/blob/main/images/1.png)
### II. When did Global Warming Started?
I make the graph with subplot to visualize the difference average mesure( land average temperature, land min temperature, land max average temperature and ocean average temperature) over the years.
![alt text](https://github.com/Ilhem23/management_project/blob/main/images/2.png)
### III.  What is the trend of temperature change in the world?
I wanted to investigate how many historical records had in this decade to learn if global warming more rapid last decade.
I selected 'World' records from 'Country Name' column. Then, I chose only monthly basis temperature change values and whole world records. 
Result shows that already eight of the ten years in the current decade (2010–2015) were among the ten hottest years on record in terms of  mean annual temperatures. Additionally, Radar chart clearly shows how temperature change increased day by day.
![alt text](https://github.com/Ilhem23/management_project/blob/main/images/3.png)

### IV. What are the most countries that suffer from temperature increasing ?
To realize this analysis, I make a join the continents dataset with average temperature by country, i groupe the data by country, year, latitude and longitude, after that i calculate the difference between the max and the mean to shopw the degree of the increase of temperature.
![alt text](https://github.com/Ilhem23/management_project/blob/main/images/4.png)

### IV.  Interactive Map of the countries - Temperature increase over the years
The standard metric of temperature change is the level associated with devastating impacts. We have 1.5° C the level associated with less devastating impacts than higher levels of global warming beyond 1.5°C increasingly severe and expensive impacts.
To gzt this value from our dataset, I calculate the difference of average temperature between the year and the next year group by countries.
I make a interactive map of countries to better visualize the change over the years. 
![alt text](https://github.com/Ilhem23/management_project/blob/main/images/5.png)

## Conclusion

In this the project, I examined how global surface temperature change between 1860 to 2015. According to my guiding question answers, when examining the top areas that have the highest temperature change in the last decade are mostly industrialized countries. Additionally, I found that temperature increased every ten decades, and the last decade can count as the hottest decade. Finally,  I tried to show how temperature is increasing worldwide as a proof of global warming.

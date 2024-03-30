
# Data Cleaning in Python

The purpose of the project is to clean a dataset in preparation for [Creating Visuals](https://www.genome.gov/) and EDA


## Data Set Used

 - [Anime Dataset 2023](https://www.kaggle.com/datasets/dbdmobile/myanimelist-dataset/data?select=anime-filtered.csv)

## Environment Used

- VM inside of VS Code running ```Python3```

- ```Jupyter Notebook``` inside of VS Code



## Libraries Used

- ```pandas```

## Some code snippets and pictures of the cleaning process 

- ### Table BEFORE cleaning
```python
pd.set_option('display.max_columns', None)
df = pd.read_csv('FILE PATH HERE')
df.head()
``` 
![Table_Before_Drop_Columns](Images/Table_Before_Drop_Columns.png)
- ### Table AFTER columns were
```python
df.drop(columns={'anime_id', 'English name', 'Japanese name', 'sypnopsis', 'Producers', 'Licensors', 'Studios', 'Source', 'Duration'}, inplace=True)
df.head()
``` 
![Table_After_Drop_Columns](Images/Table_After_Drop_Columns.png)
- ### Querying the "Premiered" column for "Unknown" values
```python
results = df.query('Premiered.str.contains("Unknown")')
results.head()
``` 
![Premiered_Cols_Unk](Images/Premiered_Cols_Unk.png)
- ### Table AFTER the "Premiered" column had been replaced by the "Season_Premiered" and	"Year_Premiered" column
```python
df.drop(columns={'Aired', 'Premiered'}, inplace=True)
df.insert(5, "Season_Premiered", aired_season)
df.insert(6, "Year_Premiered", aired_year)
df.head()
``` 
![Year_Season_Cols](Images/Year_Season_Cols.png)
- ### Table BEFORE the "Genres" column was trimmed
```python
df.head()
``` 
![Before_Genre_Trim](Images/Before_Genre_Trim.png)
- ### Table AFTER the "Genres" column was trimmed
```python
genre = df['Genres'].str.split(',').str[0]
df.drop(columns='Genres', inplace=True)
df.insert(2, "Genre", genre)
df.head()
``` 
![After_Genre_Trim](Images/After_Genre_Trim.png)
- ### Table BEFORE the "Rating" column was trimmed
```python
df.head()
``` 
![Before_Rating_Trim](Images/Before_Rating_Trim.png)
- ### Table AFTER the "Rating" column was trimmed
```python
rating = df['Rating'].str.split(' ').str[0]
df.drop(columns='Rating', inplace=True)
df.insert(7, "Rating", rating)
df.head()
``` 
![After_Rating_Trim](Images/After_Rating_Trim.png)
- ### Table AFTER cleaning
```python
df.head(20)
``` 
![Final_Table](Images/Final_Table.png)

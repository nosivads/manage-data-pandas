| A workshop inspired by | Sponsored by |
| [<img src='TheCarpentries.svg' alt='Caltech Library' width='150'/>](https://carpentries.org) | [<img src='caltechlibrary-logo.png' alt='Caltech Library' width='150'/>](https://www.library.caltech.edu/) |

#### December 2, 2022

## Introduction

This workshop provides a brief introduction to Pandas ...

## Setup

The workshop assumes use of a Jupyter Notebook to run code examples. JupyterLab, Jupyter Notebook, and Google Colab are all 
good options. JupyterLab and Jupyter Notebook can be downloaded as part of the [Anaconda data science suite](https://anaconda.com).
Google Colab in a cloud-based Jupyter Notebook implementation.

### Google Colaboratory

We will be using Google Colaboratory ("Colab") to run code in this workshop. Colab is a free Jupyter Notebook environment
that runs in the cloud and stores its notebooks on Google Drive. To use Colab you will need to sign in to a Google account. 
(Note: Caltech Google accounts do not provide access to Colab. You will need to use a personal account.)

An introduction to Google Colab is available here: [https://research.google.com/colaboratory/](https://research.google.com/colaboratory/)

Before the workshop please confirm that you have a Google Account with access to Colab.

## Contents

1. [abc](abc.md)
    + 1.1 abc
    + 1.2 abc

2. [abc](abc.md) (abc)
    + 2.1 abc
### Managing Data with Pandas
##### Stephen Davison sdavison@caltech.edu
December 2, 2022

#### INTRODUCTION

The Python package, pandas (“panel data”) is a general purpose data analysis package that provides data structures and operations for manipulating numerical tables and time series. Information and documentation are available here: https://pandas.pydata.org/.

This workshop uses the Carpentries Databases and SQL data set, available here: http://swcarpentry.github.io/sql-novice-survey/files/survey.db, an SQLite database. The workshop is designed to follow the Databases and SQL workshop, but can stand alone also.

#### CREATING A DATAFRAME FROM SCRATCH

First import the pandas package...


```python
import pandas
```

A Pandas DataFrame is a two-dimensional Python object, similar to a database table or a spreadsheet.
DataFrames can be created from a Python list:


```python
# mydata is a list of lists
mydata = [['Tom', 'Physics', 2025, 3.7], 
          ['Li', 'Mathematics', 2026, 3.8],
          ['Juan', 'Chemistry', 2024, 4.0], 
          ['Shyla', 'Geology', 2023, 3.9]]

mydf = pandas.DataFrame(mydata, columns=['Name', 'Major', 'Class', 'GPA'])
```


```python
mydata
```

``
[['Tom', 'Physics', 2025, 3.7],  
['Li', 'Mathematics', 2026, 3.8],
['Juan', 'Chemistry', 2024, 4.0],
['Shyla', 'Geology', 2023, 3.9]]
``

```python
mydf
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
      <th>Name</th>
      <th>Major</th>
      <th>Class</th>
      <th>GPA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>Physics</td>
      <td>2025</td>
      <td>3.7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Li</td>
      <td>Mathematics</td>
      <td>2026</td>
      <td>3.8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Juan</td>
      <td>Chemistry</td>
      <td>2024</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Shyla</td>
      <td>Geology</td>
      <td>2023</td>
      <td>3.9</td>
    </tr>
  </tbody>
</table>
</div>



DataFrames can also be created from a Python dictionary:


```python
# mydictdata is a dictionary
mydictdata = {
    'Name' : ['Tom', 'Li', 'Juan', 'Shyla'],
    'Major' : ['Physics', 'Mathematics', 'Chemistry', 'Geology'],
    'Class' : [2025, 2026, 2024, 2023],
    'GPA' : [3.7, 3.8, 4.0, 3.9]
    }

mydf2 = pandas.DataFrame(mydictdata)
# no need to define the columns because they are identified in the dictionary
```


```python
mydictdata
```




    {'Name': ['Tom', 'Li', 'Juan', 'Shyla'],
     'Major': ['Physics', 'Mathematics', 'Chemistry', 'Geology'],
     'Class': [2025, 2026, 2024, 2023],
     'GPA': [3.7, 3.8, 4.0, 3.9]}




```python
mydf2
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
      <th>Name</th>
      <th>Major</th>
      <th>Class</th>
      <th>GPA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>Physics</td>
      <td>2025</td>
      <td>3.7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Li</td>
      <td>Mathematics</td>
      <td>2026</td>
      <td>3.8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Juan</td>
      <td>Chemistry</td>
      <td>2024</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Shyla</td>
      <td>Geology</td>
      <td>2023</td>
      <td>3.9</td>
    </tr>
  </tbody>
</table>
</div>



A DataFrame can be exported to a CSV file:


```python
mydf.to_csv('data_out.csv')
# open the CSV file to check

mydf.to_csv('data_out2.csv', index=False)
# use index=False to omit the row index numbers
```

Let's complete the round trip by importing the CSV back in as a DataFrame:


```python
roundtripdf = pandas.read_csv('data_out2.csv')
```


```python
roundtripdf
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
      <th>Name</th>
      <th>Major</th>
      <th>Class</th>
      <th>GPA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>Physics</td>
      <td>2025</td>
      <td>3.7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Li</td>
      <td>Mathematics</td>
      <td>2026</td>
      <td>3.8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Juan</td>
      <td>Chemistry</td>
      <td>2024</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Shyla</td>
      <td>Geology</td>
      <td>2023</td>
      <td>3.9</td>
    </tr>
  </tbody>
</table>
</div>



#### CREATING DATAFRAMES FROM DATABASE TABLES

DataFrames can also be created from database talbes. We are going to use the SQLite3 data, `survey.db`, that we used in the Databases and SQL workshop. We need to import the [sqlalchemy](https://www.sqlalchemy.org/) package to connect to this SQLite3-specific database file.


```python
import sqlalchemy
```

The sqlalchemy function, `create_engine()`, makes a connection with the database file. We will choose to call the connection `engine`, but that is an arbitrary choice:


```python
engine = sqlalchemy.create_engine('sqlite:///survey.db')
```

The pandas function, `read_sql_query()`, uses the `engine` connection to query the database aand return a pandas DataFrame:


```python
survey = pandas.read_sql_query('SELECT * FROM Survey', engine)
```

Let's verify that `survey` is a DataFrame:


```python
print(type(survey))
```

    <class 'pandas.core.frame.DataFrame'>
    

And display the DataFrame:


```python
survey
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
      <th>taken</th>
      <th>person</th>
      <th>quant</th>
      <th>reading</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>619</td>
      <td>dyer</td>
      <td>rad</td>
      <td>9.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>619</td>
      <td>dyer</td>
      <td>sal</td>
      <td>0.13</td>
    </tr>
    <tr>
      <th>2</th>
      <td>622</td>
      <td>dyer</td>
      <td>rad</td>
      <td>7.80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>622</td>
      <td>dyer</td>
      <td>sal</td>
      <td>0.09</td>
    </tr>
    <tr>
      <th>4</th>
      <td>734</td>
      <td>pb</td>
      <td>rad</td>
      <td>8.41</td>
    </tr>
    <tr>
      <th>5</th>
      <td>734</td>
      <td>lake</td>
      <td>sal</td>
      <td>0.05</td>
    </tr>
    <tr>
      <th>6</th>
      <td>734</td>
      <td>pb</td>
      <td>temp</td>
      <td>-21.50</td>
    </tr>
    <tr>
      <th>7</th>
      <td>735</td>
      <td>pb</td>
      <td>rad</td>
      <td>7.22</td>
    </tr>
    <tr>
      <th>8</th>
      <td>735</td>
      <td>None</td>
      <td>sal</td>
      <td>0.06</td>
    </tr>
    <tr>
      <th>9</th>
      <td>735</td>
      <td>None</td>
      <td>temp</td>
      <td>-26.00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>751</td>
      <td>pb</td>
      <td>rad</td>
      <td>4.35</td>
    </tr>
    <tr>
      <th>11</th>
      <td>751</td>
      <td>pb</td>
      <td>temp</td>
      <td>-18.50</td>
    </tr>
    <tr>
      <th>12</th>
      <td>751</td>
      <td>lake</td>
      <td>sal</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>13</th>
      <td>752</td>
      <td>lake</td>
      <td>rad</td>
      <td>2.19</td>
    </tr>
    <tr>
      <th>14</th>
      <td>752</td>
      <td>lake</td>
      <td>sal</td>
      <td>0.09</td>
    </tr>
    <tr>
      <th>15</th>
      <td>752</td>
      <td>lake</td>
      <td>temp</td>
      <td>-16.00</td>
    </tr>
    <tr>
      <th>16</th>
      <td>752</td>
      <td>roe</td>
      <td>sal</td>
      <td>41.60</td>
    </tr>
    <tr>
      <th>17</th>
      <td>837</td>
      <td>lake</td>
      <td>rad</td>
      <td>1.46</td>
    </tr>
    <tr>
      <th>18</th>
      <td>837</td>
      <td>lake</td>
      <td>sal</td>
      <td>0.21</td>
    </tr>
    <tr>
      <th>19</th>
      <td>837</td>
      <td>roe</td>
      <td>sal</td>
      <td>22.50</td>
    </tr>
    <tr>
      <th>20</th>
      <td>844</td>
      <td>roe</td>
      <td>rad</td>
      <td>11.25</td>
    </tr>
  </tbody>
</table>
</div>



There are three other tables in the database: site, visited, and person. Let's create a DataFrame for each of them and display them:


```python
site = pandas.read_sql_query('SELECT * FROM Site', engine)
```


```python
site
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
      <th>name</th>
      <th>lat</th>
      <th>long</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
    </tr>
    <tr>
      <th>1</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
    </tr>
  </tbody>
</table>
</div>




```python
visited = pandas.read_sql_query('SELECT * FROM Visited', engine)
```


```python
visited
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
      <th>id</th>
      <th>site</th>
      <th>dated</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>619</td>
      <td>DR-1</td>
      <td>1927-02-08</td>
    </tr>
    <tr>
      <th>1</th>
      <td>622</td>
      <td>DR-1</td>
      <td>1927-02-10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>734</td>
      <td>DR-3</td>
      <td>1930-01-07</td>
    </tr>
    <tr>
      <th>3</th>
      <td>735</td>
      <td>DR-3</td>
      <td>1930-01-12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>751</td>
      <td>DR-3</td>
      <td>1930-02-26</td>
    </tr>
    <tr>
      <th>5</th>
      <td>752</td>
      <td>DR-3</td>
      <td>None</td>
    </tr>
    <tr>
      <th>6</th>
      <td>837</td>
      <td>MSK-4</td>
      <td>1932-01-14</td>
    </tr>
    <tr>
      <th>7</th>
      <td>844</td>
      <td>DR-1</td>
      <td>1932-03-22</td>
    </tr>
  </tbody>
</table>
</div>




```python
person = pandas.read_sql_query('SELECT * FROM Person', engine)
```


```python
person
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
      <th>id</th>
      <th>personal</th>
      <th>family</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dyer</td>
      <td>William</td>
      <td>Dyer</td>
    </tr>
    <tr>
      <th>1</th>
      <td>pb</td>
      <td>Frank</td>
      <td>Pabodie</td>
    </tr>
    <tr>
      <th>2</th>
      <td>lake</td>
      <td>Anderson</td>
      <td>Lake</td>
    </tr>
    <tr>
      <th>3</th>
      <td>roe</td>
      <td>Valentina</td>
      <td>Roerich</td>
    </tr>
    <tr>
      <th>4</th>
      <td>danforth</td>
      <td>Frank</td>
      <td>Danforth</td>
    </tr>
    <tr>
      <th>5</th>
      <td>barrett</td>
      <td>Mary</td>
      <td>Barrett</td>
    </tr>
  </tbody>
</table>
</div>




```python
survey
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
      <th>taken</th>
      <th>person</th>
      <th>quant</th>
      <th>reading</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>619</td>
      <td>dyer</td>
      <td>rad</td>
      <td>9.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>619</td>
      <td>dyer</td>
      <td>sal</td>
      <td>0.13</td>
    </tr>
    <tr>
      <th>2</th>
      <td>622</td>
      <td>dyer</td>
      <td>rad</td>
      <td>7.80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>622</td>
      <td>dyer</td>
      <td>sal</td>
      <td>0.09</td>
    </tr>
    <tr>
      <th>4</th>
      <td>734</td>
      <td>pb</td>
      <td>rad</td>
      <td>8.41</td>
    </tr>
    <tr>
      <th>5</th>
      <td>734</td>
      <td>lake</td>
      <td>sal</td>
      <td>0.05</td>
    </tr>
    <tr>
      <th>6</th>
      <td>734</td>
      <td>pb</td>
      <td>temp</td>
      <td>-21.50</td>
    </tr>
    <tr>
      <th>7</th>
      <td>735</td>
      <td>pb</td>
      <td>rad</td>
      <td>7.22</td>
    </tr>
    <tr>
      <th>8</th>
      <td>735</td>
      <td>None</td>
      <td>sal</td>
      <td>0.06</td>
    </tr>
    <tr>
      <th>9</th>
      <td>735</td>
      <td>None</td>
      <td>temp</td>
      <td>-26.00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>751</td>
      <td>pb</td>
      <td>rad</td>
      <td>4.35</td>
    </tr>
    <tr>
      <th>11</th>
      <td>751</td>
      <td>pb</td>
      <td>temp</td>
      <td>-18.50</td>
    </tr>
    <tr>
      <th>12</th>
      <td>751</td>
      <td>lake</td>
      <td>sal</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>13</th>
      <td>752</td>
      <td>lake</td>
      <td>rad</td>
      <td>2.19</td>
    </tr>
    <tr>
      <th>14</th>
      <td>752</td>
      <td>lake</td>
      <td>sal</td>
      <td>0.09</td>
    </tr>
    <tr>
      <th>15</th>
      <td>752</td>
      <td>lake</td>
      <td>temp</td>
      <td>-16.00</td>
    </tr>
    <tr>
      <th>16</th>
      <td>752</td>
      <td>roe</td>
      <td>sal</td>
      <td>41.60</td>
    </tr>
    <tr>
      <th>17</th>
      <td>837</td>
      <td>lake</td>
      <td>rad</td>
      <td>1.46</td>
    </tr>
    <tr>
      <th>18</th>
      <td>837</td>
      <td>lake</td>
      <td>sal</td>
      <td>0.21</td>
    </tr>
    <tr>
      <th>19</th>
      <td>837</td>
      <td>roe</td>
      <td>sal</td>
      <td>22.50</td>
    </tr>
    <tr>
      <th>20</th>
      <td>844</td>
      <td>roe</td>
      <td>rad</td>
      <td>11.25</td>
    </tr>
  </tbody>
</table>
</div>



The `dtypes` attribute contains the data types of the columns in a DataFrame:


```python
survey.dtypes
```




    taken        int64
    person      object
    quant       object
    reading    float64
    dtype: object



The four tables in the database are related as shown here:

- Person: identifies people taking measurements
- Site: where the measurements were made
- Visited: date measurements were made, and reference to site
- Survey: the actual data


![TABLES](tables.jpg)

We can use `read_sql_query` to join the four tables and select the appropriate columns using the following SQL command:

`
SELECT Person.personal, Person.family, Site.name, Site.lat, Site.long, 
        Visited.dated, Survey.reading, Survey.quant
    FROM Survey
        JOIN Person ON Survey.person = Person.id
        JOIN Visited ON Survey.taken = Visited.id
        JOIN Site ON Visited.site = Site.name
    ORDER BY family,personal,name;
`


```python
survey_data = pandas.read_sql_query('SELECT personal,family,name,lat,long,dated,reading,quant \
                  FROM Survey \
                  JOIN Person ON Survey.person = Person.id \
                  JOIN Visited ON Survey.taken = Visited.id \
                  JOIN Site ON Visited.site = Site.name \
                  ORDER BY family,personal,name;', engine)

# The backslashes `\` are an indication to Python that the string (in red, delimited by quotes) continues on the next line.
```


```python
# Display the DataFrame

survey_data
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
      <th>personal</th>
      <th>family</th>
      <th>name</th>
      <th>lat</th>
      <th>long</th>
      <th>dated</th>
      <th>reading</th>
      <th>quant</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>William</td>
      <td>Dyer</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>1927-02-08</td>
      <td>9.82</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>1</th>
      <td>William</td>
      <td>Dyer</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>1927-02-08</td>
      <td>0.13</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>2</th>
      <td>William</td>
      <td>Dyer</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>1927-02-10</td>
      <td>7.80</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>3</th>
      <td>William</td>
      <td>Dyer</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>1927-02-10</td>
      <td>0.09</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Anderson</td>
      <td>Lake</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-01-07</td>
      <td>0.05</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Anderson</td>
      <td>Lake</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-02-26</td>
      <td>0.10</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Anderson</td>
      <td>Lake</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>None</td>
      <td>2.19</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Anderson</td>
      <td>Lake</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>None</td>
      <td>0.09</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Anderson</td>
      <td>Lake</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>None</td>
      <td>-16.00</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Anderson</td>
      <td>Lake</td>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>1932-01-14</td>
      <td>1.46</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Anderson</td>
      <td>Lake</td>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>1932-01-14</td>
      <td>0.21</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-01-07</td>
      <td>8.41</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-01-07</td>
      <td>-21.50</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-01-12</td>
      <td>7.22</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-02-26</td>
      <td>4.35</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-02-26</td>
      <td>-18.50</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Valentina</td>
      <td>Roerich</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>1932-03-22</td>
      <td>11.25</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Valentina</td>
      <td>Roerich</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>None</td>
      <td>41.60</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Valentina</td>
      <td>Roerich</td>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>1932-01-14</td>
      <td>22.50</td>
      <td>sal</td>
    </tr>
  </tbody>
</table>
</div>



#### DATAFRAME PROPERTIES

The `dtypes` attribute and the `describe()` method provide some summary information about the DataFrame:


```python
# Display the data types

survey_data.dtypes
```




    personal     object
    family       object
    name         object
    lat         float64
    long        float64
    dated        object
    reading     float64
    quant        object
    dtype: object




```python
# The describe() function does basic stats on the data (not meaningful in this case!)

survey_data.describe()
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
      <th>lat</th>
      <th>long</th>
      <th>reading</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>19.000000</td>
      <td>19.000000</td>
      <td>19.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>-48.132105</td>
      <td>-126.682632</td>
      <td>3.224737</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.224725</td>
      <td>1.669218</td>
      <td>14.008651</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-49.850000</td>
      <td>-128.570000</td>
      <td>-21.500000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-49.360000</td>
      <td>-127.645000</td>
      <td>0.090000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>-47.150000</td>
      <td>-126.720000</td>
      <td>1.460000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>-47.150000</td>
      <td>-126.720000</td>
      <td>8.105000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>-47.150000</td>
      <td>-123.400000</td>
      <td>41.600000</td>
    </tr>
  </tbody>
</table>
</div>



#### MERGING DATA

DataFrames can be merged in a manner similar to joining tables in SQL:


```python
# merge 'survey' and 'person' DataFrames and name the new DataFrame 'survey_df'
# 'left_on' and 'right_on' indicate which fields to match on

survey_df = pandas.merge(survey, person, left_on='person', right_on='id')
```


```python
# merge 'survey_df' and 'person' DataFrames on 'survey_df.taken' and 'visited.id'
# write back to the survey_df DataFrame

survey_df = pandas.merge(survey_df, visited, left_on='taken', right_on='id')
```


```python
# merge 'survey' and 'person' DataFrames on 'survey_df. site' and 'site.hame'
# write back to survey_df

survey_df = pandas.merge(survey_df, site, left_on='site', right_on='name')
```


```python
# display survey_df

survey_df
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
      <th>taken</th>
      <th>person</th>
      <th>quant</th>
      <th>reading</th>
      <th>id_x</th>
      <th>personal</th>
      <th>family</th>
      <th>id_y</th>
      <th>site</th>
      <th>dated</th>
      <th>name</th>
      <th>lat</th>
      <th>long</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>619</td>
      <td>dyer</td>
      <td>rad</td>
      <td>9.82</td>
      <td>dyer</td>
      <td>William</td>
      <td>Dyer</td>
      <td>619</td>
      <td>DR-1</td>
      <td>1927-02-08</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
    </tr>
    <tr>
      <th>1</th>
      <td>619</td>
      <td>dyer</td>
      <td>sal</td>
      <td>0.13</td>
      <td>dyer</td>
      <td>William</td>
      <td>Dyer</td>
      <td>619</td>
      <td>DR-1</td>
      <td>1927-02-08</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
    </tr>
    <tr>
      <th>2</th>
      <td>622</td>
      <td>dyer</td>
      <td>rad</td>
      <td>7.80</td>
      <td>dyer</td>
      <td>William</td>
      <td>Dyer</td>
      <td>622</td>
      <td>DR-1</td>
      <td>1927-02-10</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
    </tr>
    <tr>
      <th>3</th>
      <td>622</td>
      <td>dyer</td>
      <td>sal</td>
      <td>0.09</td>
      <td>dyer</td>
      <td>William</td>
      <td>Dyer</td>
      <td>622</td>
      <td>DR-1</td>
      <td>1927-02-10</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
    </tr>
    <tr>
      <th>4</th>
      <td>844</td>
      <td>roe</td>
      <td>rad</td>
      <td>11.25</td>
      <td>roe</td>
      <td>Valentina</td>
      <td>Roerich</td>
      <td>844</td>
      <td>DR-1</td>
      <td>1932-03-22</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
    </tr>
    <tr>
      <th>5</th>
      <td>734</td>
      <td>pb</td>
      <td>rad</td>
      <td>8.41</td>
      <td>pb</td>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>734</td>
      <td>DR-3</td>
      <td>1930-01-07</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>6</th>
      <td>734</td>
      <td>pb</td>
      <td>temp</td>
      <td>-21.50</td>
      <td>pb</td>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>734</td>
      <td>DR-3</td>
      <td>1930-01-07</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>7</th>
      <td>734</td>
      <td>lake</td>
      <td>sal</td>
      <td>0.05</td>
      <td>lake</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>734</td>
      <td>DR-3</td>
      <td>1930-01-07</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>8</th>
      <td>735</td>
      <td>pb</td>
      <td>rad</td>
      <td>7.22</td>
      <td>pb</td>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>735</td>
      <td>DR-3</td>
      <td>1930-01-12</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>9</th>
      <td>751</td>
      <td>pb</td>
      <td>rad</td>
      <td>4.35</td>
      <td>pb</td>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>751</td>
      <td>DR-3</td>
      <td>1930-02-26</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>10</th>
      <td>751</td>
      <td>pb</td>
      <td>temp</td>
      <td>-18.50</td>
      <td>pb</td>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>751</td>
      <td>DR-3</td>
      <td>1930-02-26</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>11</th>
      <td>751</td>
      <td>lake</td>
      <td>sal</td>
      <td>0.10</td>
      <td>lake</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>751</td>
      <td>DR-3</td>
      <td>1930-02-26</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>12</th>
      <td>752</td>
      <td>lake</td>
      <td>rad</td>
      <td>2.19</td>
      <td>lake</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>752</td>
      <td>DR-3</td>
      <td>None</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>13</th>
      <td>752</td>
      <td>lake</td>
      <td>sal</td>
      <td>0.09</td>
      <td>lake</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>752</td>
      <td>DR-3</td>
      <td>None</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>14</th>
      <td>752</td>
      <td>lake</td>
      <td>temp</td>
      <td>-16.00</td>
      <td>lake</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>752</td>
      <td>DR-3</td>
      <td>None</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>15</th>
      <td>752</td>
      <td>roe</td>
      <td>sal</td>
      <td>41.60</td>
      <td>roe</td>
      <td>Valentina</td>
      <td>Roerich</td>
      <td>752</td>
      <td>DR-3</td>
      <td>None</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>16</th>
      <td>837</td>
      <td>lake</td>
      <td>rad</td>
      <td>1.46</td>
      <td>lake</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>837</td>
      <td>MSK-4</td>
      <td>1932-01-14</td>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
    </tr>
    <tr>
      <th>17</th>
      <td>837</td>
      <td>lake</td>
      <td>sal</td>
      <td>0.21</td>
      <td>lake</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>837</td>
      <td>MSK-4</td>
      <td>1932-01-14</td>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
    </tr>
    <tr>
      <th>18</th>
      <td>837</td>
      <td>roe</td>
      <td>sal</td>
      <td>22.50</td>
      <td>roe</td>
      <td>Valentina</td>
      <td>Roerich</td>
      <td>837</td>
      <td>MSK-4</td>
      <td>1932-01-14</td>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
    </tr>
  </tbody>
</table>
</div>




```python
# there are redundant columns we need to get rid of: id_x (same as person), id_y (same as taken), name (same as site)
# we can also remove taken and person if we like, as they are keys

survey_df.drop(['taken', 'person', 'id_x', 'id_y', 'site'], axis=1, inplace=True)
```


```python
# here is the result

survey_df
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
      <th>quant</th>
      <th>reading</th>
      <th>personal</th>
      <th>family</th>
      <th>dated</th>
      <th>name</th>
      <th>lat</th>
      <th>long</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>rad</td>
      <td>9.82</td>
      <td>William</td>
      <td>Dyer</td>
      <td>1927-02-08</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
    </tr>
    <tr>
      <th>1</th>
      <td>sal</td>
      <td>0.13</td>
      <td>William</td>
      <td>Dyer</td>
      <td>1927-02-08</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
    </tr>
    <tr>
      <th>2</th>
      <td>rad</td>
      <td>7.80</td>
      <td>William</td>
      <td>Dyer</td>
      <td>1927-02-10</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
    </tr>
    <tr>
      <th>3</th>
      <td>sal</td>
      <td>0.09</td>
      <td>William</td>
      <td>Dyer</td>
      <td>1927-02-10</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
    </tr>
    <tr>
      <th>4</th>
      <td>rad</td>
      <td>11.25</td>
      <td>Valentina</td>
      <td>Roerich</td>
      <td>1932-03-22</td>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
    </tr>
    <tr>
      <th>5</th>
      <td>rad</td>
      <td>8.41</td>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>1930-01-07</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>6</th>
      <td>temp</td>
      <td>-21.50</td>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>1930-01-07</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>7</th>
      <td>sal</td>
      <td>0.05</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>1930-01-07</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>8</th>
      <td>rad</td>
      <td>7.22</td>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>1930-01-12</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>9</th>
      <td>rad</td>
      <td>4.35</td>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>1930-02-26</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>10</th>
      <td>temp</td>
      <td>-18.50</td>
      <td>Frank</td>
      <td>Pabodie</td>
      <td>1930-02-26</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>11</th>
      <td>sal</td>
      <td>0.10</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>1930-02-26</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>12</th>
      <td>rad</td>
      <td>2.19</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>None</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>13</th>
      <td>sal</td>
      <td>0.09</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>None</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>14</th>
      <td>temp</td>
      <td>-16.00</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>None</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>15</th>
      <td>sal</td>
      <td>41.60</td>
      <td>Valentina</td>
      <td>Roerich</td>
      <td>None</td>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
    </tr>
    <tr>
      <th>16</th>
      <td>rad</td>
      <td>1.46</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>1932-01-14</td>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
    </tr>
    <tr>
      <th>17</th>
      <td>sal</td>
      <td>0.21</td>
      <td>Anderson</td>
      <td>Lake</td>
      <td>1932-01-14</td>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
    </tr>
    <tr>
      <th>18</th>
      <td>sal</td>
      <td>22.50</td>
      <td>Valentina</td>
      <td>Roerich</td>
      <td>1932-01-14</td>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
    </tr>
  </tbody>
</table>
</div>




```python
# except for the order of the columns the two DataFrames are the same
# the '\n' adds a blank (new) line

print('survey_data data types:')
print(survey_data.dtypes, '\n')
print('survey_df data types:')
print(survey_df.dtypes)
```

    survey_data data types:
    personal     object
    family       object
    name         object
    lat         float64
    long        float64
    dated        object
    reading     float64
    quant        object
    dtype: object 
    
    survey_df data types:
    quant        object
    reading     float64
    personal     object
    family       object
    dated        object
    name         object
    lat         float64
    long        float64
    dtype: object
    

#### COMPARING DATA

Let's change the order of the columns to they are logical and then sort by site 'name', and then 'family' and 'personal' names




```python
# rewrite the DataFrames

survey_data = survey_data[['name', 'lat', 'long', 'family', 'personal', 'dated', 'reading', 'quant']]
survey_df = survey_df[['name', 'lat', 'long', 'family', 'personal', 'dated', 'reading', 'quant']]
```


```python
# compare DataFrames

survey_data.compare(survey_df)

# first four rows are the same; the rest are different
# the rows that don't match are listed below
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">name</th>
      <th colspan="2" halign="left">lat</th>
      <th colspan="2" halign="left">long</th>
      <th colspan="2" halign="left">family</th>
      <th colspan="2" halign="left">personal</th>
      <th colspan="2" halign="left">dated</th>
      <th colspan="2" halign="left">reading</th>
      <th colspan="2" halign="left">quant</th>
    </tr>
    <tr>
      <th></th>
      <th>self</th>
      <th>other</th>
      <th>self</th>
      <th>other</th>
      <th>self</th>
      <th>other</th>
      <th>self</th>
      <th>other</th>
      <th>self</th>
      <th>other</th>
      <th>self</th>
      <th>other</th>
      <th>self</th>
      <th>other</th>
      <th>self</th>
      <th>other</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>DR-3</td>
      <td>DR-1</td>
      <td>-47.15</td>
      <td>-49.85</td>
      <td>-126.72</td>
      <td>-128.57</td>
      <td>Lake</td>
      <td>Roerich</td>
      <td>Anderson</td>
      <td>Valentina</td>
      <td>1930-01-07</td>
      <td>1932-03-22</td>
      <td>0.05</td>
      <td>11.25</td>
      <td>sal</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Lake</td>
      <td>Pabodie</td>
      <td>Anderson</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>1930-01-07</td>
      <td>0.10</td>
      <td>8.41</td>
      <td>sal</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Lake</td>
      <td>Pabodie</td>
      <td>Anderson</td>
      <td>Frank</td>
      <td>None</td>
      <td>1930-01-07</td>
      <td>2.19</td>
      <td>-21.50</td>
      <td>rad</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>1930-01-07</td>
      <td>0.09</td>
      <td>0.05</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Lake</td>
      <td>Pabodie</td>
      <td>Anderson</td>
      <td>Frank</td>
      <td>None</td>
      <td>1930-01-12</td>
      <td>-16.00</td>
      <td>7.22</td>
      <td>temp</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>9</th>
      <td>MSK-4</td>
      <td>DR-3</td>
      <td>-48.87</td>
      <td>-47.15</td>
      <td>-123.40</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Pabodie</td>
      <td>Anderson</td>
      <td>Frank</td>
      <td>1932-01-14</td>
      <td>1930-02-26</td>
      <td>1.46</td>
      <td>4.35</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>MSK-4</td>
      <td>DR-3</td>
      <td>-48.87</td>
      <td>-47.15</td>
      <td>-123.40</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Pabodie</td>
      <td>Anderson</td>
      <td>Frank</td>
      <td>1932-01-14</td>
      <td>1930-02-26</td>
      <td>0.21</td>
      <td>-18.50</td>
      <td>sal</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>11</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Pabodie</td>
      <td>Lake</td>
      <td>Frank</td>
      <td>Anderson</td>
      <td>1930-01-07</td>
      <td>1930-02-26</td>
      <td>8.41</td>
      <td>0.10</td>
      <td>rad</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>12</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Pabodie</td>
      <td>Lake</td>
      <td>Frank</td>
      <td>Anderson</td>
      <td>1930-01-07</td>
      <td>None</td>
      <td>-21.50</td>
      <td>2.19</td>
      <td>temp</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>13</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Pabodie</td>
      <td>Lake</td>
      <td>Frank</td>
      <td>Anderson</td>
      <td>1930-01-12</td>
      <td>None</td>
      <td>7.22</td>
      <td>0.09</td>
      <td>rad</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>14</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Pabodie</td>
      <td>Lake</td>
      <td>Frank</td>
      <td>Anderson</td>
      <td>1930-02-26</td>
      <td>None</td>
      <td>4.35</td>
      <td>-16.00</td>
      <td>rad</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>15</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Pabodie</td>
      <td>Roerich</td>
      <td>Frank</td>
      <td>Valentina</td>
      <td>1930-02-26</td>
      <td>None</td>
      <td>-18.50</td>
      <td>41.60</td>
      <td>temp</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>16</th>
      <td>DR-1</td>
      <td>MSK-4</td>
      <td>-49.85</td>
      <td>-48.87</td>
      <td>-128.57</td>
      <td>-123.40</td>
      <td>Roerich</td>
      <td>Lake</td>
      <td>Valentina</td>
      <td>Anderson</td>
      <td>1932-03-22</td>
      <td>1932-01-14</td>
      <td>11.25</td>
      <td>1.46</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17</th>
      <td>DR-3</td>
      <td>MSK-4</td>
      <td>-47.15</td>
      <td>-48.87</td>
      <td>-126.72</td>
      <td>-123.40</td>
      <td>Roerich</td>
      <td>Lake</td>
      <td>Valentina</td>
      <td>Anderson</td>
      <td>None</td>
      <td>1932-01-14</td>
      <td>41.60</td>
      <td>0.21</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# sort both DataFrames on name, personal, family, dated
survey_data.sort_values(by = ['name', 'family', 'personal', 'dated'], inplace = True)
survey_df.sort_values(by = ['name', 'family', 'personal', 'dated'], inplace = True)
```


```python
# compare the line numbers of the two DataFrames, survey_data and survey_df:
survey_data
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
      <th>name</th>
      <th>lat</th>
      <th>long</th>
      <th>family</th>
      <th>personal</th>
      <th>dated</th>
      <th>reading</th>
      <th>quant</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-08</td>
      <td>9.82</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>1</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-08</td>
      <td>0.13</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>2</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-10</td>
      <td>7.80</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>3</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-10</td>
      <td>0.09</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>16</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Roerich</td>
      <td>Valentina</td>
      <td>1932-03-22</td>
      <td>11.25</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>4</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1930-01-07</td>
      <td>0.05</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>5</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1930-02-26</td>
      <td>0.10</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>6</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>2.19</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>7</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>0.09</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>8</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>-16.00</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>11</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-07</td>
      <td>8.41</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>12</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-07</td>
      <td>-21.50</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>13</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-12</td>
      <td>7.22</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>14</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>4.35</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>15</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>-18.50</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>17</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Roerich</td>
      <td>Valentina</td>
      <td>None</td>
      <td>41.60</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>9</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1932-01-14</td>
      <td>1.46</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>10</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1932-01-14</td>
      <td>0.21</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>18</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>Roerich</td>
      <td>Valentina</td>
      <td>1932-01-14</td>
      <td>22.50</td>
      <td>sal</td>
    </tr>
  </tbody>
</table>
</div>




```python
survey_df
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
      <th>name</th>
      <th>lat</th>
      <th>long</th>
      <th>family</th>
      <th>personal</th>
      <th>dated</th>
      <th>reading</th>
      <th>quant</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-08</td>
      <td>9.82</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>1</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-08</td>
      <td>0.13</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>2</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-10</td>
      <td>7.80</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>3</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-10</td>
      <td>0.09</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>4</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Roerich</td>
      <td>Valentina</td>
      <td>1932-03-22</td>
      <td>11.25</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>7</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1930-01-07</td>
      <td>0.05</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>11</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1930-02-26</td>
      <td>0.10</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>12</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>2.19</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>13</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>0.09</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>14</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>-16.00</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>5</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-07</td>
      <td>8.41</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>6</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-07</td>
      <td>-21.50</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>8</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-12</td>
      <td>7.22</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>9</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>4.35</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>10</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>-18.50</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>15</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Roerich</td>
      <td>Valentina</td>
      <td>None</td>
      <td>41.60</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>16</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1932-01-14</td>
      <td>1.46</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>17</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1932-01-14</td>
      <td>0.21</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>18</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>Roerich</td>
      <td>Valentina</td>
      <td>1932-01-14</td>
      <td>22.50</td>
      <td>sal</td>
    </tr>
  </tbody>
</table>
</div>




```python
# before comparing again we need to reset the index (i.e. rewrite the line numbers)

survey_data.reset_index(inplace = True, drop = True)
survey_df.reset_index(inplace = True, drop = True)

# and now compare again

print(survey_data.compare(survey_df))

# the result is an empty DataFrame, so survey_data and survey_df are identical
```

    Empty DataFrame
    Columns: []
    Index: []
    


```python
survey_df # same as survey_data; organized by name, family, personal
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
      <th>name</th>
      <th>lat</th>
      <th>long</th>
      <th>family</th>
      <th>personal</th>
      <th>dated</th>
      <th>reading</th>
      <th>quant</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-08</td>
      <td>9.82</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>1</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-08</td>
      <td>0.13</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>2</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-10</td>
      <td>7.80</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>3</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-10</td>
      <td>0.09</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>4</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Roerich</td>
      <td>Valentina</td>
      <td>1932-03-22</td>
      <td>11.25</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>5</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1930-01-07</td>
      <td>0.05</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>6</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1930-02-26</td>
      <td>0.10</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>7</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>2.19</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>8</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>0.09</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>9</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>-16.00</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>10</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-07</td>
      <td>8.41</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>11</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-07</td>
      <td>-21.50</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>12</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-12</td>
      <td>7.22</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>13</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>4.35</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>14</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>-18.50</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>15</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Roerich</td>
      <td>Valentina</td>
      <td>None</td>
      <td>41.60</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>16</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1932-01-14</td>
      <td>1.46</td>
      <td>rad</td>
    </tr>
    <tr>
      <th>17</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1932-01-14</td>
      <td>0.21</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>18</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>Roerich</td>
      <td>Valentina</td>
      <td>1932-01-14</td>
      <td>22.50</td>
      <td>sal</td>
    </tr>
  </tbody>
</table>
</div>



FILTERING DATAFRAMES
To display selected columns as a DataFrame use a list of column names:

```python
survey_data[ ['dated'] ] # this is a 'list' of a single column name
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
      <th>dated</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1927-02-08</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1927-02-08</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1927-02-10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1927-02-10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1932-03-22</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1930-01-07</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1930-02-26</td>
    </tr>
    <tr>
      <th>7</th>
      <td>None</td>
    </tr>
    <tr>
      <th>8</th>
      <td>None</td>
    </tr>
    <tr>
      <th>9</th>
      <td>None</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1930-01-07</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1930-01-07</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1930-01-12</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1930-02-26</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1930-02-26</td>
    </tr>
    <tr>
      <th>15</th>
      <td>None</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1932-01-14</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1932-01-14</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1932-01-14</td>
    </tr>
  </tbody>
</table>
</div>




```python
survey_data[ ['lat', 'long', 'dated'] ]
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
      <th>lat</th>
      <th>long</th>
      <th>dated</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>1927-02-08</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>1927-02-08</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>1927-02-10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>1927-02-10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>1932-03-22</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-01-07</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-02-26</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>None</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>None</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>None</td>
    </tr>
    <tr>
      <th>10</th>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-01-07</td>
    </tr>
    <tr>
      <th>11</th>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-01-07</td>
    </tr>
    <tr>
      <th>12</th>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-01-12</td>
    </tr>
    <tr>
      <th>13</th>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-02-26</td>
    </tr>
    <tr>
      <th>14</th>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>1930-02-26</td>
    </tr>
    <tr>
      <th>15</th>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>None</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>1932-01-14</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>1932-01-14</td>
    </tr>
    <tr>
      <th>18</th>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>1932-01-14</td>
    </tr>
  </tbody>
</table>
</div>



To display single columns as a Pandas Series, rather than a DataFrame, either of these notations is valid:
`survey_data['dated']` or `survey_data.dated


```python
survey_data['dated']
```




    0     1927-02-08
    1     1927-02-08
    2     1927-02-10
    3     1927-02-10
    4     1932-03-22
    5     1930-01-07
    6     1930-02-26
    7           None
    8           None
    9           None
    10    1930-01-07
    11    1930-01-07
    12    1930-01-12
    13    1930-02-26
    14    1930-02-26
    15          None
    16    1932-01-14
    17    1932-01-14
    18    1932-01-14
    Name: dated, dtype: object




```python
survey_data.dated
```




    0     1927-02-08
    1     1927-02-08
    2     1927-02-10
    3     1927-02-10
    4     1932-03-22
    5     1930-01-07
    6     1930-02-26
    7           None
    8           None
    9           None
    10    1930-01-07
    11    1930-01-07
    12    1930-01-12
    13    1930-02-26
    14    1930-02-26
    15          None
    16    1932-01-14
    17    1932-01-14
    18    1932-01-14
    Name: dated, dtype: object



`.loc` and `.iloc` are used to filter by both rows and columns by 'slicing'. The format of both methods is similar:

`DataFrame.loc[row-start : row-stop : row-step , col-start : col-stop : col-step]`
`DataFrame.iloc[row-start : row-stop : row-step , col-start : col-stop : col-step]`

`.loc` is used when referring to row and column __labels__; `.iloc` is used when referring to row and column __numbers__. (In our examples the row labels are numbers.)


```python
# display rows 0 through 6 (inclusive), skip by 2; display columns 'personal' through 'dated' (inclusive), skip by 2
survey_data.loc[0:6:2, 'family':'dated':2]
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
      <th>family</th>
      <th>dated</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Dyer</td>
      <td>1927-02-08</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Dyer</td>
      <td>1927-02-10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Roerich</td>
      <td>1932-03-22</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Lake</td>
      <td>1930-02-26</td>
    </tr>
  </tbody>
</table>
</div>



Note that the top of the range in `.loc` is inclusive; top of range in `.iloc` is exclusive (as is normal in Python). The following two commands produce the same result:


```python
survey_data.iloc[2:9, 2:5]
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
      <th>long</th>
      <th>family</th>
      <th>personal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-128.57</td>
      <td>Roerich</td>
      <td>Valentina</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
    </tr>
  </tbody>
</table>
</div>




```python
survey_data.loc[2:8, 'long':'personal']
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
      <th>long</th>
      <th>family</th>
      <th>personal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-128.57</td>
      <td>Roerich</td>
      <td>Valentina</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
    </tr>
  </tbody>
</table>
</div>



To display specific rows and columns, use lists or rows and columns (i.e. within square brackets, separated with commas):


```python
survey_data.loc[[0,5], ['personal','dated']]
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
      <th>personal</th>
      <th>dated</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>William</td>
      <td>1927-02-08</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Anderson</td>
      <td>1930-01-07</td>
    </tr>
  </tbody>
</table>
</div>



Data can be selected using conditional statements:


```python
survey_data[ survey_data.quant == 'temp' ] # can use either survey_data.quant or survey_data['quant'] here
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
      <th>name</th>
      <th>lat</th>
      <th>long</th>
      <th>family</th>
      <th>personal</th>
      <th>dated</th>
      <th>reading</th>
      <th>quant</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>-16.0</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>11</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-07</td>
      <td>-21.5</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>14</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>-18.5</td>
      <td>temp</td>
    </tr>
  </tbody>
</table>
</div>




```python
survey_data[ (survey_data.dated < '1930-01-01') & (survey_data.quant=='sal') ]
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
      <th>name</th>
      <th>lat</th>
      <th>long</th>
      <th>family</th>
      <th>personal</th>
      <th>dated</th>
      <th>reading</th>
      <th>quant</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-08</td>
      <td>0.13</td>
      <td>sal</td>
    </tr>
    <tr>
      <th>3</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-10</td>
      <td>0.09</td>
      <td>sal</td>
    </tr>
  </tbody>
</table>
</div>




```python
survey_data[survey_data.quant=='temp']
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
      <th>name</th>
      <th>lat</th>
      <th>long</th>
      <th>family</th>
      <th>personal</th>
      <th>dated</th>
      <th>reading</th>
      <th>quant</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>-16.0</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>11</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-07</td>
      <td>-21.5</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>14</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>-18.5</td>
      <td>temp</td>
    </tr>
  </tbody>
</table>
</div>



To save the result of a filtered DataFrame to a new DataFrame use the `.copy()` method and assign to a new name:


```python
temps = survey_data[survey_data.quant=='temp'].copy()
```


```python
temps
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
      <th>name</th>
      <th>lat</th>
      <th>long</th>
      <th>family</th>
      <th>personal</th>
      <th>dated</th>
      <th>reading</th>
      <th>quant</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>-16.0</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>11</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-07</td>
      <td>-21.5</td>
      <td>temp</td>
    </tr>
    <tr>
      <th>14</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>-18.5</td>
      <td>temp</td>
    </tr>
  </tbody>
</table>
</div>



Let's create a new column for Celsius temperatures. First create a function to calcuate Celsius temps and test it:


```python
def celsius(temp):
    temp_c = round((temp-32)*(5/9), 1)
    return temp_c
```


```python
celsius(212)
```




    100.0




```python
celsius(32)
```




    0.0




```python
celsius(62)
```




    16.7



Now create a new column, called `celsius`, with values derived from the `reading` column. The `.apply()` method 
takes the function `celsius`, defined above, as an argument and applies it to the `reading` column:


```python
temps['celsius'] = temps['reading'].apply(celsius)
```


```python
temps
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
      <th>name</th>
      <th>lat</th>
      <th>long</th>
      <th>family</th>
      <th>personal</th>
      <th>dated</th>
      <th>reading</th>
      <th>quant</th>
      <th>celsius</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>-16.0</td>
      <td>temp</td>
      <td>-26.7</td>
    </tr>
    <tr>
      <th>11</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-07</td>
      <td>-21.5</td>
      <td>temp</td>
      <td>-29.7</td>
    </tr>
    <tr>
      <th>14</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>-18.5</td>
      <td>temp</td>
      <td>-28.1</td>
    </tr>
  </tbody>
</table>
</div>



We can use a conditional on the survey_data DataFrame, `survey_data.quant=='temp'`, to limit the application to
only the temperature readings:


```python
survey_data['celsius'] = survey_data[survey_data.quant=='temp']['reading'].apply(celsius)
```


```python
survey_data
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
      <th>name</th>
      <th>lat</th>
      <th>long</th>
      <th>family</th>
      <th>personal</th>
      <th>dated</th>
      <th>reading</th>
      <th>quant</th>
      <th>celsius</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-08</td>
      <td>9.82</td>
      <td>rad</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-08</td>
      <td>0.13</td>
      <td>sal</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-10</td>
      <td>7.80</td>
      <td>rad</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Dyer</td>
      <td>William</td>
      <td>1927-02-10</td>
      <td>0.09</td>
      <td>sal</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>DR-1</td>
      <td>-49.85</td>
      <td>-128.57</td>
      <td>Roerich</td>
      <td>Valentina</td>
      <td>1932-03-22</td>
      <td>11.25</td>
      <td>rad</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1930-01-07</td>
      <td>0.05</td>
      <td>sal</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1930-02-26</td>
      <td>0.10</td>
      <td>sal</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>2.19</td>
      <td>rad</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>0.09</td>
      <td>sal</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>None</td>
      <td>-16.00</td>
      <td>temp</td>
      <td>-26.7</td>
    </tr>
    <tr>
      <th>10</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-07</td>
      <td>8.41</td>
      <td>rad</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-07</td>
      <td>-21.50</td>
      <td>temp</td>
      <td>-29.7</td>
    </tr>
    <tr>
      <th>12</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-01-12</td>
      <td>7.22</td>
      <td>rad</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>4.35</td>
      <td>rad</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Pabodie</td>
      <td>Frank</td>
      <td>1930-02-26</td>
      <td>-18.50</td>
      <td>temp</td>
      <td>-28.1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>DR-3</td>
      <td>-47.15</td>
      <td>-126.72</td>
      <td>Roerich</td>
      <td>Valentina</td>
      <td>None</td>
      <td>41.60</td>
      <td>sal</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>16</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1932-01-14</td>
      <td>1.46</td>
      <td>rad</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>Lake</td>
      <td>Anderson</td>
      <td>1932-01-14</td>
      <td>0.21</td>
      <td>sal</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>18</th>
      <td>MSK-4</td>
      <td>-48.87</td>
      <td>-123.40</td>
      <td>Roerich</td>
      <td>Valentina</td>
      <td>1932-01-14</td>
      <td>22.50</td>
      <td>sal</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



And finally, save our expanded DataFrame to a CSV file.


```python
survey_data.to_csv('mynewdata.csv')
```



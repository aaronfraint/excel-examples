# Read data from Excel into Python

(this is a `markdown` cell, which is an easy method of formatting text. [See this guide](https://docs.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax))

Markdown cells are used for longform notes. 

An inline comment within a `code` cell is prefixed with the pound sign:

`# I am a comment, not code`

In this script we will: 
- `import pandas`
- read an excel file
- print some information about it
- do a basic filter on the data


```python
# Import the modules we want to use
import pandas as pd
```


```python
# Read the CSV into a "dataframe" that we will refer to as "df"

df = pd.read_csv("data/employee_salaries.csv")
```


```python
# You can see the first or last 5 rows with .head() or .tail()

df.tail()
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
      <th>objectid</th>
      <th>calendar_year</th>
      <th>quarter</th>
      <th>last_name</th>
      <th>first_name</th>
      <th>title</th>
      <th>department</th>
      <th>annual_salary</th>
      <th>ytd_overtime_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>471165</th>
      <td>565386</td>
      <td>2019</td>
      <td>1</td>
      <td>VAZHAPPILLY</td>
      <td>BINCY TERENA</td>
      <td>LEGAL CLERK 1</td>
      <td>COMMON PLEAS COURT</td>
      <td>33419.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>471166</th>
      <td>565387</td>
      <td>2019</td>
      <td>1</td>
      <td>VAZQUEZ</td>
      <td>CECILIA</td>
      <td>COURT REPRESENTATIOVE 2 (UNION)</td>
      <td>COMMON PLEAS COURT</td>
      <td>49732.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>471167</th>
      <td>565388</td>
      <td>2019</td>
      <td>1</td>
      <td>VAZQUEZ</td>
      <td>JENITZA</td>
      <td>ADM TECHNICIAN I</td>
      <td>COMMON PLEAS COURT</td>
      <td>38691.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>471168</th>
      <td>565389</td>
      <td>2019</td>
      <td>1</td>
      <td>VAZQUEZ</td>
      <td>MONICA</td>
      <td>COURT REPORTER TRAINEE</td>
      <td>COMMON PLEAS COURT</td>
      <td>46127.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>471169</th>
      <td>565390</td>
      <td>2019</td>
      <td>1</td>
      <td>VEASEY III</td>
      <td>JOSEPH</td>
      <td>PROBATION OFFICER 2</td>
      <td>COMMON PLEAS COURT</td>
      <td>61064.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# the .shape property will tell you the number of rows and columns

df.shape

# In this case we have almost half a million rows (~471,000)
```




    (471170, 9)




```python
# print out the name of each column and the datatype it contains

df.dtypes
```




    objectid                int64
    calendar_year           int64
    quarter                 int64
    last_name              object
    first_name             object
    title                  object
    department             object
    annual_salary         float64
    ytd_overtime_gross    float64
    dtype: object



## Filtering

Filters in pandas leverage boolean true/false masks. In python the double equal sign `==` means "is like". For example:

`df["last_name"] == "KENNEY"` returns a series, with true or false if the condition matches.

You can then use this series to "mask" the original dataset, returning only the rows that are True:

`df[df["last_name"] == "KENNEY"]`

You can chain multiple masks together, but need to wrap each condition within a set of parentheses:

`df[(df["last_name"] == "KENNEY") & (df["first_name"] == "JAMES")]`

When combnining conditions, the ampersand symbol `&` is "AND" and the pipe symbol `|` is "OR"


```python
# You can filter data and store it in a new variable

# In this case I'm filtering to rows with first name "JAMES" and last name "KENNEY"

kenney_data = df[(df["last_name"] == "KENNEY") & (df["first_name"] == "JAMES")]
```


```python
# In a notebook, a line of code with an object that was previously created will print out the object

kenney_data
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
      <th>objectid</th>
      <th>calendar_year</th>
      <th>quarter</th>
      <th>last_name</th>
      <th>first_name</th>
      <th>title</th>
      <th>department</th>
      <th>annual_salary</th>
      <th>ytd_overtime_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>28919</th>
      <td>28177</td>
      <td>2016</td>
      <td>1</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>217820.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>32854</th>
      <td>30959</td>
      <td>2016</td>
      <td>2</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>217820.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>62462</th>
      <td>61673</td>
      <td>2016</td>
      <td>3</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218255.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>95600</th>
      <td>93127</td>
      <td>2016</td>
      <td>4</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218255.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>123292</th>
      <td>123934</td>
      <td>2017</td>
      <td>1</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218255.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>150889</th>
      <td>154717</td>
      <td>2017</td>
      <td>2</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218255.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>192890</th>
      <td>186084</td>
      <td>2017</td>
      <td>3</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218474.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>217486</th>
      <td>376531</td>
      <td>2017</td>
      <td>4</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218474.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>256755</th>
      <td>439283</td>
      <td>2018</td>
      <td>2</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218474.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>289411</th>
      <td>312328</td>
      <td>2018</td>
      <td>2</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218474.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>313692</th>
      <td>344362</td>
      <td>2018</td>
      <td>3</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218474.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>315593</th>
      <td>407961</td>
      <td>2018</td>
      <td>1</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218474.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>372517</th>
      <td>471317</td>
      <td>2018</td>
      <td>3</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218474.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>409364</th>
      <td>503537</td>
      <td>2018</td>
      <td>4</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218474.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>440537</th>
      <td>535009</td>
      <td>2019</td>
      <td>1</td>
      <td>KENNEY</td>
      <td>JAMES</td>
      <td>MAYOR</td>
      <td>MAYOR'S OFFICE</td>
      <td>218474.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



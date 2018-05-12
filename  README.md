
# PyCity Schools Analysis

# The district schools have more students than charter schools. For this raeson it looks like the budget is higher.
# The charter schools show better performance based on the overall pasing rate.
# The charter schdools appears to be more focused on math while the district is on reading.
# The budget per student does not seems to be a factor to help in getting better performance.
# Above based on the top performing schools and the budget p/student.
# There is not that much fluctuation or difference in the scores between the different grades.



```python
# Importing Dependencies
import pandas as pd
import numpy as np
```


```python
# Assigning the path to our CSV files
file = "raw_data/schools_complete.csv"
file_2 = "raw_data/students_complete.csv"
```


```python
# Read the School_Complete data into pandas
school = pd.read_csv(file)
school.head()
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
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
students = pd.read_csv(file_2)
students.head()
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
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
school = school.rename(columns={"name": "school"})
school.head()
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
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
merged_df = pd.merge(school, students, on = "school")
merged_df.head()
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
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
merged_df.count()
```




    School ID        39170
    school           39170
    type             39170
    size             39170
    budget           39170
    Student ID       39170
    name             39170
    gender           39170
    grade            39170
    reading_score    39170
    math_score       39170
    dtype: int64




```python
school.count()
```




    School ID    15
    school       15
    type         15
    size         15
    budget       15
    dtype: int64




```python
students.count()
```




    Student ID       39170
    name             39170
    gender           39170
    grade            39170
    school           39170
    reading_score    39170
    math_score       39170
    dtype: int64




```python
total_budget = school["budget"].sum()
total_budget
```




    24649428




```python
# getting the required data
student_in_school = pd.DataFrame(merged_df["school"].value_counts())
student_in_school
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
      <th>school</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>4976</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>4761</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>4635</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>3999</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>2949</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>2917</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>2739</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>2283</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>1858</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>1800</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>1761</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>1635</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>1468</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>962</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>427</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_names = merged_df['school'].unique()
school_names
```




    array(['Huang High School', 'Figueroa High School', 'Shelton High School',
           'Hernandez High School', 'Griffin High School',
           'Wilson High School', 'Cabrera High School', 'Bailey High School',
           'Holden High School', 'Pena High School', 'Wright High School',
           'Rodriguez High School', 'Johnson High School', 'Ford High School',
           'Thomas High School'], dtype=object)




```python
school_number = len(school_names)
school_number
```




    15




```python
total_students = students['name'].count()
total_students
```




    39170




```python
math_score_average = merged_df["math_score"].mean()
math_score_average
```




    78.98537145774827




```python
reading_score_average = merged_df["reading_score"].mean()
reading_score_average
```




    81.87784018381414




```python
# Amount of passing math scores (Above 70)
num_passing_math = students.loc[students['math_score'] >= 70]['math_score'].count()
percent_math_pass = num_passing_math/float(total_students) * 100
percent_math_pass
```




    74.9808526933878




```python
# Amount of passing reading scores (Above 70)
num_passing_read = students.loc[students['reading_score'] >= 70]['reading_score'].count()
percent_read_pass = num_passing_read/float(total_students) * 100
percent_read_pass
```




    85.80546336482001




```python
overall_passing_rate = (percent_math_pass + percent_read_pass) / 2
overall_passing_rate
```




    80.39315802910392




```python
# Creating a District summary DataFrame using above values
dist_summary_df = pd.DataFrame({"Total Schools" : [school_number],
                            "Total Students": [total_students],
                           "Total Budget": [total_budget],
                           "Average Math Score": [math_score_average],
                           "Average Reading Score": [reading_score_average],
                           "% Passing Math": [percent_math_pass],
                           "% Passing Reading": [percent_read_pass],     
                           "Overall Passing Rate": [overall_passing_rate]})


dist_summary_df
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
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Overall Passing Rate</th>
      <th>Total Budget</th>
      <th>Total Schools</th>
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>74.980853</td>
      <td>85.805463</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>80.393158</td>
      <td>24649428</td>
      <td>15</td>
      <td>39170</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create a different Data Frame so we can arrange the columns the way that it is required
district_summary = dist_summary_df[["Total Schools", "Total Students", "Total Budget", "Average Math Score", "Average Reading Score", 
                                 '% Passing Math', '% Passing Reading', 'Overall Passing Rate']]
district_summary
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
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39170</td>
      <td>24649428</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>74.980853</td>
      <td>85.805463</td>
      <td>80.393158</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Use Map to format all the columns
district_summary["Total Students"] = district_summary["Total Students"].map("{:,}".format)
district_summary["Total Budget"] = district_summary["Total Budget"].map("${:,.2f}".format)
district_summary["Average Math Score"] = district_summary["Average Math Score"].map("{:.6f}".format)
```

# District Summary


```python
district_summary
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
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428.00</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>74.980853</td>
      <td>85.805463</td>
      <td>80.393158</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Group everything by School to be used for the School Summary
school_grouped = merged_df.set_index('school').groupby("school")
school_grouped
#.groupby(['school'])
#school_grouped.head()
```




    <pandas.core.groupby.DataFrameGroupBy object at 0x112834128>




```python
# Obtain the school type (either District or Charter)
school_type = school.set_index('school') ['type']
school_type.head()
```




    school
    Huang High School        District
    Figueroa High School     District
    Shelton High School       Charter
    Hernandez High School    District
    Griffin High School       Charter
    Name: type, dtype: object




```python
# Get students by School
students_per_school = school_grouped['Student ID'].count()
students_per_school
```




    school
    Bailey High School       4976
    Cabrera High School      1858
    Figueroa High School     2949
    Ford High School         2739
    Griffin High School      1468
    Hernandez High School    4635
    Holden High School        427
    Huang High School        2917
    Johnson High School      4761
    Pena High School          962
    Rodriguez High School    3999
    Shelton High School      1761
    Thomas High School       1635
    Wilson High School       2283
    Wright High School       1800
    Name: Student ID, dtype: int64




```python
# Get budget by school
budget_per_school = school.set_index('school')['budget']
budget_per_school
```




    school
    Huang High School        1910635
    Figueroa High School     1884411
    Shelton High School      1056600
    Hernandez High School    3022020
    Griffin High School       917500
    Wilson High School       1319574
    Cabrera High School      1081356
    Bailey High School       3124928
    Holden High School        248087
    Pena High School          585858
    Wright High School       1049400
    Rodriguez High School    2547363
    Johnson High School      3094650
    Ford High School         1763916
    Thomas High School       1043130
    Name: budget, dtype: int64




```python
# Get the amount of budget per student
student_budget = school.set_index('school')['budget'] / school.set_index('school')['size']
student_budget.head()
```




    school
    Huang High School        655.0
    Figueroa High School     639.0
    Shelton High School      600.0
    Hernandez High School    652.0
    Griffin High School      625.0
    dtype: float64




```python
# Obtain the Average Math & Reading Scores
school_average_math = school_grouped['math_score'].mean()
school_average_reading = school_grouped['reading_score'].mean()
school_average_reading
```




    school
    Bailey High School       81.033963
    Cabrera High School      83.975780
    Figueroa High School     81.158020
    Ford High School         80.746258
    Griffin High School      83.816757
    Hernandez High School    80.934412
    Holden High School       83.814988
    Huang High School        81.182722
    Johnson High School      80.966394
    Pena High School         84.044699
    Rodriguez High School    80.744686
    Shelton High School      83.725724
    Thomas High School       83.848930
    Wilson High School       83.989488
    Wright High School       83.955000
    Name: reading_score, dtype: float64




```python
# Get the passing math % per school
school_passing_math = (merged_df[merged_df['math_score'] >= 70].groupby('school')['Student ID'].count() / students_per_school) * 100
school_passing_math
```




    school
    Bailey High School       66.680064
    Cabrera High School      94.133477
    Figueroa High School     65.988471
    Ford High School         68.309602
    Griffin High School      93.392371
    Hernandez High School    66.752967
    Holden High School       92.505855
    Huang High School        65.683922
    Johnson High School      66.057551
    Pena High School         94.594595
    Rodriguez High School    66.366592
    Shelton High School      93.867121
    Thomas High School       93.272171
    Wilson High School       93.867718
    Wright High School       93.333333
    Name: Student ID, dtype: float64




```python
# Get the passing reading % per school
school_passing_reading = (merged_df[merged_df['reading_score'] >= 70].groupby('school')['Student ID'].count() / students_per_school) * 100
school_passing_reading
```




    school
    Bailey High School       81.933280
    Cabrera High School      97.039828
    Figueroa High School     80.739234
    Ford High School         79.299014
    Griffin High School      97.138965
    Hernandez High School    80.862999
    Holden High School       96.252927
    Huang High School        81.316421
    Johnson High School      81.222432
    Pena High School         95.945946
    Rodriguez High School    80.220055
    Shelton High School      95.854628
    Thomas High School       97.308869
    Wilson High School       96.539641
    Wright High School       96.611111
    Name: Student ID, dtype: float64




```python
# Obtaining Overall Passing Rate per school
overall_pass_rate_school = (school_passing_math + school_passing_reading) / 2
overall_pass_rate_school
```




    school
    Bailey High School       74.306672
    Cabrera High School      95.586652
    Figueroa High School     73.363852
    Ford High School         73.804308
    Griffin High School      95.265668
    Hernandez High School    73.807983
    Holden High School       94.379391
    Huang High School        73.500171
    Johnson High School      73.639992
    Pena High School         95.270270
    Rodriguez High School    73.293323
    Shelton High School      94.860875
    Thomas High School       95.290520
    Wilson High School       95.203679
    Wright High School       94.972222
    Name: Student ID, dtype: float64




```python
# Creating the school summary DataFrame using above values
school_summary_df = pd.DataFrame({"School Type" : school_type,
                            "Total Students": students_per_school,
                           "Total School Budget": budget_per_school,
                           "Per Student Budget": student_budget,       
                           "Average Math Score": school_average_math,
                           "Average Reading Score": school_average_reading,
                           '% Passing Math': school_passing_math,
                           '% Passing Reading': school_passing_reading,     
                           "Overall Passing Rate": overall_pass_rate_school})
```


```python
# Arranging the columns the way that it is required
school_summary_df = school_summary_df[['School Type', 'Total Students', 'Total School Budget',
                   'Per Student Budget', 'Average Math Score', 'Average Reading Score',
                   '% Passing Math', '% Passing Reading', 'Overall Passing Rate']]
school_summary_df
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
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>73.807983</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>92.505855</td>
      <td>96.252927</td>
      <td>94.379391</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>94.860875</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>94.972222</td>
    </tr>
  </tbody>
</table>
</div>



# School Summary


```python
# Format the columns
school_summary_df.style.format ({"Total School Budget" : "${:,.2f}",
                                "Per Student Budget" : "${:,.2f}"})
```




<style  type="text/css" >
</style>  
<table id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >School Type</th> 
        <th class="col_heading level0 col1" >Total Students</th> 
        <th class="col_heading level0 col2" >Total School Budget</th> 
        <th class="col_heading level0 col3" >Per Student Budget</th> 
        <th class="col_heading level0 col4" >Average Math Score</th> 
        <th class="col_heading level0 col5" >Average Reading Score</th> 
        <th class="col_heading level0 col6" >% Passing Math</th> 
        <th class="col_heading level0 col7" >% Passing Reading</th> 
        <th class="col_heading level0 col8" >Overall Passing Rate</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row0" class="row_heading level0 row0" >Bailey High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row0_col0" class="data row0 col0" >District</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row0_col1" class="data row0 col1" >4976</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row0_col2" class="data row0 col2" >$3,124,928.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row0_col3" class="data row0 col3" >$628.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row0_col4" class="data row0 col4" >77.0484</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row0_col5" class="data row0 col5" >81.034</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row0_col6" class="data row0 col6" >66.6801</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row0_col7" class="data row0 col7" >81.9333</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row0_col8" class="data row0 col8" >74.3067</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row1" class="row_heading level0 row1" >Cabrera High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row1_col0" class="data row1 col0" >Charter</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row1_col1" class="data row1 col1" >1858</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row1_col2" class="data row1 col2" >$1,081,356.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row1_col3" class="data row1 col3" >$582.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row1_col4" class="data row1 col4" >83.0619</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row1_col5" class="data row1 col5" >83.9758</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row1_col6" class="data row1 col6" >94.1335</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row1_col7" class="data row1 col7" >97.0398</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row1_col8" class="data row1 col8" >95.5867</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row2" class="row_heading level0 row2" >Figueroa High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row2_col0" class="data row2 col0" >District</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row2_col1" class="data row2 col1" >2949</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row2_col2" class="data row2 col2" >$1,884,411.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row2_col3" class="data row2 col3" >$639.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row2_col4" class="data row2 col4" >76.7118</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row2_col5" class="data row2 col5" >81.158</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row2_col6" class="data row2 col6" >65.9885</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row2_col7" class="data row2 col7" >80.7392</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row2_col8" class="data row2 col8" >73.3639</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row3" class="row_heading level0 row3" >Ford High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row3_col0" class="data row3 col0" >District</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row3_col1" class="data row3 col1" >2739</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row3_col2" class="data row3 col2" >$1,763,916.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row3_col3" class="data row3 col3" >$644.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row3_col4" class="data row3 col4" >77.1026</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row3_col5" class="data row3 col5" >80.7463</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row3_col6" class="data row3 col6" >68.3096</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row3_col7" class="data row3 col7" >79.299</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row3_col8" class="data row3 col8" >73.8043</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row4" class="row_heading level0 row4" >Griffin High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row4_col0" class="data row4 col0" >Charter</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row4_col1" class="data row4 col1" >1468</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row4_col2" class="data row4 col2" >$917,500.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row4_col3" class="data row4 col3" >$625.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row4_col4" class="data row4 col4" >83.3515</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row4_col5" class="data row4 col5" >83.8168</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row4_col6" class="data row4 col6" >93.3924</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row4_col7" class="data row4 col7" >97.139</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row4_col8" class="data row4 col8" >95.2657</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row5" class="row_heading level0 row5" >Hernandez High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row5_col0" class="data row5 col0" >District</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row5_col1" class="data row5 col1" >4635</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row5_col2" class="data row5 col2" >$3,022,020.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row5_col3" class="data row5 col3" >$652.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row5_col4" class="data row5 col4" >77.2898</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row5_col5" class="data row5 col5" >80.9344</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row5_col6" class="data row5 col6" >66.753</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row5_col7" class="data row5 col7" >80.863</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row5_col8" class="data row5 col8" >73.808</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row6" class="row_heading level0 row6" >Holden High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row6_col0" class="data row6 col0" >Charter</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row6_col1" class="data row6 col1" >427</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row6_col2" class="data row6 col2" >$248,087.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row6_col3" class="data row6 col3" >$581.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row6_col4" class="data row6 col4" >83.8033</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row6_col5" class="data row6 col5" >83.815</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row6_col6" class="data row6 col6" >92.5059</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row6_col7" class="data row6 col7" >96.2529</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row6_col8" class="data row6 col8" >94.3794</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row7" class="row_heading level0 row7" >Huang High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row7_col0" class="data row7 col0" >District</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row7_col1" class="data row7 col1" >2917</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row7_col2" class="data row7 col2" >$1,910,635.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row7_col3" class="data row7 col3" >$655.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row7_col4" class="data row7 col4" >76.6294</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row7_col5" class="data row7 col5" >81.1827</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row7_col6" class="data row7 col6" >65.6839</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row7_col7" class="data row7 col7" >81.3164</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row7_col8" class="data row7 col8" >73.5002</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row8" class="row_heading level0 row8" >Johnson High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row8_col0" class="data row8 col0" >District</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row8_col1" class="data row8 col1" >4761</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row8_col2" class="data row8 col2" >$3,094,650.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row8_col3" class="data row8 col3" >$650.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row8_col4" class="data row8 col4" >77.0725</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row8_col5" class="data row8 col5" >80.9664</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row8_col6" class="data row8 col6" >66.0576</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row8_col7" class="data row8 col7" >81.2224</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row8_col8" class="data row8 col8" >73.64</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row9" class="row_heading level0 row9" >Pena High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row9_col0" class="data row9 col0" >Charter</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row9_col1" class="data row9 col1" >962</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row9_col2" class="data row9 col2" >$585,858.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row9_col3" class="data row9 col3" >$609.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row9_col4" class="data row9 col4" >83.8399</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row9_col5" class="data row9 col5" >84.0447</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row9_col6" class="data row9 col6" >94.5946</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row9_col7" class="data row9 col7" >95.9459</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row9_col8" class="data row9 col8" >95.2703</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row10" class="row_heading level0 row10" >Rodriguez High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row10_col0" class="data row10 col0" >District</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row10_col1" class="data row10 col1" >3999</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row10_col2" class="data row10 col2" >$2,547,363.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row10_col3" class="data row10 col3" >$637.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row10_col4" class="data row10 col4" >76.8427</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row10_col5" class="data row10 col5" >80.7447</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row10_col6" class="data row10 col6" >66.3666</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row10_col7" class="data row10 col7" >80.2201</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row10_col8" class="data row10 col8" >73.2933</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row11" class="row_heading level0 row11" >Shelton High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row11_col0" class="data row11 col0" >Charter</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row11_col1" class="data row11 col1" >1761</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row11_col2" class="data row11 col2" >$1,056,600.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row11_col3" class="data row11 col3" >$600.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row11_col4" class="data row11 col4" >83.3595</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row11_col5" class="data row11 col5" >83.7257</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row11_col6" class="data row11 col6" >93.8671</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row11_col7" class="data row11 col7" >95.8546</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row11_col8" class="data row11 col8" >94.8609</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row12" class="row_heading level0 row12" >Thomas High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row12_col0" class="data row12 col0" >Charter</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row12_col1" class="data row12 col1" >1635</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row12_col2" class="data row12 col2" >$1,043,130.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row12_col3" class="data row12 col3" >$638.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row12_col4" class="data row12 col4" >83.4183</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row12_col5" class="data row12 col5" >83.8489</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row12_col6" class="data row12 col6" >93.2722</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row12_col7" class="data row12 col7" >97.3089</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row12_col8" class="data row12 col8" >95.2905</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row13" class="row_heading level0 row13" >Wilson High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row13_col0" class="data row13 col0" >Charter</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row13_col1" class="data row13 col1" >2283</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row13_col2" class="data row13 col2" >$1,319,574.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row13_col3" class="data row13 col3" >$578.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row13_col4" class="data row13 col4" >83.2742</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row13_col5" class="data row13 col5" >83.9895</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row13_col6" class="data row13 col6" >93.8677</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row13_col7" class="data row13 col7" >96.5396</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row13_col8" class="data row13 col8" >95.2037</td> 
    </tr>    <tr> 
        <th id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8level0_row14" class="row_heading level0 row14" >Wright High School</th> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row14_col0" class="data row14 col0" >Charter</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row14_col1" class="data row14 col1" >1800</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row14_col2" class="data row14 col2" >$1,049,400.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row14_col3" class="data row14 col3" >$583.00</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row14_col4" class="data row14 col4" >83.6822</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row14_col5" class="data row14 col5" >83.955</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row14_col6" class="data row14 col6" >93.3333</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row14_col7" class="data row14 col7" >96.6111</td> 
        <td id="T_6ecbd152_563e_11e8_84a9_a8667f22f1d8row14_col8" class="data row14 col8" >94.9722</td> 
    </tr></tbody> 
</table> 



# Top Performing Schools (By Passing Rate)


```python
# Sorting the data frame to obtain the top FIVE Overall Passing Rate Schools
top_five_schools = school_summary_df.sort_values('Overall Passing Rate', ascending=False)
top_five_schools.head(5).style.format ({"Total School Budget" : "${:,.2f}",
                                "Per Student Budget" : "${:,.2f}"})
```




<style  type="text/css" >
</style>  
<table id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >School Type</th> 
        <th class="col_heading level0 col1" >Total Students</th> 
        <th class="col_heading level0 col2" >Total School Budget</th> 
        <th class="col_heading level0 col3" >Per Student Budget</th> 
        <th class="col_heading level0 col4" >Average Math Score</th> 
        <th class="col_heading level0 col5" >Average Reading Score</th> 
        <th class="col_heading level0 col6" >% Passing Math</th> 
        <th class="col_heading level0 col7" >% Passing Reading</th> 
        <th class="col_heading level0 col8" >Overall Passing Rate</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8level0_row0" class="row_heading level0 row0" >Cabrera High School</th> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row0_col0" class="data row0 col0" >Charter</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row0_col1" class="data row0 col1" >1858</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row0_col2" class="data row0 col2" >$1,081,356.00</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row0_col3" class="data row0 col3" >$582.00</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row0_col4" class="data row0 col4" >83.0619</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row0_col5" class="data row0 col5" >83.9758</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row0_col6" class="data row0 col6" >94.1335</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row0_col7" class="data row0 col7" >97.0398</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row0_col8" class="data row0 col8" >95.5867</td> 
    </tr>    <tr> 
        <th id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8level0_row1" class="row_heading level0 row1" >Thomas High School</th> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row1_col0" class="data row1 col0" >Charter</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row1_col1" class="data row1 col1" >1635</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row1_col2" class="data row1 col2" >$1,043,130.00</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row1_col3" class="data row1 col3" >$638.00</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row1_col4" class="data row1 col4" >83.4183</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row1_col5" class="data row1 col5" >83.8489</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row1_col6" class="data row1 col6" >93.2722</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row1_col7" class="data row1 col7" >97.3089</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row1_col8" class="data row1 col8" >95.2905</td> 
    </tr>    <tr> 
        <th id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8level0_row2" class="row_heading level0 row2" >Pena High School</th> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row2_col0" class="data row2 col0" >Charter</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row2_col1" class="data row2 col1" >962</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row2_col2" class="data row2 col2" >$585,858.00</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row2_col3" class="data row2 col3" >$609.00</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row2_col4" class="data row2 col4" >83.8399</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row2_col5" class="data row2 col5" >84.0447</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row2_col6" class="data row2 col6" >94.5946</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row2_col7" class="data row2 col7" >95.9459</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row2_col8" class="data row2 col8" >95.2703</td> 
    </tr>    <tr> 
        <th id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8level0_row3" class="row_heading level0 row3" >Griffin High School</th> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row3_col0" class="data row3 col0" >Charter</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row3_col1" class="data row3 col1" >1468</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row3_col2" class="data row3 col2" >$917,500.00</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row3_col3" class="data row3 col3" >$625.00</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row3_col4" class="data row3 col4" >83.3515</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row3_col5" class="data row3 col5" >83.8168</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row3_col6" class="data row3 col6" >93.3924</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row3_col7" class="data row3 col7" >97.139</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row3_col8" class="data row3 col8" >95.2657</td> 
    </tr>    <tr> 
        <th id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8level0_row4" class="row_heading level0 row4" >Wilson High School</th> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row4_col0" class="data row4 col0" >Charter</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row4_col1" class="data row4 col1" >2283</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row4_col2" class="data row4 col2" >$1,319,574.00</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row4_col3" class="data row4 col3" >$578.00</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row4_col4" class="data row4 col4" >83.2742</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row4_col5" class="data row4 col5" >83.9895</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row4_col6" class="data row4 col6" >93.8677</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row4_col7" class="data row4 col7" >96.5396</td> 
        <td id="T_6ed632c8_563e_11e8_a675_a8667f22f1d8row4_col8" class="data row4 col8" >95.2037</td> 
    </tr></tbody> 
</table> 



# Bottom Performing Schools (By Passing Rate)


```python
# Sorting the data frame to get the Bottom FIVE Performing Schools (By Passing Rate)
bottom_five_schools = school_summary_df.sort_values('Overall Passing Rate', ascending=True)
bottom_five_schools.head(5).style.format ({"Total School Budget" : "${:,.2f}",
                                "Per Student Budget" : "${:,.2f}"})
```




<style  type="text/css" >
</style>  
<table id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >School Type</th> 
        <th class="col_heading level0 col1" >Total Students</th> 
        <th class="col_heading level0 col2" >Total School Budget</th> 
        <th class="col_heading level0 col3" >Per Student Budget</th> 
        <th class="col_heading level0 col4" >Average Math Score</th> 
        <th class="col_heading level0 col5" >Average Reading Score</th> 
        <th class="col_heading level0 col6" >% Passing Math</th> 
        <th class="col_heading level0 col7" >% Passing Reading</th> 
        <th class="col_heading level0 col8" >Overall Passing Rate</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8level0_row0" class="row_heading level0 row0" >Rodriguez High School</th> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row0_col0" class="data row0 col0" >District</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row0_col1" class="data row0 col1" >3999</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row0_col2" class="data row0 col2" >$2,547,363.00</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row0_col3" class="data row0 col3" >$637.00</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row0_col4" class="data row0 col4" >76.8427</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row0_col5" class="data row0 col5" >80.7447</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row0_col6" class="data row0 col6" >66.3666</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row0_col7" class="data row0 col7" >80.2201</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row0_col8" class="data row0 col8" >73.2933</td> 
    </tr>    <tr> 
        <th id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8level0_row1" class="row_heading level0 row1" >Figueroa High School</th> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row1_col0" class="data row1 col0" >District</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row1_col1" class="data row1 col1" >2949</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row1_col2" class="data row1 col2" >$1,884,411.00</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row1_col3" class="data row1 col3" >$639.00</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row1_col4" class="data row1 col4" >76.7118</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row1_col5" class="data row1 col5" >81.158</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row1_col6" class="data row1 col6" >65.9885</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row1_col7" class="data row1 col7" >80.7392</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row1_col8" class="data row1 col8" >73.3639</td> 
    </tr>    <tr> 
        <th id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8level0_row2" class="row_heading level0 row2" >Huang High School</th> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row2_col0" class="data row2 col0" >District</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row2_col1" class="data row2 col1" >2917</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row2_col2" class="data row2 col2" >$1,910,635.00</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row2_col3" class="data row2 col3" >$655.00</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row2_col4" class="data row2 col4" >76.6294</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row2_col5" class="data row2 col5" >81.1827</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row2_col6" class="data row2 col6" >65.6839</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row2_col7" class="data row2 col7" >81.3164</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row2_col8" class="data row2 col8" >73.5002</td> 
    </tr>    <tr> 
        <th id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8level0_row3" class="row_heading level0 row3" >Johnson High School</th> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row3_col0" class="data row3 col0" >District</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row3_col1" class="data row3 col1" >4761</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row3_col2" class="data row3 col2" >$3,094,650.00</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row3_col3" class="data row3 col3" >$650.00</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row3_col4" class="data row3 col4" >77.0725</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row3_col5" class="data row3 col5" >80.9664</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row3_col6" class="data row3 col6" >66.0576</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row3_col7" class="data row3 col7" >81.2224</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row3_col8" class="data row3 col8" >73.64</td> 
    </tr>    <tr> 
        <th id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8level0_row4" class="row_heading level0 row4" >Ford High School</th> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row4_col0" class="data row4 col0" >District</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row4_col1" class="data row4 col1" >2739</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row4_col2" class="data row4 col2" >$1,763,916.00</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row4_col3" class="data row4 col3" >$644.00</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row4_col4" class="data row4 col4" >77.1026</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row4_col5" class="data row4 col5" >80.7463</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row4_col6" class="data row4 col6" >68.3096</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row4_col7" class="data row4 col7" >79.299</td> 
        <td id="T_6eda36ac_563e_11e8_ab95_a8667f22f1d8row4_col8" class="data row4 col8" >73.8043</td> 
    </tr></tbody> 
</table> 




```python
# Getting the Math Scores by Grade
math_nine = students.loc[students["grade"] == "9th"].groupby("school")["math_score"].mean()
math_ten = students.loc[students["grade"] == "10th"].groupby("school")["math_score"].mean()
math_eleven = students.loc[students["grade"] == "11th"].groupby("school")["math_score"].mean()
math_twelve = students.loc[students["grade"] == "12th"].groupby("school")["math_score"].mean()
```


```python
# Create a DataFrame with above information and set the index to School
math_score_grade = pd.DataFrame({"9th" : math_nine, "10th" : math_ten, "11th" : math_eleven,
                            "12th" : math_twelve})
math_score_grade = math_score_grade[["9th", "10th", "11th", "12th"]]
```

# Math Scores by Grade


```python
math_score_grade
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
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.083676</td>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.094697</td>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.403037</td>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.361345</td>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.044010</td>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.438495</td>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.787402</td>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>77.027251</td>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.187857</td>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.625455</td>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.859966</td>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.420755</td>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.590022</td>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.085578</td>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.264706</td>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Getting the reading Scores by Grade
read_nine = students.loc[students["grade"] == "9th"].groupby("school")["reading_score"].mean()
read_ten = students.loc[students["grade"] == "10th"].groupby("school")["reading_score"].mean()
read_eleven = students.loc[students["grade"] == "11th"].groupby("school")["reading_score"].mean()
read_twelve = students.loc[students["grade"] == "12th"].groupby("school")["reading_score"].mean()
```


```python
# Create a DataFrame with above information and set the index to School
read_score_grade = pd.DataFrame({"9th" : read_nine, "10th" : read_ten, "11th" : read_eleven,
                            "12th" : read_twelve})
read_score_grade = read_score_grade[["9th", "10th", "11th", "12th"]]
```

# Reading Scores by Grade


```python
read_score_grade
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
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>81.303155</td>
      <td>80.907183</td>
      <td>80.945643</td>
      <td>80.912451</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.676136</td>
      <td>84.253219</td>
      <td>83.788382</td>
      <td>84.287958</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.198598</td>
      <td>81.408912</td>
      <td>80.640339</td>
      <td>81.384863</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>80.632653</td>
      <td>81.262712</td>
      <td>80.403642</td>
      <td>80.662338</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.369193</td>
      <td>83.706897</td>
      <td>84.288089</td>
      <td>84.013699</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.866860</td>
      <td>80.660147</td>
      <td>81.396140</td>
      <td>80.857143</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.677165</td>
      <td>83.324561</td>
      <td>83.815534</td>
      <td>84.698795</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>81.290284</td>
      <td>81.512386</td>
      <td>81.417476</td>
      <td>80.305983</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>81.260714</td>
      <td>80.773431</td>
      <td>80.616027</td>
      <td>81.227564</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.807273</td>
      <td>83.612000</td>
      <td>84.335938</td>
      <td>84.591160</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>80.993127</td>
      <td>80.629808</td>
      <td>80.864811</td>
      <td>80.376426</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>84.122642</td>
      <td>83.441964</td>
      <td>84.373786</td>
      <td>82.781671</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.728850</td>
      <td>84.254157</td>
      <td>83.585542</td>
      <td>83.831361</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.939778</td>
      <td>84.021452</td>
      <td>83.764608</td>
      <td>84.317673</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.833333</td>
      <td>83.812757</td>
      <td>84.156322</td>
      <td>84.073171</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create the bins in which Data will be held
# Bins are (0 < x <= $585), ($585 < x <= $615), ($615 < x <= $645), ($645 < x <= $675)
bins = [0, 584.999, 614.999 , 644.999, 999999]
group_bin = ["< $585", "$585-$615", "$615-$645","$645-$675"]
merged_df['spending_ranges'] = pd.cut(merged_df['budget']/merged_df['size'], bins, labels = group_bin)
```


```python
# Grouping by Spending Bins
grp_by_spending = merged_df.groupby('spending_ranges')
```


```python
# Calculate: Average Math Score // Average Reading Score // % Passing Math // % Passing Reading // 
# Overall Passing Rate BY SCHOOL SPENDING
ave_math = grp_by_spending['math_score'].mean()
ave_reading = grp_by_spending['reading_score'].mean()
pass_math = merged_df[merged_df['math_score'] >= 70].groupby('spending_ranges')['Student ID'].count() / grp_by_spending['Student ID'].count()*100
pass_read = merged_df[merged_df['reading_score'] >= 70].groupby('spending_ranges')['Student ID'].count() / grp_by_spending['Student ID'].count()*100
overall = (pass_math + pass_read) / 2
```


```python
# Create the DataFrame to gatter the required information
score_by_spent = pd.DataFrame({
                            "Average Math Score": ave_math,
                            "Average Reading Score": ave_reading,
                            '% Passing Math': pass_math,
                            '% Passing Reading' : pass_read,
                            "Overall Passing Rate": overall
})
```


```python
# Re-Order the Data Frame to match the requested format
score_by_spent = score_by_spent[[
                            "Average Math Score",
                            "Average Reading Score",
                            '% Passing Math',
                            '% Passing Reading',
                            "Overall Passing Rate"
]]
```


```python
# Change the Index name to the one mentioned on the Example
score_by_spent.index.name = "Spending Ranges (Per Student)"
score_by_spent = score_by_spent.reindex(group_bin)
```

# Scores by School Spending


```python
score_by_spent
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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Spending Ranges (Per Student)</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt; $585</th>
      <td>83.363065</td>
      <td>83.964039</td>
      <td>93.702889</td>
      <td>96.686558</td>
      <td>95.194724</td>
    </tr>
    <tr>
      <th>$585-$615</th>
      <td>83.529196</td>
      <td>83.838414</td>
      <td>94.124128</td>
      <td>95.886889</td>
      <td>95.005509</td>
    </tr>
    <tr>
      <th>$615-$645</th>
      <td>78.061635</td>
      <td>81.434088</td>
      <td>71.400428</td>
      <td>83.614770</td>
      <td>77.507599</td>
    </tr>
    <tr>
      <th>$645-$675</th>
      <td>77.049297</td>
      <td>81.005604</td>
      <td>66.230813</td>
      <td>81.109397</td>
      <td>73.670105</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create the bins in which Data will be held
# Bins are (0 < x < 999.99), (1000 < x < 1999.99), (2000 < x < 5000)
bins = [0, 999, 1999, 999999]
group_bin = ["Small (<1000)", "Medium (1000-2000)", "Large (2000-5000)"]
merged_df['school_size'] = pd.cut(merged_df['size'], bins, labels = group_bin)
```


```python
# Group them by Spending again
grp_by_size = merged_df.groupby('school_size')
```


```python
# Calculate: Average Math Score // Average Reading Score // % Passing Math // % Passing Reading // 
# Overall Passing Rate BY SCHOOL SIZE
ave_math = grp_by_size['math_score'].mean()
ave_reading = grp_by_size['reading_score'].mean()
pass_math = merged_df[merged_df['math_score'] >= 70].groupby('school_size')['Student ID'].count() / grp_by_size['Student ID'].count()*100
pass_read = merged_df[merged_df['reading_score'] >= 70].groupby('school_size')['Student ID'].count() / grp_by_size['Student ID'].count()*100
overall = (pass_math + pass_read) / 2
```


```python
# Create the DataFrame to gatter the required information
score_by_size = pd.DataFrame({
                            "Average Math Score": ave_math,
                            "Average Reading Score": ave_reading,
                            '% Passing Math': pass_math,
                            '% Passing Reading' : pass_read,
                            "Overall Passing Rate": overall
})
```


```python
# Re-Order the Data Frame to match the requested format
score_by_size = score_by_size[[
                            "Average Math Score",
                            "Average Reading Score",
                            '% Passing Math',
                            '% Passing Reading',
                            "Overall Passing Rate"
]]
```


```python
# Change the Index name to the one mentioned on the Example
score_by_size.index.name = "School Size"
score_by_size = score_by_size.reindex(group_bin)
```

# Scores by School Size


```python
score_by_size
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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Size</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small (&lt;1000)</th>
      <td>83.828654</td>
      <td>83.974082</td>
      <td>93.952484</td>
      <td>96.040317</td>
      <td>94.996400</td>
    </tr>
    <tr>
      <th>Medium (1000-2000)</th>
      <td>83.372682</td>
      <td>83.867989</td>
      <td>93.616522</td>
      <td>96.773058</td>
      <td>95.194790</td>
    </tr>
    <tr>
      <th>Large (2000-5000)</th>
      <td>77.477597</td>
      <td>81.198674</td>
      <td>68.652380</td>
      <td>82.125158</td>
      <td>75.388769</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Repeat the breakdown, but group the schools based on school type (Charter vs. District)
# Now group by Type
grp_by_type = merged_df.groupby("type")
```


```python
# Make the calcualtions but based on type
ave_math = grp_by_type['math_score'].mean()
ave_reading = grp_by_type['reading_score'].mean()
pass_math = merged_df[merged_df['math_score'] >= 70].groupby('type')['Student ID'].count() / grp_by_type['Student ID'].count()*100
pass_read = merged_df[merged_df['reading_score'] >= 70].groupby('type')['Student ID'].count() / grp_by_type['Student ID'].count()*100
overall = (pass_math + pass_read) / 2
```


```python
# Create the DataFrame to gatter the required information
score_by_type = pd.DataFrame({
                            "Average Math Score": ave_math,
                            "Average Reading Score": ave_reading,
                            '% Passing Math': pass_math,
                            '% Passing Reading' : pass_read,
                            "Overall Passing Rate": overall
})
```


```python
# Re-Order the Data Frame to match the requested format
score_by_type = score_by_type[[
                            "Average Math Score",
                            "Average Reading Score",
                            '% Passing Math',
                            '% Passing Reading',
                            "Overall Passing Rate"
]]
```


```python
# Change the Index name to the one mentioned on the Example
score_by_type.index.name = "School Type"
```

# Scores by School Type


```python
score_by_type
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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.406183</td>
      <td>83.902821</td>
      <td>93.701821</td>
      <td>96.645891</td>
      <td>95.173856</td>
    </tr>
    <tr>
      <th>District</th>
      <td>76.987026</td>
      <td>80.962485</td>
      <td>66.518387</td>
      <td>80.905249</td>
      <td>73.711818</td>
    </tr>
  </tbody>
</table>
</div>



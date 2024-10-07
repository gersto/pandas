
### Task01

```python
import pandas as pd
temperatures = pd.Series([20, 22, 25, 23, 21, 19, 24], 
                         index=['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'])
```

You are given a Series of daily temperatures for a week.

Calculate and print the following
- The temperature increase if each day was 2 degrees warmer
- The weekly average temperature
- The difference between each day's temperature and the weekly average


### Task02

```python
import pandas as pd
grades = pd.Series([65, 92, 68, 72, 84], index=['Alice', 'Bob', 'Charlie', 'David', 'Eva'])
```

Let us solve a practice problem that combines your knowledge of Pandas series and Python.

You are given a Pandas series in the IDE. You need to modify the Series based on certain conditions.

Using the gradebook Series:
- Add 10 points all scores and output the series
- Cap the maximum score at 100 and output the series
- Create a new Pandas series - 'grade_summary' - which summarises the count of students in different score ranges.

### Task03

```python
import pandas as pd
import numpy as np

# Create the initial DataFrame
data = {
    'Student ID': range(1, 11),
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve', 'Frank', 'Grace', 'Henry', 'Ivy', 'Jack'],
    'Age': [18, 19, 18, 20, 19, 18, 20, 19, 18, 20],
    'Math Score': [85, 76, 90, 88, 92, 78, 95, 82, 89, 91],
    'Science Score': [88, 82, 85, 90, 86, 80, 92, 78, 94, 89],
    'English Score': [92, 78, 88, 85, 90, 86, 94, 80, 91, 87]
}

df = pd.DataFrame(data)
```

We have given you a dataset containing information on student performance.

DataFrame Creation and Basic Viewing
- Create a new DataFrame containing only students aged 19 or older.
- Display the first 3 rows and basic information about this new DataFrame.


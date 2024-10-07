
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

We have given you a dataset containing information on student performance.

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

#### Part1
DataFrame Creation and Basic Viewing
- Create a new DataFrame containing only students aged 19 or older.
- Display the first 3 rows and basic information about this new DataFrame.

#### Part2
Perform the following operations - remember - after each operation, output the new DataFrame to the console
- Add a new column - 'Total_score'. This column should contain the total score of any student across all 3 tests.
- Display the 'Name' and 'Total_score' columns for students with an total score greater than 240.

#### Part3
Task
- Use iloc to output the DataFrame corresponding to the 3rd, 4th row and the 2nd, 3rd column
- Use loc to select and output the Math and Science scores for students David, Frank and Henry

#### Part4
Task
- Create a new column 'Performance' with values 'Excellent' for total score > 270, 'Good' for total score > 240, and 'Average' for the rest.
- Use boolean indexing to display all information about students who performed 'Excellent' in Math (score > 90).

#### Part5
Task
- Calculate and display the average score for each subject.
- Remove the 'Age' column and display the first 5 rows of the resulting DataFrame.

### Task04

```python
import pandas as pd

# Create the DataFrame
df = pd.DataFrame({
    'Title': ['Book A', 'Book B', 'Book C', 'Book D', 'Book E'],
    'Author': ['Author 1', 'Author 2', 'Author 3', 'Author 1', 'Author 2'],
    'Year': [2020, 2019, 2020, 2018, 2019],
    'Sales': [5000, 6000, 4500, 3000, 7000]
})
```

You have a DataFrame df with information about books, including 'Title', 'Author', 'Year', and 'Sales'.

Perform the following operations and output the result to the console:
- Sort the books by 'Year' in descending order (newest first). For books published in the same year, sort them by 'Sales' in descending order.
- Rename the column 'Title' as 'Book_name'

### Task05

# School District Analysis
Michelle Curran
Python Module 4 Challenge

## Project Overview
A school board has found evidence of academic dishonesty in the reading and math grades for Thomas High School ninth graders and uphold state-testing standards by replacing these grades with NaNs.

Then, a school district analysis was performed to determine the effect of replacing ninth-grade reading and math scores for Thomas High School on the overall analysis results, through performing a data analysis from all grades, and then performing a second analysis from all grades except for the reading and math grades for Thomas High School ninth graders. 

## Resources
- Data source: students_complete.csv, schools_complete.csv
- Software: Python 3.10.1, Visual Studio Code 1.63.2

## Challenge Overview - Overview of School District Analysis
! The purpose of this analysis is well defined 
The purpose of the school district analysis is to examine how excluding Thomas High School ninth-grade math and reading grades from the school district analysis changed the intial school district analysis that included these academically dishonest grades.
  * The analysis was performed through the following deliverables:
1. Replace ninth-grade reading and math scores
2. Repeat the school district analysis
4. A written report for the school district analysis (README.md)

## School District Analysis Results
! There is a bulleted list that addresses how each of the seven school district metrics was affected by the changes in the data 
- The school district metric of x caused y by changing the data z.
- The school district metric of x caused y by changing the data z.
- The school district metric of x caused y by changing the data z.
- The school district metric of x caused y by changing the data z.
- The school district metric of x caused y by changing the data z.
- The school district metric of x caused y by changing the data z.
- The school district metric of x caused y by changing the data z.

### Code
Code reference for School District Analysis Summary section below and the School District Analysis Results above.
```
# Dependencies and Setup
import pandas as pd

# File to Load (Remember to change the path if needed.)
school_data_to_load = "Resources/schools_complete.csv"
student_data_to_load = "Resources/students_complete.csv"

# Read the School Data and Student Data and store into a Pandas DataFrame
school_data_df = pd.read_csv(school_data_to_load)
student_data_df = pd.read_csv(student_data_to_load)

```

## Challenge Summary - School District Analysis Summary
In order to use the script for any school district, must modify the script as seen above as follows:
- Change school_data_to_load to a different path that leads to a different csv file. 
    - ```school_data_to_load = "Resources/schools_complete.csv"```
- Change student_data_to_load  to a different path that leads to a different txt file. 
    - ```student_data_to_load = "Resources/students_complete.csv"```
    
    

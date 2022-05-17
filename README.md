# School_District_Analysis
Michelle Curran
Python Module 4 Challenge

## Project Overview
A school board has found evidence of academic dishonesty in the reading and math grades for Thomas High School ninth graders and uphold state-testing standards by replacing these grades with NaNs.

Then, a school district analysis was performed to:
- x,
- y, 
- and provide results showing how the effect of replacement of grades on the overall analysis.

## Resources
- Data source: students_complete.csv, schools_complete.csv
- Software: Python 3.10.1, Visual Studio Code 1.63.2

## Challenge Overview - Overview of School District Analysis
! The purpose of this analysis is well defined 
The xyz:
  * The

Deliverables are as follows:
1. Replace ninth-grade reading and math scores
2. Repeat the school district analysis
3. A written report for the school district analysis (README.md)

## School District Analysis Results
! There is a bulleted list that addresses how each of the seven school district metrics was affected by the changes in the data 

- The 

### Code
Code reference for School District Analysis Summary section below.
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
    
Therefore, as long as you have a csv file with the data to be analyzed, and a txt file to write or output the results to, then any election can be analyzed using this script.
There is a statement summarizing four changes to the school district analysis after reading and math scores have been replaced 
First, the replacement ... The school district analysis showed:
- 


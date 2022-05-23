# School District Analysis
Python Module 4 Challenge

## Project Overview
A school board has found evidence of academic dishonesty in the reading and math grades for Thomas High School ninth graders and uphold state-testing standards by replacing these grades with NaNs.

A school district analysis was performed to determine the effect of replacing ninth-grade reading and math scores for Thomas High School on the overall analysis results, through performing a data analysis from all grades, and then performing a second analysis from all grades except for the reading and math grades for Thomas High School ninth graders. 

## Resources
- Data source: students_complete.csv, schools_complete.csv
- Software: Python 3.10.1, Visual Studio Code 1.63.2

## Challenge Overview - Overview of School District Analysis
The purpose of the school district analysis is to examine how excluding Thomas High School ninth-grade students' math and reading grades from the school district analysis changes the prior analysis with academically dishonest grades.
  * The analysis was performed through the following deliverables:
1. Replace ninth-grade reading and math scores
2. Repeat the school district analysis:
 - a. Dataframe of all schools' student's ID, name, gender, grade, school name,reading score, math score, and type (district/charter), size and budget of student's school. 
 - b. First dataframe calculated the totals of all 15 school's number of students, budget, average math and reading scores, as well as the percentages of all the students passing math, reading, and both in the schools. The second dataframe contained the data of each of the 15 school's total number of schools, students, budget, average math and reading scores, as well as the percentages of students passing math, reading, and both.
 - c. Create dataframe of 10th through 12th graders passing math and reading at Thomas High School.
 - d. Edit existing dataframe containing the summary of each school's data by replacing the passing percentages for Thomas High School, updating the numbers that have changed due to removing the ninth-grade scores.
 - e. Calculate the top and bottom 5 performances from schools based on the percentage of students passing overall.
 - f. Two dataframes were created to show math and reading scores by grade. 
 - g. Created dataframe to analyze scores and spending per student by school and then by scores.
 - h. Created dataframe to analyze scores and school sizes.
 - i. Created dataframe to analyze scores and school types.
3. A written report for the school district analysis (README.md)


## School District Analysis Results
! There is a bulleted list that addresses how each of the seven school district metrics was affected by the changes in the data 
The school district metrics of x1, .., x7 were affected by changes in the data in the following ways:

By excluding ninth grade student's math and reading scores from data, the number of students dropped from x to y, the average math and reading scores dropped by z respectively, reflecting the change in math and reading scores to . The math and reading scores by grade changes. The overall passing percentage changed from x to y. 
The top 5 schools were x and the bottom 5 schools were z. After replacing ninth grade scores, the top 5 schools were x and the bottom 5 schools were z. The spending per student and per school changes : xyz. The spending relating to scores changes : xyz. 

### Code
Code reference for School District Analysis Summary section below and the School District Analysis Results above.
```
# Python Module 4 Challenge
# Michelle Curran

# Dependencies and Setup
import pandas as pd

# File to Load (Remember to change the path if needed.)
school_data_to_load = "Resources/schools_complete.csv"
student_data_to_load = "Resources/students_complete.csv"

# Read the School Data and Student Data and store into a Pandas DataFrame
school_data_df = pd.read_csv(school_data_to_load)
student_data_df = pd.read_csv(student_data_to_load)

# Cleaning Student Names and Replacing Substrings in a Python String
# Add each prefix and suffix to remove to a list.
prefixes_suffixes = ["Dr. ", "Mr. ","Ms. ",
 "Mrs. ", "Miss ", " MD", " DDS", " DVM", " PhD"]

# Iterate through the words in the "prefixes_suffixes" list and replace them with an empty space, "".
for word in prefixes_suffixes:
    student_data_df["student_name"] = student_data_df["student_name"].str.replace(word,"")

# Check names.
student_data_df.head(10)
## Deliverable 1: Replace the reading and math scores.

### Replace the 9th grade reading and math scores at Thomas High School with NaN.
# Install numpy using conda install numpy or pip install numpy. 
# Step 1. Import numpy as np.
import numpy as np
student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th")]
# Step 2. Use the loc method on the student_data_df to select all the reading scores from the 9th grade at Thomas High School and replace them with NaN.
student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th"),["reading_score"]]=np.nan
#  Step 3. Refactor the code in Step 2 to replace the math scores with NaN
student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th"),["math_score"]]=np.nan
student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th")]
student_data_df.tail(10)
## Deliverable 2 : Repeat the school district analysis
### District Summary
# Combine the data into a single dataset
school_data_complete_df = pd.merge(student_data_df, school_data_df, how="left", on=["school_name", "school_name"])
school_data_complete_df.head()
school_data_complete_df
# Calculate the Totals (Schools and Students)
school_count = len(school_data_complete_df["school_name"].unique())
student_count = school_data_complete_df["student_name"].count()

# Calculate the Total Budget
total_budget = school_data_df["budget"].sum()
student_count
# Calculate the Average Scores using the "clean_student_data".
average_reading_score = school_data_complete_df["reading_score"].mean()
average_math_score = school_data_complete_df["math_score"].mean()
# Step 1. Get the number of students that are in ninth grade at Thomas High School.
# These students have no grades. 
# Create a grade level DataFrames.
ninth_graders = school_data_complete_df[(school_data_complete_df["grade"] == "9th")]
ninth_graders_ths = ninth_graders[(ninth_graders["school_name"] == "Thomas High School")]
ninth_graders_ths_count = ninth_graders_ths["school_name"].count()
ninth_graders_ths_count
# Get the total student count 
student_count
# Step 2. Subtract the number of students that are in ninth grade at 
# Thomas High School from the total student count to get the new total student count.
new_student_count = student_count - ninth_graders_ths_count
new_student_count
# Calculate the passing rates using the "clean_student_data".
passing_math_count = school_data_complete_df[(school_data_complete_df["math_score"] >= 70)].count()["student_name"]
passing_reading_count = school_data_complete_df[(school_data_complete_df["reading_score"] >= 70)].count()["student_name"]
passing_math_count
# Step 3. Calculate the passing percentages with the new total student count.
new_passing_math_percentage = passing_math_count/new_student_count.astype(float) * 100
new_passing_reading_percentage = passing_reading_count/new_student_count.astype(float) * 100
new_passing_math_percentage
new_passing_reading_percentage
# Calculate the students who passed both reading and math.
passing_math_reading = school_data_complete_df[(school_data_complete_df["math_score"] >= 70)
                                               & (school_data_complete_df["reading_score"] >= 70)]

# Calculate the number of students that passed both reading and math.
overall_passing_math_reading_count = passing_math_reading["student_name"].count()

# Step 4.Calculate the overall passing percentage with new total student count.
new_overall_passing_percentage = overall_passing_math_reading_count / new_student_count.astype(float) * 100
average_reading_score
# Create a DataFrame
district_summary_df = pd.DataFrame(
          [{"Total Schools": school_count, 
          "Total Students": student_count, 
          "Total Budget": total_budget,
          "Average Math Score": average_math_score, 
          "Average Reading Score": average_reading_score,
          "% Passing Math": new_passing_math_percentage,
         "% Passing Reading": new_passing_reading_percentage,
        "% Overall Passing": new_overall_passing_percentage}])

# Format the "Total Students" to have the comma for a thousands separator.
district_summary_df["Total Students"] = district_summary_df["Total Students"].map("{:,}".format)
# Format the "Total Budget" to have the comma for a thousands separator, a decimal separator and a "$".
district_summary_df["Total Budget"] = district_summary_df["Total Budget"].map("${:,.2f}".format)
# Format the columns.
district_summary_df["Average Math Score"] = district_summary_df["Average Math Score"].map("{:.1f}".format)
district_summary_df["Average Reading Score"] = district_summary_df["Average Reading Score"].map("{:.1f}".format)
district_summary_df["% Passing Math"] = district_summary_df["% Passing Math"].map("{:.1f}".format)
district_summary_df["% Passing Reading"] = district_summary_df["% Passing Reading"].map("{:.1f}".format)
district_summary_df["% Overall Passing"] = district_summary_df["% Overall Passing"].map("{:.1f}".format)
# Display the dataframe.
district_summary_df
##  School Summary
# Determine the School Type
per_school_types = school_data_df.set_index(["school_name"])["type"]

# Calculate the total student count.
per_school_counts = school_data_df.set_index(["school_name"])["size"]

# Calculate the total school budget and per capita spending
per_school_budget = school_data_complete_df.groupby(["school_name"]).mean()["budget"]
# Calculate the per capita spending.
per_school_capita = per_school_budget / per_school_counts

# Calculate the average test scores.
per_school_math = school_data_complete_df.groupby(["school_name"]).mean()["math_score"]
per_school_reading = school_data_complete_df.groupby(["school_name"]).mean()["reading_score"]

# Calculate the passing scores by creating a filtered DataFrame.
per_school_passing_math = school_data_complete_df[(school_data_complete_df["math_score"] >= 70)]
per_school_passing_reading = school_data_complete_df[(school_data_complete_df["reading_score"] >= 70)]

# Calculate the number of students passing math and passing reading by school.
per_school_passing_math = per_school_passing_math.groupby(["school_name"]).count()["student_name"]
per_school_passing_reading = per_school_passing_reading.groupby(["school_name"]).count()["student_name"]

# Calculate the percentage of passing math and reading scores per school.
per_school_passing_math = per_school_passing_math / per_school_counts * 100
per_school_passing_reading = per_school_passing_reading / per_school_counts * 100

# Calculate the students who passed both reading and math.
per_passing_math_reading = school_data_complete_df[(school_data_complete_df["reading_score"] >= 70)
                                               & (school_data_complete_df["math_score"] >= 70)]

# Calculate the number of students passing math and passing reading by school.
per_passing_math_reading = per_passing_math_reading.groupby(["school_name"]).count()["student_name"]

# Calculate the percentage of passing math and reading scores per school.
per_overall_passing_percentage = per_passing_math_reading / per_school_counts * 100
# Create the DataFrame
per_school_summary_df = pd.DataFrame({
    "School Type": per_school_types,
    "Total Students": per_school_counts,
    "Total School Budget": per_school_budget,
    "Per Student Budget": per_school_capita,
    "Average Math Score": per_school_math,
    "Average Reading Score": per_school_reading,
    "% Passing Math": per_school_passing_math,
    "% Passing Reading": per_school_passing_reading,
    "% Overall Passing": per_overall_passing_percentage})

# per_school_summary_df.head()
# Format the Total School Budget and the Per Student Budget
per_school_summary_df["Total School Budget"] = per_school_summary_df["Total School Budget"].map("${:,.2f}".format)
per_school_summary_df["Per Student Budget"] = per_school_summary_df["Per Student Budget"].map("${:,.2f}".format)

# Display the data frame
per_school_summary_df
# Step 5.  Get the number of 10th-12th graders from Thomas High School (THS).
tenth_graders = student_data_df.loc[(student_data_df["grade"] == "10th") & (student_data_df["school_name"] == "Thomas High School")]
tenth_graders_count = tenth_graders["school_name"].count()

eleventh_graders = student_data_df.loc[(student_data_df["grade"] == "11th") & (student_data_df["school_name"] == "Thomas High School")]
eleventh_graders_count = eleventh_graders["school_name"].count()

twelfth_graders = student_data_df.loc[(student_data_df["grade"] == "12th") & (student_data_df["school_name"] == "Thomas High School")]
twelfth_graders_count = twelfth_graders["school_name"].count()

total_tenth_thru_twelfth_count = tenth_graders_count + eleventh_graders_count + twelfth_graders_count
total_tenth_thru_twelfth_count
# Step 6. Get all the students passing math from THS (excluding ninth graders who do not have scores anymore)
tenth_thru_twelfth_graders_passing_math_df = student_data_df.loc[(student_data_df["grade"] != "9th") & (student_data_df["school_name"] == "Thomas High School") & (student_data_df["math_score"] >= 70)]
tenth_thru_twelfth_graders_passing_math_df
# Step 7. Get all the students passing reading from THS
tenth_thru_twelfth_graders_passing_reading_df = student_data_df.loc[(student_data_df["grade"] != "9th") & (student_data_df["school_name"] == "Thomas High School") & (student_data_df["reading_score"] >= 70)]
tenth_thru_twelfth_graders_passing_reading_df
# Step 8. Get all the students passing math and reading from THS
tenth_thru_twelfth_graders_passing_math_reading_df = student_data_df.loc[(student_data_df["grade"] != "9th") & (student_data_df["school_name"] == "Thomas High School") & (student_data_df["math_score"] >= 70) & (student_data_df["reading_score"] >= 70)]
tenth_thru_twelfth_graders_passing_math_reading_df
# Step 9. Calculate the percentage of 10th-12th grade students passing math from Thomas High School. 
tenth_thru_twelfth_graders_passing_math_count = tenth_thru_twelfth_graders_passing_math_df["Student ID"].count()
tenth_thru_twelfth_graders_passing_math_percentage = tenth_thru_twelfth_graders_passing_math_count/total_tenth_thru_twelfth_count*100
tenth_thru_twelfth_graders_passing_math_percentage
# Step 10. Calculate the percentage of 10th-12th grade students passing reading from Thomas High School.
tenth_thru_twelfth_graders_passing_reading_count = tenth_thru_twelfth_graders_passing_reading_df["Student ID"].count()
tenth_thru_twelfth_graders_passing_reading_percentage = tenth_thru_twelfth_graders_passing_reading_count/total_tenth_thru_twelfth_count*100
tenth_thru_twelfth_graders_passing_reading_percentage
# Step 11. Calculate the overall passing percentage of 10th-12th grade from Thomas High School. 
overall_passing_count = tenth_thru_twelfth_graders_passing_math_reading_df["Student ID"].count()
overrall_passing_percentage = overall_passing_count/total_tenth_thru_twelfth_count*100
overrall_passing_percentage

# Step 12. Replace the passing math percent for Thomas High School in the per_school_summary_df.
# Thomas High School is 12th index, or 13th row, of the per school summary data frame
per_school_summary_df["% Passing Math"] = per_school_summary_df["% Passing Math"].replace(per_school_passing_math[12],tenth_thru_twelfth_graders_passing_math_percentage)
per_school_summary_df
# Step 13. Replace the passing reading percentage for Thomas High School in the per_school_summary_df.
per_school_summary_df["% Passing Reading"] = per_school_summary_df["% Passing Reading"].replace(per_school_passing_reading[12],tenth_thru_twelfth_graders_passing_reading_percentage)
# Step 14. Replace the overall passing percentage for Thomas High School in the per_school_summary_df.
per_school_summary_df["% Overall Passing"] = per_school_summary_df["% Overall Passing"].replace(per_overall_passing_percentage[12],overrall_passing_percentage)
per_school_summary_df
## High and Low Performing Schools 
# Sort and show top five schools.
top_schools = per_school_summary_df.sort_values(["% Overall Passing"], ascending=False)

top_schools.head()
# Sort and show bottom five schools.
bottom_schools = per_school_summary_df.sort_values(["% Overall Passing"], ascending=True)

bottom_schools.head()
## Math and Reading Scores by Grade
# Create a Series of scores by grade levels using conditionals
ninth_graders = student_data_df[(student_data_df["grade"] == "9th")]

tenth_graders = student_data_df[(student_data_df["grade"] == "10th")]

eleventh_graders = student_data_df[(student_data_df["grade"] == "11th")]

twelfth_graders = student_data_df[(student_data_df["grade"] == "12th")]

# Group each school Series by the school name for the average math score.
ninth_grade_math_scores = ninth_graders.groupby(["school_name"]).mean()["math_score"]

tenth_grade_math_scores = tenth_graders.groupby(["school_name"]).mean()["math_score"]

eleventh_grade_math_scores = eleventh_graders.groupby(["school_name"]).mean()["math_score"]

twelfth_grade_math_scores = twelfth_graders.groupby(["school_name"]).mean()["math_score"]

# Group each school Series by the school name for the average reading score.
ninth_grade_reading_scores = ninth_graders.groupby(["school_name"]).mean()["reading_score"]

tenth_grade_reading_scores = tenth_graders.groupby(["school_name"]).mean()["reading_score"]

eleventh_grade_reading_scores = eleventh_graders.groupby(["school_name"]).mean()["reading_score"]

twelfth_grade_reading_scores = twelfth_graders.groupby(["school_name"]).mean()["reading_score"]
# Combine each Series for average math scores by school into single data frame.
math_scores_by_grade = pd.DataFrame({
               "9th": ninth_grade_math_scores,
               "10th": tenth_grade_math_scores,
               "11th": eleventh_grade_math_scores,
               "12th": twelfth_grade_math_scores})

math_scores_by_grade.head()
# Combine each Series for average reading scores by school into single data frame.
reading_scores_by_grade = pd.DataFrame({
              "9th": ninth_grade_reading_scores,
              "10th": tenth_grade_reading_scores,
              "11th": eleventh_grade_reading_scores,
              "12th": twelfth_grade_reading_scores})

reading_scores_by_grade.head()
# Format each grade column.
reading_scores_by_grade["9th"] = reading_scores_by_grade["9th"].map("{:.1f}".format)

reading_scores_by_grade["10th"] = reading_scores_by_grade["10th"].map("{:.1f}".format)

reading_scores_by_grade["11th"] = reading_scores_by_grade["11th"].map("{:.1f}".format)

reading_scores_by_grade["12th"] = reading_scores_by_grade["12th"].map("{:.1f}".format)

# Make sure the columns are in the correct order.
reading_scores_by_grade = reading_scores_by_grade[
                 ["9th", "10th", "11th", "12th"]]
# Format each grade column.
math_scores_by_grade["9th"] = math_scores_by_grade["9th"].map("{:.1f}".format)

math_scores_by_grade["10th"] = math_scores_by_grade["10th"].map("{:.1f}".format)

math_scores_by_grade["11th"] = math_scores_by_grade["11th"].map("{:.1f}".format)

math_scores_by_grade["12th"] = math_scores_by_grade["12th"].map("{:.1f}".format)

# Make sure the columns are in the correct order.
math_scores_by_grade = math_scores_by_grade[
                 ["9th", "10th", "11th", "12th"]]
# Remove the index.
math_scores_by_grade.index.name = None

# Display the data frame
math_scores_by_grade.head()
## Remove the index.
math_scores_by_grade.index.name = None

# Display the data frame
math_scores_by_grade.head()
math_scores_by_grade
reading_scores_by_grade
## Scores by School Spending
# Establish the spending bins and group names.
per_school_capita.describe()
spending_bins = [0, 585, 630, 645, 675]
group_names = ["<$586", "$586-630", "$631-645", "$646-675"]
per_school_capita.groupby(pd.cut(per_school_capita, spending_bins)).count()

# Categorize spending based on the bins.
per_school_summary_df["Spending Ranges (Per Student)"] = pd.cut(per_school_capita, spending_bins, labels=group_names)
per_school_summary_df
# Calculate averages for the desired columns. 
spending_math_scores = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["Average Math Score"]

spending_reading_scores = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["Average Reading Score"]

spending_passing_math = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["% Passing Math"]

spending_passing_reading = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["% Passing Reading"]

overall_passing_spending = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["% Overall Passing"]
# Create the DataFrame
spending_summary_df = pd.DataFrame({
          "Average Math Score" : spending_math_scores,
          "Average Reading Score": spending_reading_scores,
          "% Passing Math": spending_passing_math,
          "% Passing Reading": spending_passing_reading,
          "% Overall Passing": overall_passing_spending})

spending_summary_df
# Format the DataFrame 
spending_summary_df["Average Math Score"] = spending_summary_df["Average Math Score"].map("{:.1f}".format)

spending_summary_df["Average Reading Score"] = spending_summary_df["Average Reading Score"].map("{:.1f}".format)

spending_summary_df["% Passing Math"] = spending_summary_df["% Passing Math"].map("{:.0f}".format)

spending_summary_df["% Passing Reading"] = spending_summary_df["% Passing Reading"].map("{:.0f}".format)

spending_summary_df["% Overall Passing"] = spending_summary_df["% Overall Passing"].map("{:.0f}".format)

spending_summary_df
## Scores by School Size
# Establish the bins.
per_school_counts
size_bins = [0, 999, 1999, 5000]
group_names = ["Small (<1000)", "Medium (1000-1999)", "Large (2000-5000)"]

# Categorize spending based on the bins.
per_school_summary_df["School Size"] = pd.cut(per_school_summary_df["Total Students"], size_bins, labels=group_names)
per_school_summary_df.head()
# Calculate averages for the desired columns. 
size_math_scores = per_school_summary_df.groupby(["School Size"]).mean()["Average Math Score"]

size_reading_scores = per_school_summary_df.groupby(["School Size"]).mean()["Average Reading Score"]

size_passing_math = per_school_summary_df.groupby(["School Size"]).mean()["% Passing Math"]

size_passing_reading = per_school_summary_df.groupby(["School Size"]).mean()["% Passing Reading"]

size_overall_passing = per_school_summary_df.groupby(["School Size"]).mean()["% Overall Passing"]
# Assemble into DataFrame. 
size_summary_df = pd.DataFrame({
          "Average Math Score" : size_math_scores,
          "Average Reading Score": size_reading_scores,
          "% Passing Math": size_passing_math,
          "% Passing Reading": size_passing_reading,
          "% Overall Passing": size_overall_passing})

size_summary_df
# Format the DataFrame  
size_summary_df["Average Math Score"] = size_summary_df["Average Math Score"].map("{:.1f}".format)

size_summary_df["Average Reading Score"] = size_summary_df["Average Reading Score"].map("{:.1f}".format)

size_summary_df["% Passing Math"] = size_summary_df["% Passing Math"].map("{:.0f}".format)

size_summary_df["% Passing Reading"] = size_summary_df["% Passing Reading"].map("{:.0f}".format)

size_summary_df["% Overall Passing"] = size_summary_df["% Overall Passing"].map("{:.0f}".format)

size_summary_df
## Scores by School Type
# Calculate averages for the desired columns. 
type_math_scores = per_school_summary_df.groupby(["School Type"]).mean()["Average Math Score"]

type_reading_scores = per_school_summary_df.groupby(["School Type"]).mean()["Average Reading Score"]

type_passing_math = per_school_summary_df.groupby(["School Type"]).mean()["% Passing Math"]

type_passing_reading = per_school_summary_df.groupby(["School Type"]).mean()["% Passing Reading"]

type_overall_passing = per_school_summary_df.groupby(["School Type"]).mean()["% Overall Passing"]
# Assemble into DataFrame. 
type_summary_df = pd.DataFrame({
          "Average Math Score" : type_math_scores,
          "Average Reading Score": type_reading_scores,
          "% Passing Math": type_passing_math,
          "% Passing Reading": type_passing_reading,
          "% Overall Passing": type_overall_passing})

type_summary_df
# # Format the DataFrame 
type_summary_df["Average Math Score"] = type_summary_df["Average Math Score"].map("{:.1f}".format)

type_summary_df["Average Reading Score"] = type_summary_df["Average Reading Score"].map("{:.1f}".format)

type_summary_df["% Passing Math"] = type_summary_df["% Passing Math"].map("{:.0f}".format)

type_summary_df["% Passing Reading"] = type_summary_df["% Passing Reading"].map("{:.0f}".format)

type_summary_df["% Overall Passing"] = type_summary_df["% Overall Passing"].map("{:.0f}".format)

type_summary_df
```

## Challenge Summary - School District Analysis Summary
In order to use the script for any school district, must modify the script as seen above as follows:
- Change school_data_to_load to a different path that leads to a different csv file. 
    - ```school_data_to_load = "Resources/schools_complete.csv"```
- Change student_data_to_load  to a different path that leads to a different txt file. 
    - ```student_data_to_load = "Resources/students_complete.csv"```
    
    

```

## Challenge Summary - School District Analysis Summary
In order to use the script for any school district, must modify the script as seen above as follows:
- Change school_data_to_load to a different path that leads to a different csv file. 
    - ```school_data_to_load = "Resources/schools_complete.csv"```
- Change student_data_to_load  to a different path that leads to a different txt file. 
    - ```student_data_to_load = "Resources/students_complete.csv"```
    
    

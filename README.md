# School Performance Analysis with Pandas

![image](https://user-images.githubusercontent.com/112406455/210904891-7c74c3e9-fe27-491c-b019-5276e1887814.png)

## Background
As the new Chief Data Scientist for the city's school district, I am tasked with analyzing district-wide standardized test results to aid strategic decision-making regarding school budgets and priorities. Utilizing Pandas and Jupyter Notebook, my assignment is to create detailed reports based on every student's math and reading scores, along with school information. The objective is to aggregate this data effectively to reveal clear trends in school performance. This analysis will help in creating a comprehensive snapshot of the district's educational landscape, encompassing various key metrics like average scores, passing percentages, and budget allocations. The insights gained will be pivotal in guiding the school board and mayor's decisions, ensuring resource allocation aligns with the areas of greatest need and impact.
## Objective
The primary goal of this project is to utilize advanced data manipulation techniques with Pandas and Jupyter Notebook to conduct a thorough analysis of standardized test results across the school district. The key objectives are outlined as follows:
1. **District Summary**: To compute and present a high-level snapshot of the district's key educational metrics, including the total number of schools, students, overall budget, average scores, and percentages of students passing math, reading, and both subjects.
2. **School Summary**: To create a detailed report for each school, covering metrics such as school type, total students, budget allocations, average scores, and passing rates. This will provide a clear understanding of each school's performance within the district.
3. **Performance Analysis by Various Criteria**:
	* **Highest-Performing Schools**: Identify and list the top schools based on overall passing rates.
	* **Lowest-Performing Schools**: Determine schools that need the most attention and improvement.
	* **Math and Reading Scores by Grade**: Analyze average scores in math and reading across different grade levels for each school.
	* **Scores by School Spending**: Examine how school performance correlates with spending per student.
	* **Scores by School Size**: Assess how school size impacts student performance.
	* **Scores by School Type**: Investigate performance trends based on the type of school (Charter vs. District).
4. **Data-Driven Decision Making**: The ultimate aim is to provide the school board and mayor with actionable insights derived from the data. This involves identifying trends and patterns that can inform strategic decisions on resource allocation, policy-making, and prioritizing initiatives for the overall enhancement of the district's educational standards.

This comprehensive analysis is intended not only to reflect the current state of the school district but also to highlight areas for potential growth and improvement, ensuring that every decision made contributes positively to the educational journey of each student in the district.
## Data
This project utilizes two primary data sources in CSV format, focusing on the educational landscape of various schools and their student performance. These datasets have been generated by [Mockaroo, LLC (2022)](https://mockaroo.com/) under the title "Realistic Data Generator" and are intended for educational purposes only. The data creation is credited to edX Boot Camps LLC.

**Schools Data** (`schools_complete.csv`)
| Column      | Description                                   |
|-------------|-----------------------------------------------|
| School ID   | Unique identifier for each school.            |
| school_name | Name of the school.                           |
| type        | The type of school (e.g., District or Charter)|
| size        | The number of students enrolled in the school.|
| budget      | The total budget allocated to the school.     |

**Students Data** (`students_complete.csv`)
| Column       | Description                                    |
|--------------|------------------------------------------------|
| Student ID   | Unique identifier for each student.            |
| student_name | Name of the student.                           |
| gender       | Gender of the student.                         |
| grade        | Grade level of the student (e.g., 9th, 10th).  |
| school_name  | Name of the school the student attends.        |
| reading_score| Reading score of the student.                  |
| math_score   | Math score of the student.                     |

The schools dataset provides a foundation for analyzing the distribution of schools by type, their sizes, and budget allocations. The students dataset is crucial for evaluating student performance in different subjects across various schools and grades. Together, they offer a comprehensive view of the structure of the school system and the academic achievements of its students. The analysis aims to uncover insights into the effectiveness of different school types and identify areas for improvement in student education.
## Implementation
This section outlines the key steps taken in the PyCity Schools Analysis
### District Summary
#### Date Preparation and Merging
```python
# Import pandas library
import pandas as pd

# File paths for school and student data
school_data_file = '../Resources/schools_complete.csv'
student_data_file = '../Resources/students_complete.csv'

# Load files into DataFrames
school_data = pd.read_csv(school_data_file)
student_data = pd.read_csv(student_data_file)

# Merge student and school data on 'school_name' and display results
school_data_complete = pd.merge(student_data, school_data, how='left', on=['school_name', 'school_name'])
school_data_complete.head()
```
The process begins with the `pandas` library being imported for data handling. School and student data, sourced from CSV files, are loaded into separate DataFrames. These datasets are then merged into a single DataFrame, `school_data_complete`, based on the `school_name` column. 
#### Calculating the Total Number of Unique Schools
```python
# Calculate the total number of unique schools
school_count = school_data_complete['school_name'].nunique()
school_count
```
The unique count of schools is determined using the `nunique()` method on the `school_name` column of the `school_data_complete` DataFrame.
#### Calculating the Total Number of Students
```python
# Calculate the total number of students
student_count = school_data_complete['student_name'].count()
student_count
```
The total number of students is calculated by applying the `count()` method to the `student_name` column of the `school_data_complete` DataFrame.
#### Calculating the Total Budget
```python
# Calculate the total budget
total_budget = school_data['budget'].sum()
total_budget
```
The overall budget for all schools is computed by summing the values in the `budget` column of the `school_data` DataFrame.
#### Calculating the Average Math Score
```python
# Calculate the average (mean) math score
average_math_score = school_data_complete['math_score'].mean()
average_math_score
```
The average math score across the student body is calculated using the `mean()` method on the `math_score` column in the `school_data_complete` DataFrame.
#### Calculating the Average Reading Score
```python
# Calculate the average (mean) reading score
average_reading_score = school_data_complete['reading_score'].mean()
average_reading_score
```
The average reading score is calculated by applying the `mean()` method to the `reading_score` column in the `school_data_complete` DataFrame.
#### Calculating the Percentage of Students Passing Math
```python
# Calculate the percentage of students who passed math (math scores greater than or equal to 70)
passing_math_count = school_data_complete[(school_data_complete["math_score"] >= 70)].count()["student_name"]
passing_math_percentage = passing_math_count / float(student_count) * 100
passing_math_percentage
```
The percentage of students passing math is calculated by identifying scores ≥ 70 in `math_score` and expressing this count as a percentage of total students.
#### Calculating the Percentage of Students Passing Reading
```python
# Calculate the percentage of students who passed reading
passing_reading_count = school_data_complete[(school_data_complete["reading_score"] >= 70)].count()["student_name"]
passing_reading_percentage = passing_reading_count / float(student_count) * 100
passing_reading_percentage
```
The percentage of students passing reading is calculated by identifying scores ≥ 70 in `reading_score` and expressing this count as a percentage of total students.
#### Percentage of Students Passing Both Math and Reading
```python
# Calculate the percentage of students that passed math and reading
passing_math_reading_count = school_data_complete[
    (school_data_complete["math_score"] >= 70) & (school_data_complete["reading_score"] >= 70)
].count()["student_name"]
overall_passing_rate = passing_math_reading_count /  float(student_count) * 100
overall_passing_rate
```
The percentage of students passing both math and reading is computed by identifying those who scored ≥ 70 in both subjects and then calculating this group's proportion relative to the total student count.
#### Creation of District Summary DataFrame
```python
# Create a high-level snapshot of the district's key metrics in a DataFrame
district_summary = pd.DataFrame([{
    "Total Shools": school_count,
    "Total Students": student_count,
    "Total Budget": total_budget,
    "Average Math Score": average_math_score,
    "Average Reading Score": average_reading_score,
    "% Passing Math": passing_math_percentage,
    "% Passing Reading": passing_reading_percentage,
    "% Overall Passing": overall_passing_rate
}])

# Formatting
district_summary["Total Students"] = district_summary["Total Students"].map("{:,}".format)
district_summary["Total Budget"] = district_summary["Total Budget"].map("${:,.2f}".format)

# Display the DataFrame
district_summary
```
A high-level snapshot of the district's key metrics is compiled into a DataFrame named `district_summary`. This DataFrame includes total schools, students, budget, average scores, and passing percentages, with formatting applied to enhance readability.
### School Summary
#### Selecting School Types
```python
# Select the school type
school_types = school_data.set_index(["school_name"])["type"]
school_types
```
The script extracts the types of each school, setting `school_name` as the index and selecting the `type` column from the `school_data` DataFrame.
#### Calculating Total Student Count per School
```python
# Calculate the total student count
per_school_counts = school_data_complete.groupby('school_name')['student_name'].count()
per_school_counts
```
The total number of students for each school is calculated by grouping `school_data_complete` by `school_name` and counting `student_name` entries.
#### Calculating School Budgets and Per Capita Spending
```python
# Calculate the total school budget and per capita spending
per_school_budget = school_data_complete.groupby(["school_name"]).mean(numeric_only=True)["budget"]
per_school_capita = per_school_budget / per_school_counts
```
The script computes each school's total budget and per capita spending by grouping `school_data_complete` by `school_name`, averaging the `budget`, and then dividing by the student count per school.
#### Calculating Average Test Scores per School
```python
# Calculate the average test scores
per_school_math = school_data_complete.groupby('school_name')['math_score'].mean()
per_school_reading = school_data_complete.groupby('school_name')['reading_score'].mean()
```
The average math and reading scores for each school are calculated by grouping `school_data_complete` by `school_name` and computing the mean of `math_score` and `reading_score`, respectively.
#### Schools with Math Scores of 70 or Higher
```python
# Calculate the number of schools with math scores of 70 or higher
school_passing_math = school_data_complete[school_data_complete["math_score"] >= 70]
```
Schools where students have achieved math scores of 70 or higher are identified from `school_data_complete` using a conditional filter on `math_score`.
#### Schools with Reading Scores of 70 or Higher
```python
# Calculate the number of schools with reading scores of 70 or higher
school_passing_reading = school_data_complete[school_data_complete["reading_score"] >= 70]
```
Schools with students achieving reading scores of 70 or higher are determined by filtering `school_data_complete` based on `reading_score`.
#### Identifying Schools Passing Both Math and Reading
```python
# Calculate the schools that passed both math and reading with scores of 70 or higher
passing_math_and_reading = school_data_complete[
    (school_data_complete["reading_score"] >= 70) & (school_data_complete["math_score"] >= 70)
]
```
Schools where students passed both math and reading with scores of 70 or higher are identified by applying a combined filter to `school_data_complete` on both `math_score` and `reading_score`.
#### Calculating Passing Rates for Each School
```python
# Calculate the passing rates
per_school_passing_math = school_passing_math.groupby(["school_name"]).count()["student_name"] / per_school_counts * 100
per_school_passing_reading = school_passing_reading.groupby(["school_name"]).count()["student_name"] / per_school_counts * 100
overall_passing_rate = passing_math_and_reading.groupby(["school_name"]).count()["student_name"] / per_school_counts * 100
```
The passing rates for math and reading are computed by dividing the count of students who passed in each subject by the total student count per school, then multiplying by 100. Similarly, the overall passing rate is determined by the proportion of students passing both math and reading.
#### Creating the School Summary DataFrame
```python
# Create a DataFrame called `per_school_summary` with columns for the calculations above.
per_school_summary = pd.DataFrame({
    "School Type": school_types,
    "Total Students": per_school_counts,
    "Total School Budget": per_school_budget,
    "Per Student Budget": per_school_capita,
    "Average Math Score": per_school_math,
    "Average Reading Score": per_school_reading,
    "% Passing Math": per_school_passing_math,
    "% Passing Reading": per_school_passing_reading,
    "% Overall Passing": overall_passing_rate
})

# Formatting
per_school_summary["Total School Budget"] = per_school_summary["Total School Budget"].map("${:,.2f}".format)
per_school_summary["Per Student Budget"] = per_school_summary["Per Student Budget"].map("${:,.2f}".format)

# Reset index and display the DataFrame
per_school_summary.reset_index(inplace=True)
per_school_summary
```
A DataFrame named `per_school_summary` is created, encapsulating key metrics such as school type, student counts, budgets, average scores, and passing rates. It includes formatting for budget values and resets the index for clearer presentation.
### Highest-Performing Schools (by % Overall Passing)
```python
# Sort the schools by '% Overall Passing' in descending order and display the top 5 rows
top_schools = per_school_summary.sort_values("% Overall Passing", ascending=False)
top_schools.head()
```
The DataFrame `per_school_summary` is sorted by '% Overall Passing' in descending order, and the top 5 schools are displayed, showcasing the highest achievers in terms of overall student passing rates.
### Bottom Performing Schools (By % Overall Passing)
```python
# Sort the schools by `% Overall Passing` in ascending order and display the top 5 rows.
bottom_schools = per_school_summary.sort_values("% Overall Passing", ascending=True)
bottom_schools.head()
```
The schools are sorted by `% Overall Passing` in ascending order to identify those with the lowest passing rates. The top 5 rows from this sorted list are displayed, highlighting the schools requiring the most attention in terms of improving student performance.
### Math Scores by Grade
```python
# Separate the data by grade
ninth_graders = school_data_complete[(school_data_complete["grade"] == "9th")]
tenth_graders = school_data_complete[(school_data_complete["grade"] == "10th")]
eleventh_graders = school_data_complete[(school_data_complete["grade"] == "11th")]
twelfth_graders = school_data_complete[(school_data_complete["grade"] == "12th")]

# Group by "school_name" and take the mean of each.
ninth_graders_scores = ninth_graders.groupby(["school_name"]).mean(numeric_only=True)
tenth_graders_scores = tenth_graders.groupby(["school_name"]).mean(numeric_only=True)
eleventh_graders_scores = eleventh_graders.groupby(["school_name"]).mean(numeric_only=True)
twelfth_graders_scores = twelfth_graders.groupby(["school_name"]).mean(numeric_only=True)

# Select only the `math_score`.
ninth_grade_math_scores = ninth_graders_scores["math_score"]
tenth_grade_math_scores = tenth_graders_scores["math_score"]
eleventh_grade_math_scores = eleventh_graders_scores.mean()["math_score"]
twelfth_grade_math_scores = twelfth_graders_scores["math_score"]

# Combine each of the scores above into single DataFrame called `math_scores_by_grade`
math_scores_by_grade =pd.DataFrame({
    "9th":ninth_grade_math_scores,
    "10th":tenth_grade_math_scores,
    "11th":eleventh_grade_math_scores,
    "12th":twelfth_grade_math_scores
})

# Minor data wrangling
math_scores_by_grade.index.name = None

# Display the DataFrame
math_scores_by_grade
```
Math scores are segmented by grade levels: 9th, 10th, 11th, and 12th. The data is separated for each grade, grouped by school, and the average math scores are calculated. These scores are then consolidated into a DataFrame, `math_scores_by_grade`, providing a clear comparison of math achievement across different grades in each school. Minor data wrangling is applied to refine the DataFrame's presentation.
### Reading Score by Grade
```python
# Select only the `reading_score`.
ninth_grade_reading_scores = ninth_graders_scores["reading_score"]
tenth_grade_reading_scores = tenth_graders_scores["reading_score"]
eleventh_grade_reading_scores = eleventh_graders_scores["reading_score"]
twelfth_grade_reading_scores = twelfth_graders_scores["reading_score"]

# Combine each of the scores above into single DataFrame called `reading_scores_by_grade`
reading_scores_by_grade =pd.DataFrame({
    "9th":ninth_grade_reading_scores,
    "10th":tenth_grade_reading_scores,
    "11th":eleventh_grade_reading_scores,
    "12th":twelfth_grade_reading_scores
})

# Minor data wrangling
reading_scores_by_grade.index.name = None

# Display the DataFrame
reading_scores_by_grade
```
The analysis focuses on reading scores for each grade level. After extracting reading scores for 9th, 10th, 11th, and 12th graders, these are combined into a DataFrame named `reading_scores_by_grade`. This DataFrame offers a clear view of how reading performance varies across different grades within schools, facilitated by some minor data adjustments for clarity in presentation.
### Scores by School Spending
#### Established Spending Bins
```python
# Establish the bins 
spending_bins = [0, 585, 630, 645, 680]
labels = ["<$585", "$585-630", "$630-645", "$645-680"]
```
Spending bins are defined for categorizing schools by per-student budget, along with corresponding labels for each range.
#### Creating a Copy for School Spending Analysis
```python
# Create a copy of the school summary since it has the "Per Student Budget" 
school_spending_df = per_school_summary.copy()
```
A copy of the `per_school_summary` DataFrame is created, named `school_spending_df`, to facilitate analysis based on the "Per Student Budget".
#### Converting 'Per Student Budget' to Numeric Format
```python
# Convert 'Per Student Budget' from string to float by removing dollar signs and commas, then casting to float
school_spending_df['Per Student Budget'] = school_spending_df['Per Student Budget'].replace('[\$,]', '', regex=True).astype(float)
```
'Per Student Budget' in `school_spending_df` is converted from a string to a float by removing dollar signs and commas.
#### Categorizing Schools by Spending Ranges
```python
# Use `pd.cut` to categorize spending based on the bins.
school_spending_df["Spending Ranges (Per Student)"] = pd.cut(school_spending_df['Per Student Budget'], spending_bins,labels=labels, right=False)
school_spending_df
```
'Spending Ranges (Per Student)' is assigned to `school_spending_df` using `pd.cut` to categorize 'Per Student Budget' into the defined spending bins and labels.
#### Calculating Averages by Spending Range
```python
#  Calculate averages for the desired columns. 
spending_math_scores = school_spending_df.groupby(["Spending Ranges (Per Student)"]).mean(numeric_only=True)["Average Math Score"]
spending_reading_scores = school_spending_df.groupby(["Spending Ranges (Per Student)"]).mean(numeric_only=True)["Average Reading Score"]
spending_passing_math = school_spending_df.groupby(["Spending Ranges (Per Student)"]).mean(numeric_only=True)["% Passing Math"]
spending_passing_reading = school_spending_df.groupby(["Spending Ranges (Per Student)"]).mean(numeric_only=True)["% Passing Reading"]
overall_passing_spending = school_spending_df.groupby(["Spending Ranges (Per Student)"]).mean(numeric_only=True)["% Overall Passing"]
```
Averages for 'Average Math Score', 'Average Reading Score', '% Passing Math', '% Passing Reading', and '% Overall Passing' are calculated within each spending range in `school_spending_df`.
#### Assembling Spending Summary DataFrame
```python
# Assemble into DataFrame
spending_summary = pd.DataFrame({
    "Average Math Score": spending_math_scores,
    "Average Reading Score": spending_reading_scores,
    "% Passing Math": spending_passing_math,
    "% Passing Reading": spending_passing_reading,
    "% Overall Passing": overall_passing_spending
})

# Display results
spending_summary
```
A new DataFrame, `spending_summary`, is created, compiling the calculated averages for math and reading scores, and passing percentages across different spending ranges.
### Scores by School Size
#### Setting School Size Bins
```python
# Establish the bins.
size_bins = [0, 1000, 2000, 5000]
labels = ["Small (<1000)", "Medium (1000-2000)", "Large (2000-5000)"]
```
Bins and corresponding labels are defined to categorize schools based on their student population sizes.
#### Categorizing Schools by Size
```python
# Categorize the spending based on the bins
# Use `pd.cut` on the "Total Students" column of the `per_school_summary` DataFrame.
per_school_summary["School Size"] = pd.cut(per_school_summary["Total Students"], size_bins, labels=labels)
per_school_summary
``` 
School sizes are categorized in the `per_school_summary` DataFrame using `pd.cut` on the "Total Students" column, based on the predefined size bins.
#### Calculating Averages by Spending Range
```python
# Calculate averages for the desired columns. 
size_math_scores = per_school_summary.groupby(["School Size"]).mean(numeric_only=True)["Average Math Score"]
size_reading_scores = per_school_summary.groupby(["School Size"]).mean(numeric_only=True)["Average Reading Score"]
size_passing_math = per_school_summary.groupby(["School Size"]).mean(numeric_only=True)["% Passing Math"]
size_passing_reading = per_school_summary.groupby(["School Size"]).mean(numeric_only=True)["% Passing Reading"]
size_overall_passing = per_school_summary.groupby(["School Size"]).mean(numeric_only=True)["% Overall Passing"]
```
Averages for 'Average Math Score', 'Average Reading Score', '% Passing Math', '% Passing Reading', and '% Overall Passing' are calculated within each school size category in `per_school_summary`.
#### Creating School Size Summary DataFrame
```python
# Create a DataFrame called `size_summary` that breaks down school performance based on school size (small, medium, or large).
# Use the scores above to create a new DataFrame called `size_summary`
size_summary = pd.DataFrame({
    "Average Math Score": size_math_scores,
    "Average Reading Score": size_reading_scores,
    "% Passing Math": size_passing_math,
    "% Passing Reading": size_passing_reading,
    "% Overall Passing": size_overall_passing
})

# Display results
size_summary
```
A new DataFrame, `size_summary`, is created, compiling the calculated averages for math and reading scores, and passing percentages across different school sizes.
### Scores by School Type
#### School Type Performance Metrics
```python
# Group the per_school_summary DataFrame by "School Type" and average the results for different metrics.
type_math_scores = per_school_summary.groupby(["School Type"]).mean(numeric_only=True)["Average Math Score"]
type_reading_scores = per_school_summary.groupby(["School Type"]).mean(numeric_only=True)["Average Reading Score"]
type_passing_math = per_school_summary.groupby(["School Type"]).mean(numeric_only=True)["% Passing Math"]
type_passing_reading = per_school_summary.groupby(["School Type"]).mean(numeric_only=True)["% Passing Reading"]
type_overall_passing = per_school_summary.groupby(["School Type"]).mean(numeric_only=True)["% Overall Passing"]

# Select new column data
average_math_score_by_type = type_math_scores
average_reading_score_by_type = type_reading_scores
average_percent_passing_math_by_type = type_passing_math
average_percent_passing_reading_by_type = type_passing_reading
average_percent_overall_passing_by_type = type_overall_passing
```
Group the `per_school_summary` DataFrame by `School Type` and calculate the averages for 'Average Math Score', 'Average Reading Score', '% Passing Math', '% Passing Reading', and '% Overall Passing'. These averages are then assigned to new variables representing each metric, segmented by school type.
#### School Type Performance Summary DataFrame
```python
# Create a new DataFrame 'type_summary' with the calculated averages by school type
type_summary = pd.DataFrame({
    "Average Math Score": average_math_score_by_type,
    "Average Reading Score": average_reading_score_by_type,
    "% Passing Math": average_percent_passing_math_by_type,
    "% Passing Reading": average_percent_passing_reading_by_type,
    "% Overall Passing": average_percent_overall_passing_by_type
})

# Display the 'type_summary' DataFrame
type_summary
```
Create a DataFrame named `type_summary`, compiling the calculated averages for 'Average Math Score', 'Average Reading Score', '% Passing Math', '% Passing Reading', and '% Overall Passing' by school type. 
## Insights
### District Summary
Based on the provided district summary, the district comprises 15 schools with a total student population of 39,170 and an allocated budget of $24,649,428. Academic performance indicates an average math score of approximately 79 and an average reading score of nearly 82. However, there's a notable discrepancy in subject-wise passing rates: about 75% of students pass in math, while a higher proportion of 85.8% pass in reading. Despite these individual pass rates, the overall passing percentage, which likely considers students passing in both subjects, is significantly lower at 65.17%. This suggests a challenge in ensuring students excel across both core subjects.
### School Summary
The school summary highlights a clear divide in performance and resources between charter and district schools. Charter schools like Cabrera, Griffin, and Pena High Schools demonstrate high academic achievements with average math and reading scores above 83, and impressive overall passing rates above 90%. In contrast, district schools like Bailey, Figueroa, and Johnson High Schools show lower academic performance, with average scores in the mid to high 70s and overall passing rates barely crossing 54%. This disparity is also reflected in the budget allocation per student, which is generally higher in district schools (e.g., $652 at Hernandez High School) compared to charter schools (e.g., $581 at Holden High School). These insights suggest that while district schools receive more funding per student, charter schools are achieving better academic outcomes.
### Highest-Performing Schools (by % Overall Passing)
The data from the highest-performing schools, all of which are charter schools, shows a clear pattern of academic excellence. These schools - Cabrera, Thomas, Griffin, Wilson, and Pena High Schools - boast high average scores in both math and reading, exceeding 83 in each subject. Their overall passing rates are notably high, ranging from 90.54% to 91.33%. These schools also manage to achieve these results with varied per-student budgets, suggesting that factors other than just financial resources, such as school policies, teaching methods, or student support systems, play a significant role in their success. This data underscores the effectiveness of charter schools in this district, particularly in fostering high academic achievement.
### Bottom Performing Schools (By % Overall Passing)
The data from the bottom-performing schools, all district schools, indicates a consistent struggle in academic performance. These schools - Rodriguez, Figueroa, Huang, Hernandez, and Johnson High Schools - have lower average scores in math and reading, with math scores around 76-77 and reading scores just above 80. Their overall passing rates are notably lower, all below 54%. Despite having comparable or higher per-student budgets than some of the high-performing charter schools, these district schools are not achieving similar academic success. This suggests a need for a critical review of their educational strategies, resource allocation, and support systems to identify areas for improvement and to close the performance gap.
### Math Scores by Grade
The analysis of math scores by grade across various schools reveals several interesting patterns. Generally, there is consistency in math performance across different grades within the same school. Notably, schools like Cabrera, Griffin, and Wright High Schools maintain high math scores across all grades, consistently above 83. In contrast, schools like Bailey, Figueroa, and Rodriguez show lower scores, around 76-77. Interestingly, the 11th grade math scores are uniformly 80.575873 across all schools, suggesting a possible data anomaly or standardized testing effect. Schools like Pena and Shelton High Schools show an upward trend in scores from 9th to 12th grade, indicating effective progression in math education. This data can guide targeted interventions to improve math education, particularly in lower-performing schools and grades.
### Reading Scores by Grade
The analysis of reading scores by grade across different schools reveals a consistent and strong performance in reading across all grades. Notably, schools like Cabrera, Griffin, and Thomas High Schools maintain high reading scores for each grade, generally exceeding 83. There is less variability in reading scores compared to math scores, with most schools showing consistent performance across grades. Schools like Shelton and Wright High Schools exhibit particularly strong performance in the 11th and 12th grades, indicating effective upper-grade reading programs. Unlike in math, there is no uniform score across a specific grade, suggesting more individualized performance in reading. This data highlights the overall strength in reading education across these schools and can be used to identify best practices for enhancing reading skills, especially in schools with slightly lower scores.
### Scores by School Spending
The analysis of scores by school spending reveals a counterintuitive trend: schools with lower per-student spending often perform better academically. Schools like Cabrera, Holden, Wilson, and Wright High Schools, with spending below $585 per student, show high average scores (above 83) and overall passing rates above 90%. In contrast, schools in the higher spending brackets, such as Hernandez and Huang High Schools with spending between $645-680, exhibit lower academic performance, with average scores around 77 and overall passing rates just over 53%. This pattern suggests that higher spending per student does not necessarily correlate with better academic outcomes and that other factors might be influencing school performance.
### Scores by School Size
The analysis of scores by school size reveals distinct trends across different size categories. Large schools (2000-5000 students), like Bailey, Figueroa, and Johnson High Schools, generally exhibit lower academic performance, with average scores in the mid to high 70s and overall passing rates around 54%. In contrast, medium-sized schools (1000-2000 students), such as Cabrera, Griffin, and Shelton High Schools, and small schools (less than 1000 students), like Holden and Pena High Schools, show significantly higher performance. These smaller and medium-sized schools have average scores above 83 and overall passing rates above 89%. This suggests that school size may have a substantial impact on student outcomes, with smaller and medium-sized schools providing environments more conducive to higher academic achievement.
### Scores by School Type
The comparison of scores by school type presents a stark contrast in performance between charter and district schools. Charter schools show a significantly higher level of academic achievement, with average math and reading scores approximately 83.5 and 83.9, respectively, and an impressive overall passing rate of about 90.4%. In contrast, district schools have lower average scores, around 77 in math and 81 in reading, and a notably lower overall passing rate of approximately 53.7%. These figures indicate that students in charter schools are not only achieving higher scores in core academic subjects but also have a much higher likelihood of passing overall, suggesting a considerable difference in educational effectiveness between the two types of schools.
## Recommendations
* **Focus on Smaller School Sizes**: The data shows that smaller and medium-sized schools significantly outperform larger schools. It's recommended to consider strategies to reduce student-to-teacher ratios, possibly by creating more schools or reducing class sizes, to emulate the environment of smaller schools.

* **Re-evaluate Spending Strategies**: Despite higher spending per student in some district schools, this does not correlate with better academic outcomes. A thorough review of current spending allocations is suggested, focusing on optimizing resource utilization to enhance student performance, particularly in district schools.

* **Enhance Support in District Schools**: The stark contrast in performance between district and charter schools suggests the need for targeted interventions in district schools. This could include professional development for teachers, curriculum enhancements, and additional support resources for students.

* **Investigate Successful Practices in Charter Schools**: Charter schools in the dataset consistently show higher performance. Identifying and understanding the practices and policies driving these successes, and considering their application in district schools, could be beneficial.

* **Comprehensive Analysis of Individual School Performance**: While broad trends are evident, each school has its unique context and challenges. A detailed analysis of individual schools, especially those underperforming, can provide more tailored recommendations, addressing specific needs and circumstances.

Implementing these recommendations should be done with a focus on continuous monitoring and evaluation, ensuring that the strategies adopted are effectively meeting the intended goals of improving educational outcomes across all schools.	

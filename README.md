# Pandas-challenge



## Background
You are the new Chief Data Scientist for your city's school district. In this capacity, you'll be helping the school board and mayor make strategic decisions regarding future school budgets and priorities.

As a first task, you've been asked to analyze the district-wide standardized test results. You'll be given access to every student's math and reading scores, as well as various information on the schools they attend. Your task is to aggregate the data to showcase obvious trends in school performance.

## Instructions
Using Pandas and Jupyter Notebook, create a report that includes the following data. Your report must include a written description of at least two observable trends based on the data.

## District Summary
Perform the necessary calculations and then create a high-level snapshot of the district's key metrics in a DataFrame.

Include the following:

* Total number of unique schools
* Total students
* Total budget
* Average math score
* Average reading score
* % passing math (the percentage of students who passed math)
* % passing reading (the percentage of students who passed reading)
* % overall passing (the percentage of students who passed math AND reading)

Screenshot of the results:
<img width="1440" alt="Screen Shot 2022-10-17 at 11 14 06 AM" src="https://user-images.githubusercontent.com/112406455/196229143-b97c0a00-9097-46fa-80e9-0edbaa2000a6.png">

## School Summary
Perform the necessary calculations and then create a DataFrame that summarizes key metrics about each school.

Include the following:

* School name
* School type
* Total students
* Total school budget
* Per student budget
* Average math score
* Average reading score
* % passing math (the percentage of students who passed math)
* % passing reading (the percentage of students who passed reading)
* % overall passing (the percentage of students who passed math AND reading)

Screenshot of the results:
<img width="1440" alt="Screen Shot 2022-10-17 at 11 17 42 AM" src="https://user-images.githubusercontent.com/112406455/196229797-e51be9d2-deef-4deb-92aa-2a156b88f404.png">

## Highest-Performing Schools (by % Overall Passing)
Sort the schools by % Overall Passing in descending order and display the top 5 rows.
Save the results in a DataFrame called "top_schools".

Screenshot of the results:
<img width="1440" alt="Screen Shot 2022-10-17 at 11 22 12 AM" src="https://user-images.githubusercontent.com/112406455/196231309-51ea4ac3-a69b-429e-b389-79f6432b07c2.png">

## Lowest-Performing Schools (by % Overall Passing)
Sort the schools by % Overall Passing in ascending order and display the top 5 rows.
Save the results in a DataFrame called "bottom_schools".

Screenshot of the results:
<img width="1440" alt="Screen Shot 2022-10-17 at 11 22 22 AM" src="https://user-images.githubusercontent.com/112406455/196231402-c9e375a2-8329-4e9b-b1d5-aeccd9a4b36f.png">

## Math Scores by Grade
Perform the necessary calculations to create a DataFrame that lists the average math score for students of each grade level (9th, 10th, 11th, 12th) at each school.

Screenshot of the results:
<img width="1440" alt="Screen Shot 2022-10-17 at 11 22 34 AM" src="https://user-images.githubusercontent.com/112406455/196231591-ac90ece0-3769-4c12-9a5a-1cc8019abbe1.png">

## Reading Scores by Grade
Create a DataFrame that lists the average reading score for students of each grade level (9th, 10th, 11th, 12th) at each school.

Screenshot of the results:
<img width="1440" alt="Screen Shot 2022-10-17 at 11 22 44 AM" src="https://user-images.githubusercontent.com/112406455/196232181-a078c9b9-ca1a-4889-a58c-eaa14fbc5fb9.png">


## Scores by School Spending
Create a table that breaks down school performance based on average spending ranges (per student). Use the scores above to create a DataFrame called spending_summary.
Include the following metrics in the table:

* Average math score
* Average reading score
* % passing math (the percentage of students who passed math)
* % passing reading (the percentage of students who passed reading)
* % overall passing (the percentage of students who passed math AND reading)

Screenshot of the results:
<img width="1440" alt="Screen Shot 2022-10-17 at 11 23 43 AM" src="https://user-images.githubusercontent.com/112406455/196232567-168a57b2-de67-4d92-b616-384a0f5a258d.png">

## Scores by School Size
Create a DataFrame called size_summary that breaks down school performance based on school size (small, medium, or large).

Screenshot of the results:
<img width="1440" alt="Screen Shot 2022-10-17 at 11 23 55 AM" src="https://user-images.githubusercontent.com/112406455/196232924-5b2156b5-bc96-4009-b38a-ea770d3ee6ce.png">

## Scores by School Type
Use the per_school_summary DataFrame from the previous step to create a new DataFrame called type_summary.
This new DataFrame should show school performance based on the "School Type".

Screenshot of the results:
<img width="1440" alt="Screen Shot 2022-10-17 at 11 24 06 AM" src="https://user-images.githubusercontent.com/112406455/196233248-a8c9b9a5-5193-457b-a0b2-c38b20bd71dd.png">

## PyCity Schools Analysis
* Overall, schools with larger budgets does not guarantee better results. As you can see from the data, schools that spent the most per student (645-680), had the least percentage of an overall passing rate with about 54%, compared to schools that spent the least amount per student (585 and under) which had a 90% overall passing rate. 

* Large schools drastically under-performed in the overall passing rate of students compared to small and medium sized schools. Large schools had an overall passing rate of 58% compared to small and medium sized schools at about 90%.

* Charter schools preformed significantly better than district schools across the board. Charter schools had an overall passing rate of 90% compared to district schools at 54%. Charter schools had a smaller student population compared to district schools which could be a factor to their success, but more analysis would be required to confirm this assumption. 

## Instructions on how to run the code properly:

* Download the repository onto you computer
* Open the repository in Jupiter Notebook
* Select the mainscript.ipynb in the PyCitySchools folder
* Select the "Kernel" tab and click "Restart Kernel and Clear all Outputs"
* Then proceed to hit shift + enter to cycle through the script cell by cell
* The code is accompanied by an outline to walk you through the process step by step 

## References
Data generated by Mockaroo, LLCLinks to an external site., (2022). Realistic Data Generator. Modified by Trilogy Education Services, a 2U, Inc. brand.


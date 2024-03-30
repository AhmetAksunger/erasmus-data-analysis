# Erasmus Data Analysis with Pandas
This project involves the analysis of Erasmus program data using Python's Pandas library. The analysis covers the statistical analysis of the Erasmus program, including acceptance rates, grant distributions, scholarship types, country placements, and departmental statistics. The data analysis is conducted in a Jupyter Notebook environment.

## Table of Contents
1. [Data Source](#data-source)
2. [Analysis Overview](#analysis-overview)
3. [Analysis Results](#analysis-results)
    - [Final Data](#final-data)
    - [Status Summary and Distribution](#status-summary-and-distribution)
    - [Grant Summary and Distribution](#grant-summary-and-distribution)
    - [Scholarship Summary and Distribution](#scholarship-summary-and-distribution)
    - [Scholarship and Grant](#scholarship-and-grant-relation)
    - [Scholarship and Academic Score Relation](#scholarship-and-academic-score-relation)
    - [Countries of Placement Summary and Distribution](#countries-of-placement-summary-and-distribution)
    - [Department Summary and Distribution](#department-summary-and-distribution)


## Data Source
The data for this analysis was obtained from Istanbul Bilgi University, where I study. I was accepted into the Erasmus Exchange Program and decided to analyze the data published by the university. The original data source can be found in the link below.
https://www.bilgi.edu.tr/media/uploads/2024/03/25/2023-proje-erasmus-avrupa-ogrenim-hareketliligi-sonuclari.pdf

Note: The university has censored any malicious data to ensure no risky information is published.

## Analysis Overview
1. Data loading and cleaning: Loading data from Excel, cleaning up columns, handling missing values, and converting data types as needed.
2. Data preprocessing: Stripping whitespace, replacing missing values, and adding additional columns for analysis (e.g., scholarship type, grant status).
3. Statistical analysis: Grouping data, aggregating statistics, performing t-tests to compare mean scores, and generating summary statistics.
4. Visualization: Creating pie charts and data frame tables.

# Analysis Results

## Final Data
After adding additional columns and applying data cleaning, the final dataset is ready for analysis. Below is a snapshot of the first 20 rows of the cleaned data:

![Final Data](/images/final-data.png)

This image provides an overview of the cleaned dataset, showcasing the structure and content of the data after preprocessing steps.

## Status Summary and Distribution

There are 4 categories in the original data: 'Kabul Hibeli'(Accepted with Grant), 'Kabul Hibesiz'(Accepted without Grant), 'Ret'(Rejected), 'Kazanamadı(Not Accepted)', and 'Yedek'(Alternate).

The categories 'Kabul Hibeli' and 'Kabul Hibesiz' are merged into 'Accepted', 'Kazanamadı' and 'Ret' are merged into 'Rejected', and 'Yedek' is labelled as 'Alternate'.

![Status Summary](/images/status-summary.png)


This image above displays the status summary table, showing the count of applicants in each outcome category: 'Accepted', 'Rejected', and 'Alternate'.

Additionally, the pie chart below visually represents the distribution of Erasmus program statuses.
![Status Pie Chart](/images/status-distribution.png)

## Grant Summary and Distribution

The 'Grant' column in the dataset was added additionally. 
- If the student is accepted with the status 'Kabul Hibeli'(Accepted with Grant), it's labelled as Granted.
- If the student is accepted with the status 'Kabul Hibesiz'(Accepted without Grant), it's labelled as Ungranted.
- If the student is not accepted to Erasmus, the Grant column is NaN since it wouldn't make sense for that student to have a Grant-related column.

![Grant Summary](/images/grant-summary.png)


The image above displays the grant summary table, providing the distribution of granted and ungranted applicants and their average scores. 
The 'count' column shows the number of students, and the 'mean' column shows the average score of students in each category.

Additionally, the pie chart below visually represents the distribution of grants.
<div style="float: left; margin-right: 20px;">
    <img src="/images/grant-distribution.png" alt="Grant Distribution Pie Chart" width="400"/>
</div>

## Scholarship Summary and Distribution
The 'Scholarship' column in the dataset was also added additionally.
- If the student's programme includes 'Tam Burslu'(Full Scholarship), it's labelled as Full.
- If the student's programme includes '%50 Burslu'(%50 Scholarship), it's labelled as Partial.
- If the student's programme includes 'Ücretli', it's labelled as Paid.
- If it's none of these, the student is probably doing a Master's Degree, so the Scholarship section is NaN

<div style="float: left; margin-right: 20px;">
    <img src="/images/scholarship-summary.png" alt="Scholarship Summary" width="400"/>
</div>
The image above displays the scholarship summary table, providing the distribution of scholarships among Erasmus program applicants and their academic performance metrics. 

Additionally, the pie chart below visually represents the distribution of scholarships among applicants.
<div style="float: left; margin-right: 20px;">
    <img src="/images/scholarship-distribution.png" alt="Scholarship Pie Chart" width="400"/>
</div>

## Scholarship and Grant Relation
The dataset is grouped based on two columns: 'Scholarship' and 'Grant'. This grouping allows us to analyze the distribution of scholarships and grants among Erasmus program applicants
It also helps us to see which Scholarship category gets awarded with a grant the most.

<div style="float: left; margin-right: 20px;">
    <img src="/images/scholarship-grant-summary.png" alt="Scholarship Grant Summary" width="400"/>
</div>
The image above displays the scholarship and grant summary, into how scholarships and grants are distributed among applicants and their academic performance metrics.


Let's look at the distributions on the pie chart. Let's check which scholarship group was awarded with a Grant the most based on their percentages.

<div style="float: left;">
    <img src="/images/full-scholar-grant-distribution.png" alt="Scholarship Grant Pie Chart" width="400"/>
    <img src="/images/partial-scholar-grant-distribution.png" alt="Scholarship Grant Pie Chart" width="400"/>
    <img src="/images/paid-scholar-grant-distribution.png" alt="Scholarship Grant Pie Chart" width="400"/>
</div>

According to the analysis:
- 63% of students on Full Scholarships were awarded Grants.
- Knowing that Grants are allocated based on student's scores, this distribution indicates that students who are on
full scholarships may tend to get higher grades than others.

We will try to prove the second statement in the section below.

## Scholarship and Academic Score Relation

<div style="float: left;">
    <img src="/images/scholarship-grouped-summary.png" alt="Scholarship Pie Chart" width="400"/>
</div>
The table above calculates the mean, maximum, and minimum scores of students who were accepted into the Erasmus program, grouped by their scholarship status ('Scholarship'). 

The resulting pivot table provides statistics on the academic performance of accepted students based on their scholarship categories.

But do students who are on full scholarships have a significant difference from the other students?

### T-Test: Full Scholarship vs. Other Scholarships
A t-test was performed to check if students on full scholarships tend to get higher grades than students on partial or paid scholarships.

- Null Hypothesis (H0): There's no significant difference between full scholarship students and other students in terms of grades.
- Alternative Hypothesis (H1): There's a significant difference between full scholarship students and other students in terms of grades.
- Significance Level (α): 0.05

The output of the specific cell which performs the t-test is:
```
p value: 0.004429043550657171
p value is below the threshold of α = 0.05.
There is a significant difference in scores between students on Full Scholarship and others.
Students on full scholarships tend to achieve higher grades.
```

**Conclusion**:
These statistics suggest that full scholarships are associated with better academic performance among Erasmus program participants.

## Countries of Placement Summary and Distribution
The dataset is grouped based on the column 'Yerleştiği Yer Ülke', which represents the countries where students were placed during the Erasmus program. 

<div style="float: left;">
    <img src="/images/country-summary.png" alt="Scholarship Pie Chart" width="400"/>
</div>
The resulting grouped data is then summarized to provide statistics about the distribution of students across different countries and their average academic performance.

The pie chart below shows the distribution of students among different countries of placement.
Note that the last 10 countries are grouped as 'Others' in order not to make the pie chart confusing.
<div style="float: left;">
    <img src="/images/country-distribution.png" alt="Scholarship Pie Chart" width="400"/>
</div>

## Department Summary and Distribution
Students are grouped based on the 'Department' column. The 'Deparment' column is obtained by the 'Birim' column.
The 'Birim' column doesn't only include the department, but also some additional information about the programme the students are on.
Ex: Psikoloji Pr. (İngilizce) (%50 Burslu)
The 'Department' column is created by only taking the programme part which for this example is 'Psikoloji Pr.'

<div style="float: left;">
    <img src="/images/department-summary.png" alt="Scholarship Pie Chart" width="400"/>
</div>
The image above is the department summary table which showcases the number of students who have applied to the Erasmus Exchange Programme and are in the specified Department.
Also, the mean values and the percentage values are shown.

Note that the image only includes the first 10 departments. The rest of the data can be found [here](/erasmus-data-analysis.ipynb)

## References

- Istanbul Bilgi University: [Official Website](https://www.bilgi.edu.tr/)
- Data Source: [Erasmus Program Results](https://www.bilgi.edu.tr/media/uploads/2024/03/25/2023-proje-erasmus-avrupa-ogrenim-hareketliligi-sonuclari.pdf)

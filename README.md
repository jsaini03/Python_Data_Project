# The Analysis

## 1. What are the most in demand skills for the top 3 most popular data roles?

To determine the most sought-after skills for the top three data roles, I first identified the most popular positions and then selected the top five skills for each of these roles. This analysis showcases the leading job titles along with their key skills, highlighting which competencies I should focus on based on the specific role I am pursuing.

View my notebook with detailed steps here: [2_Most_InDemand_Skills.ipynb](Project\2_Most_InDemand_Skills.ipynb)

### Visualize Data

```python
fig, ax= plt.subplots(len(job_titles), 1 )

sns.set_theme(style='ticks')
for i, job_title in enumerate(job_titles):
    df_plot= df_skills_perct[df_skills_perct['job_title_short']==job_title].head()
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:g_r' )
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0,80)

    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1,n, f'{v:.0f}%' , va= 'center')
        
    if i!=len(job_titles)-1:
        ax[i].set_xticks([])


fig.suptitle("Likelihood of Skills Requested in US Job Postings", fontsize=15)
fig.tight_layout()
plt.show()
```

### Results

![Visualization of Top Skills](Project\Results\2_Most_InDemand_Skills.png.png)

### Insights

- Python is a versatile skill highly sought after across all three roles, with the highest demand seen for Data Scientists (72%) and Data Engineers (65%).
- SQL stands out as the most frequently requested skill for all three data roles, appearing in over half of the job listings.
- Data Engineers need more specialized technical skills (such as AWS, Azure, and Spark), while Data Analysts and Data Scientists are generally expected to be proficient in data management and analysis tools like Excel and Tableau.


## 2. How are in-demand skills for Data Analysts trending?

To analyze skill trends for Data Analysts in 2023, I filtered job postings specific to data analyst roles and grouped the associated skills by the month they were posted. This allowed me to identify the top 5 skills each month, highlighting the popularity of various skills throughout the year.

View my notebook with steps here: [3_Trending_Top_Skills](Project\3_Trending_Top_Skills.ipynb)

### Visualize Data

```python
plt.figure(figsize=(10,8))
sns.lineplot(data=df_plot,dashes=False, palette='tab10', )
sns.set_theme(style='ticks')
sns.despine()

plt.title('Trending Top Skills for Data Analysts in US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('')
plt.legend(loc= 'upper right', fontsize='small')

from matplotlib.ticker import PercentFormatter
ax= plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()
```

### Results
![Visualization of Trending Top Skills in US](Project\Results\3_Trending_Skills.png)

### Insights

- SQL maintained steady demand throughout the year, though with a slight decline over time. 
- In contrast, Excel shows stable demand during the first three quarters. By December, its demand rises sharply, almost catching up with SQL. This suggests that Excel skills became more valued in data analyst roles toward the end of the year.
- Python and Tableau remained relatively stable with minor fluctuations, underscoring their essential role for data analysts. 
- Meanwhile, SaS, while less in demand compared to the others, showed a modest upward trend toward the end of the year.


## 3. What is the Salary Distribution among all the data jobs in US?

To pinpoint the highest-paying roles and skills, I focused on jobs within the United States and analyzed their median salaries. I first examined the salary distributions of popular data roles like Data Scientist, Data Engineer, and Data Analyst to understand which positions offer the highest compensation.

View my notebook with steps here: [4_Salary_Analysis](Project\4_Salary_Analysis.ipynb)

### Visualize Data

```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order= job_order)
sns.set_theme(style='ticks')
sns.despine()

plt.title('Salary Distributions of Data Jobs in US')
plt.xlabel('Yearly Salary (USD)')
plt.ylabel('')
plt.xlim(0,600000)
ticks_x= plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}k')
plt.gca().xaxis.set_major_formatter(ticks_x)

plt.show()
```
### Results
![Visualization of Salary Analysis](Project\Results\4_Salary_Analysis.png)
*Box plot visualizing the salary distributions for the top 6 data jobs*

### Insights

- Salary ranges vary significantly across different data job titles. Senior Data Scientist roles have some of the highest earning potential, highlighting the industry's high regard for advanced data expertise and experience.
- Senior Data Engineer and Senior Data Scientist positions also display numerous high-end outliers, indicating that exceptional skills or unique circumstances can lead to substantial pay in these roles. In contrast, Data Analyst roles show more consistent salary distributions with fewer outliers.
- Median salaries tend to increase with role seniority and specialization. Senior positions (such as Senior Data Scientist and Senior Data Engineer) not only command higher median salaries but also show greater variation in typical pay, reflecting a wider range in compensation as responsibilities grow.

### Highest Paid & Most Demanded Skills for Data Analyst

Next I narrowed the analysis and focused on DA roles and looked for both highest paid skills and most in-demand skills. Used 2 bar charts to showcase the comparison.

### Visualize Data
```python
fig, ax = plt.subplots(2,1)

# Top 10 highest paid skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', palette='dark:g_r', ax=ax[0])
ax[0].legend().remove()
ax[0].set_title('Highest Paid Skills for DA in US')
ax[0].set_ylabel('')
ax[0].set_xlabel('')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, y: f'${int(x/1000)}k'))

# Top 10 most in-demand skills for Data Analysts
sns.barplot(data=df_DA_top_skills, x='median', y=df_DA_top_skills.index, hue='median', palette='light:g', ax=ax[1])
ax[1].legend().remove()
ax[1].set_title('Most In-Demand Skills for DA in US')
ax[1].set_ylabel('')
ax[1].set_xlabel('Median Salary (USD)')
ax[1].set_xlim(ax[0].get_xlim())
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, y: f'${int(x/1000)}k'))

sns.set_theme(style='ticks')
plt.tight_layout()
plt.show()
```
### Results
![Visualization of Top Paying Skills and Most in-demand Skills](Project\Results\4_Top_Pay_&_Skills.png)

### Insights

- The top graph shows that specialized technical skills like dplyr, Bitbucket, and Gitlab are linked to higher salaries, with some reaching up to $200K, indicating that advanced technical expertise can boost earning potential.
- In contrast, the bottom graph reveals that foundational skills such as Excel, PowerPoint, and SQL are the most in-demand, though they don’t typically offer the highest salaries. This underscores the importance of these core skills for securing roles in data analysis.
- This distinction between high-paying skills and high-demand skills suggests that data analysts looking to maximize their career potential should aim to build a well-rounded skill set that includes both lucrative specialized skills and essential foundational ones.

## 4. What are the most Optimal Skills to learn for DA roles?
To identify the most optimal skills to learn ( the ones that are the highest paid and highest in demand) I calculated the percent of skill demand and the median salary of these skills. To easily identify which are the most optimal skills to learn.

View my notebook with steps here: [5_Most_Optimal_Skills](Project\5_Most_optimal_skills.ipynb)

### Visualize Data
```python
from adjustText import adjust_text

plt.scatter(df_DA_skills['skill_percent'], df_DA_skills['median_salary'])
plt.xlabel('Percent of Data Analyst Jobs')
plt.ylabel('Median Salary ($USD)')  # Assuming this is the label you want for y-axis
plt.title('Most Optimal Skills for Data Analysts in the US')

# Get current axes, set limits, and format axes
from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))  # Example formatting y-axis
ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))
# Add labels to points and collect them in a list
texts = []
for i, txt in enumerate(df_DA_skills.index):
    texts.append(plt.text(df_DA_skills['skill_percent'].iloc[i], df_DA_skills['median_salary'].iloc[i], " " + txt))

# Adjust text to avoid overlap and add arrows
adjust_text(texts, arrowprops=dict(arrowstyle='->', color='gray'))

plt.show()
```
### Results
![Visualization of Optimal Skills](Project\Results\5_Most_Optimal_Skills.png)
*Scatter plot visualizing the most optimal skills for DA roles in US*

### Insights

- The skill Oracle appears to have the highest median salary of nearly $97K, despite being less common in job postings. This suggests a high value placed on specialized database skills within the data analyst profession.
- More commonly required skills like Excel and SQL have a large presence in job listings but lower median salaries compared to specialized skills like Python and Tableau, which not only have higher salaries but are also moderately prevalent in job listings.
- Skills such as Python, Tableau, and SQL Server are towards the higher end of the salary spectrum while also being fairly common in job listings, indicating that proficiency in these tools can lead to good opportunities in data analytics.

## Summary

Throughout this project, I gained deeper insights into the data analyst job market and strengthened my technical skills in Python, particularly in data manipulation and visualization. Here are a few key lessons I learned:
- Advanced Python Skills: Leveraging libraries like Pandas for data manipulation and Seaborn and Matplotlib for data visualization enabled me to perform complex data analysis tasks more efficiently.
- Significance of Data Cleaning: I discovered that thorough data cleaning and preparation are essential to ensure accurate insights from analysis.
- Strategic Skill Alignment: The project highlighted the value of aligning personal skills with market demand. Understanding the relationship between skill demand, salary, and job availability supports more strategic career planning within the tech industry.

### Challenges Faced
- Data Inconsistencies: Handling missing or inconsistent data entries requires careful consideration and thorough data-cleaning techniques to ensure the integrity of the analysis.
- Complex Data Visualization: Designing effective visual representations of complex datasets was challenging but critical for conveying insights clearly and compellingly.
- Balancing Breadth and Depth: Deciding how deeply to dive into each analysis while maintaining a broad overview of the data landscape required constant balancing to ensure comprehensive coverage without getting lost in details.

## Conclusion

This exploration into the data analyst job market has been highly insightful, shedding light on the key skills and trends that define this dynamic field. The insights gained have deepened my understanding and offer practical guidance for those aiming to advance in data analytics. As the market continues to evolve, ongoing analysis will be crucial to staying competitive in the field. This project serves as a solid foundation for future studies and underscores the importance of continuous learning and adaptation in data analytics.
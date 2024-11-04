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

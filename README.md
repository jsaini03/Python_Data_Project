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
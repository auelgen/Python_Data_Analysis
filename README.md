# Data Science Project: Skills and Salary Analysis
Overview
This repository contains a comprehensive analysis of skills and salaries in the tech industry. We aim to answer key questions about the trends and value of various skills in the job market. The analysis is divided into four notebooks:

# SalaryAnalysis.ipynb: Analyzes the salary distribution and factors influencing salaries.
 
      sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)
      sns.set_theme(style='ticks')
      sns.despine()
      
      plt.title('Salary Distributions of Data Jobs in the US')
      plt.xlabel('Yearly Salary (USD)')
      plt.ylabel('')
      plt.xlim(0, 600000) 
      ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
      plt.gca().xaxis.set_major_formatter(ticks_x)
      plt.show()
![image](https://github.com/user-attachments/assets/d90c30f7-fc4f-4ea8-a563-726d558f3c44)

      fig, ax = plt.subplots(2, 1)  
      
      # Top 10 Highest Salaries  for Data Analysts
      sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')
      ax[0].legend().remove()
      # original code:
      # df_DA_top_pay[::-1].plot(kind='barh', y='median', ax=ax[0], legend=False) 
      ax[0].set_title('Highest Paid Skills for Data Analysts in the US')
      ax[0].set_ylabel('')
      ax[0].set_xlabel('')
      ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))
      
      
      # Top 10 Skills for Data Analysts')
      sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')
      ax[1].legend().remove()
      
      # df_DA_skills[::-1].plot(kind='barh', y='median', ax=ax[1], legend=False)
      ax[1].set_title('Most In-Demand Skills for Data Analysts in the US')
      ax[1].set_ylabel('')
      ax[1].set_xlabel('Median Salary (USD)')
      ax[1].set_xlim(ax[0].get_xlim())  # Set the same x-axis limits as the first plot
      ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))
      
      sns.set_theme(style='ticks')
      plt.tight_layout()
      plt.show()

![image](https://github.com/user-attachments/assets/797df33e-8522-44b8-967c-2ca66de76322)
      
# Skill_Count.ipynb: Counts the occurrences of various skills in job postings.
        fig, ax = plt.subplots(len(job_titles), 1)
        
        sns.set_theme(style='ticks')
        
        for i, job_title in enumerate(job_titles):
            df_plot = df_skills_count[df_skills_count['job_title_short'] == job_title].head(5)[::-1]
            sns.barplot(data=df_plot, x='skill_count', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
            ax[i].set_title(job_title)
            ax[i].invert_yaxis()
            ax[i].set_ylabel('')
            ax[i].set_xlabel('')
            ax[i].get_legend().remove()
            ax[i].set_xlim(0, 45000) 
        
        fig.suptitle('Counts of Skills Requested in US Job Postings', fontsize=15)
        fig.tight_layout(h_pad=0.5)
        plt.show()
![image](https://github.com/user-attachments/assets/8bc809c0-14d3-4c31-b66b-4668f4873be5)

fig, ax = plt.subplots(len(job_titles), 1)


          for i, job_title in enumerate(job_titles):
              df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
              sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
              ax[i].set_title(job_title)
              ax[i].set_ylabel('')
              ax[i].set_xlabel('')
              ax[i].get_legend().remove()
              ax[i].set_xlim(0, 78)
              if i != len(job_titles) - 1:
                  ax[i].set_xticks([])
          
              for n, v in enumerate(df_plot['skill_percent']):
                  ax[i].text(v + 1, n, f'{v:.0f}%', va='center')
          
          fig.suptitle('Likelihood of Skills Requested in US Job Postings', fontsize=15)
          fig.tight_layout(h_pad=.8)
          plt.show()
![image](https://github.com/user-attachments/assets/bd9302c5-62a0-466f-a776-fd4a40018ee9)

# TrendSkills.ipynb: Examines trends in the demand for specific skills over time.
      df_DA_US_pivot.iloc[:, :5].plot(kind='line')
      
      plt.title('Trending Top Skills for Data Analysts in the US')
      plt.ylabel('Count')
      plt.xlabel('')
      plt.show()
![image](https://github.com/user-attachments/assets/69f2388b-ef70-4ade-83bc-dc3e0331fae3)

      from matplotlib.ticker import PercentFormatter
      
      df_plot = df_DA_US_percent.iloc[:, :5]
      sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')
      sns.set_theme(style='ticks')
      sns.despine() # remove top and right spines
      
      plt.title('Trending Top Skills for Data Analysts in the US')
      plt.ylabel('Likelihood in Job Posting')
      plt.xlabel('2023')
      plt.legend().remove()
      plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))
      
      for i in range(5):
          plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i], color='black')
      
      plt.show()
![image](https://github.com/user-attachments/assets/1be8bce9-e121-4e65-b320-85de536e0992)

      
# ValuableSkills.ipynb: Identifies the most valuable skills that are associated with higher salaries.
      from adjustText import adjust_text
      
      plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])
      plt.xlabel('Percent of Data Analyst Jobs')
      plt.ylabel('Median Salary ($USD)')  
      plt.title('Most Optimal Skills for Data Analysts in the US')
      
      ax = plt.gca()
      ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))  # Example formatting y-axis
      
      texts = []
      for i, txt in enumerate(df_DA_skills_high_demand.index):
          texts.append(plt.text(df_DA_skills_high_demand['skill_percent'].iloc[i], df_DA_skills_high_demand['median_salary'].iloc[i], " " + txt))
      
      adjust_text(texts, arrowprops=dict(arrowstyle='->', color='gray'))
      
      plt.show()

  ![image](https://github.com/user-attachments/assets/9caeeaf2-9b01-4bd7-8671-f5ce3c5b1ff9)



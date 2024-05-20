
Code
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
df=pd.read_csv('all_data.csv')
print(df.head())
  Country  Year  Life expectancy at birth (years)           GDP
0   Chile  2000                              77.3  7.786093e+10
1   Chile  2001                              77.3  7.097992e+10
2   Chile  2002                              77.8  6.973681e+10
3   Chile  2003                              77.9  7.564346e+10
4   Chile  2004                              78.0  9.921039e+10
df.shape
(96, 4)
print(df.Country.unique())
['Chile' 'China' 'Germany' 'Mexico' 'United States of America' 'Zimbabwe']
print(df['Year'].unique())
[2000 2001 2002 2003 2004 2005 2006 2007 2008 2009 2010 2011 2012 2013
 2014 2015]
df=df.rename({'Life expectancy at birth (years)':'LEAPBY'},axis='columns')
df.head()
Country	Year	LEAPBY	GDP
0	Chile	2000	77.3	7.786093e+10
1	Chile	2001	77.3	7.097992e+10
2	Chile	2002	77.8	6.973681e+10
3	Chile	2003	77.9	7.564346e+10
4	Chile	2004	78.0	9.921039e+10
plt.figure(figsize=(8,6))
sns.displot(df.GDP,rug=True,kde=False)
plt.xlabel('GDP in Trillion of US Dollars')
C:\Users\user\anaconda3\Lib\site-packages\seaborn\axisgrid.py:118: UserWarning: The figure layout has changed to tight
  self._figure.tight_layout(*args, **kwargs)
Text(0.5, 9.444444444444438, 'GDP in Trillion of US Dollars')
<Figure size 800x600 with 0 Axes>

plt.figure(figsize=(8,6))
sns.displot(df.LEAPBY,rug=True,kde=False)
plt.xlabel('Life Expectancy of Birth(Year)')
C:\Users\user\anaconda3\Lib\site-packages\seaborn\axisgrid.py:118: UserWarning: The figure layout has changed to tight
  self._figure.tight_layout(*args, **kwargs)
Text(0.5, 9.444444444444438, 'Life Expectancy of Birth(Year)')
<Figure size 800x600 with 0 Axes>

dfMeans=df.drop('Year',axis=1).groupby('Country').mean().reset_index()
dfMeans
Country	LEAPBY	GDP
0	Chile	78.94375	1.697888e+11
1	China	74.26250	4.957714e+12
2	Germany	79.65625	3.094776e+12
3	Mexico	75.71875	9.766506e+11
4	United States of America	78.06250	1.407500e+13
5	Zimbabwe	50.09375	9.062580e+09
plt.figure(figsize=(8,6))
sns.barplot(x='LEAPBY',y='Country',data=dfMeans)
plt.xlabel('Life Expectancy at birth (Years)')
Text(0.5, 0, 'Life Expectancy at birth (Years)')

plt.figure(figsize=(8,6))
sns.barplot(x='GDP',y='Country',data=dfMeans)
plt.xlabel('GDP in Trillion of US Dollars')
Text(0.5, 0, 'GDP in Trillion of US Dollars')

fig,axes=plt.subplots(1,2,sharey=True,figsize=(15,5))
axes[0]=sns.violinplot(ax=axes[0],x=df.GDP,y=df.Country)
axes[0].set_xlabel('GDP in Trillion of US Dollar')
axes[1]=sns.violinplot(ax=axes[1],x=df.LEAPBY,y=df.Country)
axes[1].set_xlabel('Life Expectancy at birth(Year)')
Text(0.5, 0, 'Life Expectancy at birth(Year)')

figs,axes=plt.subplots(1,2,sharey=True,figsize=(15,5))
axes[0]=sns.swarmplot(ax=axes[0],x=df.GDP,y=df.Country)
axes[0].set_xlabel('GDP in Trillion of US Dollars')
axes[1]=sns.swarmplot(ax=axes[1],x=df.LEAPBY,y=df.Country)
axes[1].set_xlabel('Life Expectancy at birth(Year)')
C:\Users\user\anaconda3\Lib\site-packages\seaborn\categorical.py:3544: UserWarning: 56.2% of the points cannot be placed; you may want to decrease the size of the markers or use stripplot.
  warnings.warn(msg, UserWarning)
C:\Users\user\anaconda3\Lib\site-packages\seaborn\categorical.py:3544: UserWarning: 56.2% of the points cannot be placed; you may want to decrease the size of the markers or use stripplot.
  warnings.warn(msg, UserWarning)
Text(0.5, 25.722222222222214, 'Life Expectancy at birth(Year)')

fig,axes=plt.subplots(1,2,sharey=True,figsize=(15,5))
axes[0]=sns.violinplot(ax=axes[0],x=df.GDP,y=df.Country,color='Black')
axes[0]=sns.swarmplot(ax=axes[0],x=df.GDP,y=df.Country)
axes[0].set_xlabel('GDP in Trillion of US Dollars')
axes[1]=sns.violinplot(ax=axes[1],x=df.LEAPBY,y=df.Country,color='Black')
axes[1]=sns.swarmplot(ax=axes[1],x=df.LEAPBY,y=df.Country)
axes[1].set_xlabel('Life Expectancy at Birth Year')
C:\Users\user\anaconda3\Lib\site-packages\seaborn\categorical.py:3544: UserWarning: 56.2% of the points cannot be placed; you may want to decrease the size of the markers or use stripplot.
  warnings.warn(msg, UserWarning)
C:\Users\user\anaconda3\Lib\site-packages\seaborn\categorical.py:3544: UserWarning: 56.2% of the points cannot be placed; you may want to decrease the size of the markers or use stripplot.
  warnings.warn(msg, UserWarning)
Text(0.5, 25.722222222222214, 'Life Expectancy at Birth Year')

plt.figure(figsize=(8,6))
sns.lineplot(x=df.Year,y=df.LEAPBY,hue=df.Country)
plt.legend(loc='center left',bbox_to_anchor=(1,0.5),ncol=1)
plt.ylabel('Life Expectancy at birth (Years)')
Text(0, 0.5, 'Life Expectancy at birth (Years)')

graphLEAPBY=sns.FacetGrid(df,col='Country',col_wrap=3,
                        hue='Country',sharey=False)
graphLEAPBY=(graphLEAPBY.map(sns.lineplot,'Year','LEAPBY')
                             .add_legend()
                             .set_axis_labels('Year','Life Expectancy of birth (Years)'))
graphLEAPBY
C:\Users\user\anaconda3\Lib\site-packages\seaborn\axisgrid.py:118: UserWarning: The figure layout has changed to tight
  self._figure.tight_layout(*args, **kwargs)
<seaborn.axisgrid.FacetGrid at 0x218117bfad0>

sns.scatterplot(x=df.LEAPBY,y=df.GDP,hue=df.Country).legend(loc='center left',bbox_to_anchor=(1,0.5),ncol=1)
<matplotlib.legend.Legend at 0x2180be57490>

graph=sns.FacetGrid(df,col='Country',col_wrap=3,hue='Country',sharey=False,sharex=False)
graph=(graph.map(sns.scatterplot,'LEAPBY','GDP')
      .add_legend()
      .set_axis_labels('Life Expectancy at Birth(Years)','GDP in Trillion US Dollar '))
C:\Users\user\anaconda3\Lib\site-packages\seaborn\axisgrid.py:118: UserWarning: The figure layout has changed to tight
  self._figure.tight_layout(*args, **kwargs)

This project was able to make quite a few data visualizations with the data even though there were only 96 rows and 4 columns. 
​
The project was also able to answer some of the questions posed in the beginning:
​
- Has life expectancy increased over time in the six nations?
    - Yes with Zimbabwe having the greatest increase.
- Has GDP increased over time in the six nations?
    - GDP has also increased for all countries in our list, especially for China.
- Is there a correlation between GDP and life expectancy of a country?
    - Yes there is a positive correlation between GDP and life expectancy for countries in our list.
- What is the average life expectancy in these nations?
    - Average life expectancy was between mid to high 70s for the countries except for Zimbabwe which was 50.
- What is the distribution of that life expectancy?
    - the life expectancy had a left skew, or most of the observations were on the right side.

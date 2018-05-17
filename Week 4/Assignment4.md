
# Assignment 4

Before working on this assignment please read these instructions fully. In the submission area, you will notice that you can click the link to **Preview the Grading** for each step of the assignment. This is the criteria that will be used for peer grading. Please familiarize yourself with the criteria before beginning the assignment.

This assignment requires that you to find **at least** two datasets on the web which are related, and that you visualize these datasets to answer a question with the broad topic of **weather phenomena** (see below) for the region of **Ann Arbor, Michigan, United States**, or **United States** more broadly.

You can merge these datasets with data from different regions if you like! For instance, you might want to compare **Ann Arbor, Michigan, United States** to Ann Arbor, USA. In that case at least one source file must be about **Ann Arbor, Michigan, United States**.

You are welcome to choose datasets at your discretion, but keep in mind **they will be shared with your peers**, so choose appropriate datasets. Sensitive, confidential, illicit, and proprietary materials are not good choices for datasets for this assignment. You are welcome to upload datasets of your own as well, and link to them using a third party repository such as github, bitbucket, pastebin, etc. Please be aware of the Coursera terms of service with respect to intellectual property.

Also, you are welcome to preserve data in its original language, but for the purposes of grading you should provide english translations. You are welcome to provide multiple visuals in different languages if you would like!

As this assignment is for the whole course, you must incorporate principles discussed in the first week, such as having as high data-ink ratio (Tufte) and aligning with Cairo’s principles of truth, beauty, function, and insight.

Here are the assignment instructions:

 * State the region and the domain category that your data sets are about (e.g., **Ann Arbor, Michigan, United States** and **weather phenomena**).
 * You must state a question about the domain category and region that you identified as being interesting.
 * You must provide at least two links to available datasets. These could be links to files such as CSV or Excel files, or links to websites which might have data in tabular form, such as Wikipedia pages.
 * You must upload an image which addresses the research question you stated. In addition to addressing the question, this visual should follow Cairo's principles of truthfulness, functionality, beauty, and insightfulness.
 * You must contribute a short (1-2 paragraph) written justification of how your visualization addresses your stated research question.

What do we mean by **weather phenomena**?  For this category you might want to consider seasonal changes, natural disasters, or historical trends.

## Tips
* Wikipedia is an excellent source of data, and I strongly encourage you to explore it for new data sources.
* Many governments run open data initiatives at the city, region, and country levels, and these are wonderful resources for localized data sources.
* Several international agencies, such as the [United Nations](http://data.un.org/), the [World Bank](http://data.worldbank.org/), the [Global Open Data Index](http://index.okfn.org/place/) are other great places to look for data.
* This assignment requires you to convert and clean datafiles. Check out the discussion forums for tips on how to do this from various sources, and share your successes with your fellow students!

## Example
Looking for an example? Here's what our course assistant put together for the **Ann Arbor, MI, USA** area using **sports and athletics** as the topic. [Example Solution File](./readonly/Assignment4_example.pdf)


```python
import pandas as pd
```

# importing Thunder data and cleaning it

Data source: https://en.wikipedia.org/wiki/List_of_Oklahoma_City_Thunder_seasons


```python
thunder = pd.read_excel("thunder.xlsx")

thunder.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Season</th>
      <th>Team</th>
      <th>Conference</th>
      <th>Conf.</th>
      <th>Division</th>
      <th>Div.</th>
      <th>Wins</th>
      <th>Losses</th>
      <th>Win%</th>
      <th>GB</th>
      <th>Playoffs</th>
      <th>Awards</th>
      <th>Head coach</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Finish</td>
      <td>NaN</td>
      <td>Finish</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1967–68</td>
      <td>1967–68[b]</td>
      <td>—</td>
      <td>—</td>
      <td>Western</td>
      <td>5th</td>
      <td>23.0</td>
      <td>59.0</td>
      <td>0.280</td>
      <td>33</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Al Bianchi</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1968–69</td>
      <td>1968–69</td>
      <td>—</td>
      <td>—</td>
      <td>Western</td>
      <td>6th</td>
      <td>30.0</td>
      <td>52.0</td>
      <td>0.366</td>
      <td>25</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Al Bianchi</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1969–70</td>
      <td>1969–70</td>
      <td>—</td>
      <td>—</td>
      <td>Western</td>
      <td>5th</td>
      <td>36.0</td>
      <td>46.0</td>
      <td>0.439</td>
      <td>12</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Lenny Wilkens</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1970–71</td>
      <td>1970–71</td>
      <td>Western</td>
      <td>8th</td>
      <td>Pacific</td>
      <td>4th</td>
      <td>38.0</td>
      <td>44.0</td>
      <td>0.463</td>
      <td>10</td>
      <td>NaN</td>
      <td>Lenny Wilkens</td>
      <td>Lenny Wilkens</td>
    </tr>
  </tbody>
</table>
</div>




```python
thunder = thunder.iloc[1:]
```


```python
thunder = thunder[['Season', 'Win%']]
```


```python
thunder.dropna(inplace= True)
```


```python
def yearchange(year):
    return year[:4]
```


```python
thunder['Season'] = thunder['Season'].apply(yearchange)
```


```python
thunder.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Season</th>
      <th>Win%</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1967</td>
      <td>0.280</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1968</td>
      <td>0.366</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1969</td>
      <td>0.439</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1970</td>
      <td>0.463</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1971</td>
      <td>0.537</td>
    </tr>
  </tbody>
</table>
</div>



# Importing Ou Sooners data and cleaning it

data source: https://en.wikipedia.org/wiki/List_of_Oklahoma_Sooners_football_seasons


```python
sooners = pd.read_excel("Sooners.xlsx")
```


```python
sooners.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Season</th>
      <th>Head coach</th>
      <th>Conference</th>
      <th>Season results</th>
      <th>Unnamed: 4</th>
      <th>Wins</th>
      <th>Losses</th>
      <th>Ties</th>
      <th>Bowl result</th>
      <th>Final ranking</th>
      <th>Unnamed: 10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1895</td>
      <td>John A. Harts</td>
      <td>Independent</td>
      <td>—</td>
      <td>—</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>—</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1896</td>
      <td>No coach</td>
      <td>Independent</td>
      <td>—</td>
      <td>—</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>—</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1897</td>
      <td>Vernon L. Parrington</td>
      <td>Independent</td>
      <td>—</td>
      <td>—</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>—</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1898</td>
      <td>NaN</td>
      <td>Independent</td>
      <td>—</td>
      <td>—</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>—</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1899</td>
      <td>NaN</td>
      <td>Independent</td>
      <td>—</td>
      <td>—</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>—</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
sooners= sooners[['Season', 'Wins', 'Losses', 'Ties']]
```


```python
sooners.dropna(inplace= True)
```


```python
def changeties(row):
    if isinstance(row, int):
        return row
    else:
        return 0
```


```python
sooners['Ties'] = sooners['Ties'].apply(changeties)
```


```python
def win(row):
    return (row['Wins'] + 0.5*row['Ties'])/(row['Wins'] + row['Ties'] + row['Losses'])
```


```python
sooners['Win%'] = sooners.apply(lambda row: win(row),axis=1)
```


```python
sooners = sooners.loc[72:]
```


```python
sooners['Season'] = sooners['Season'].astype(str)
```


```python
sooners['Season'] = sooners['Season'].apply(yearchange)
```


```python
sooners = sooners[['Season', 'Win%']]
```

# Plotting


```python
import matplotlib.pyplot as plt

import seaborn as sns

%matplotlib inline
```


```python
plt.figure(num=None, figsize=(14, 10), dpi=80)


plt.plot(sooners['Season'], sooners['Win%'], color = 'red', label = 'OU Sooners', alpha = 0.5, linewidth = 5)
plt.plot(thunder['Season'], thunder['Win%'], color = 'blue', label = 'OKC Thunder',alpha = 0.5, linewidth = 5)
plt.ylim(0, 1)


plt.ylabel('Win %')
plt.xlabel('Season')
plt.title('Major Oklahoma Sport teams Win% over time')

# legend    
legend = plt.legend(loc='upper right', shadow=False, frameon = True, fontsize = 15)

# remove the frame of the chart
for spine in plt.gca().spines.values():
    spine.set_visible(False)
    
# Hide grid lines
plt.grid(False)

# grid lines
plt.grid(linestyle= 'dashed', linewidth=0.5, axis = 'y')    

plt.text(1970, 0.2, r'Win% = Games Won/Total Games', bbox=dict(facecolor='black', alpha=0.1), fontsize = 20)
    

sns.set_style("whitegrid")    
    
plt.show()
```

    /opt/conda/lib/python3.5/site-packages/matplotlib/font_manager.py:1297: UserWarning: findfont: Font family ['sans-serif'] not found. Falling back to DejaVu Sans
      (prop.get_family(), self.defaultFamily[fontext]))



![png](output_27_1.png)



```python

```

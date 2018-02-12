
#Heros of Pymoli

Your final report should include each of the following:

**Player Count**

* Total Number of Players

**Purchasing Analysis (Total)**

* Number of Unique Items
* Average Purchase Price
* Total Number of Purchases
* Total Revenue

**Gender Demographics**

* Percentage and Count of Male Players
* Percentage and Count of Female Players
* Percentage and Count of Other / Non-Disclosed

**Purchasing Analysis (Gender)** 

* The below each broken by gender
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Normalized Totals

**Age Demographics**

* The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.) 
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Normalized Totals

**Top Spenders**

* Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
  * SN
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value

**Most Popular Items**

* Identify the 5 most popular items by purchase count, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value

**Most Profitable Items**

* Identify the 5 most profitable items by total purchase value, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value

As final considerations:

* Your script must work for both data-sets given.
* You must use the Pandas Library and the Jupyter Notebook.
* You must submit a link to your Jupyter Notebook with the viewable Data Frames. 
* You must include an exported markdown version of your Notebook called  `README.md` in your GitHub repository.  
* You must include a written description of three observable trends based on the data. 
* See [Example Solution](HeroesOfPymoli/HeroesOfPymoli_Example.pdf) for a reference on expected format. 


```python
import pandas as pd
import numpy as np
import json as js
```


```python
#open CSV file
userinput = input('Please enter which file you want to read, purchase_data.json or purchase_data2.json.')
csv_path = userinput
```

    Please enter which file you want to read, purchase_data.json or purchase_data2.json.purchase_data2.json



```python
df = pd.read_json(csv_path)
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>



## Player Count


```python
#Total Number of Players
a = df["SN"].unique()
Tp = {'Total Players':[len(a)]}
Tp1 = pd.DataFrame(Tp)
Tp1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>74</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Total)


```python
#Number of Unique Items


#Total Revenue
i = df["Item ID"].unique()
print("Number of Unique Items")
items = len(i)
items
```

    Number of Unique Items





    64




```python
#Average Purchase Price
ap = round(df["Price"].mean(),2)
ap
```




    2.92




```python
#Total Number of Purchases
p = df["Item ID"].count()
p
```




    78




```python
#Total Revenue
Revenue = round(df["Price"].sum(),2)
Revenue
```




    228.1




```python
PurchaseAna = {'Number of Unique Items': [items], 'Average Purchase Price': [ap],'Total Number of Purchases': [p],"Total Revenue"
              : Revenue}
PA = pd.DataFrame(PurchaseAna)
PA 
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Number of Unique Items</th>
      <th>Total Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2.92</td>
      <td>64</td>
      <td>78</td>
      <td>228.1</td>
    </tr>
  </tbody>
</table>
</div>



## Gender Demographics


```python
#Percentage and Count of Male Players
# Percentage and Count of Female Players
#Percentage and Count of Other / Non-Disclosed
```


```python
total_gender = df["Gender"].count()
male = df["Gender"].value_counts()['Male']
female = df["Gender"].value_counts()['Female']
non_gender_specific = total_gender - male - female
```


```python
male_percent = round((male/total_gender) * 100,2)
female_percent = round((female/total_gender) * 100,2)
non_gender_specific_percent = round((non_gender_specific/total_gender) * 100,2)
```


```python
gender_Count = {'Male': [male], 'Female': [female],'Non-Disclosed': [non_gender_specific]}
geneder_Percent = {'Male': [male_percent], 'Female': [female_percent],'Non-Disclosed': [non_gender_specific_percent]}
gcount = pd.DataFrame(gender_Count)
gpercent = pd.DataFrame(geneder_Percent)
```


```python
male_player = {'Population': "Male",'Count': [male], 'Percent': [male_percent]}
Female_Player = {'Population': "Female", 'Count': [female], 'Percent': [female_percent]}
non_player = {'Population': "Non-Disclosed", 'Count': [non_gender_specific], 'Percent': [non_gender_specific_percent]}
combined = pd.DataFrame(male_player,Female_Player)
male_player_df = pd.DataFrame(male_player)
female_player_df = pd.DataFrame(Female_Player)
non_df = pd.DataFrame(non_player)
pd.concat([male_player_df,female_player_df,non_df],ignore_index=True)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Count</th>
      <th>Percent</th>
      <th>Population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>64</td>
      <td>82.05</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13</td>
      <td>16.67</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>1.28</td>
      <td>Non-Disclosed</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Gender)

The below each broken by gender
Purchase Count
Average Purchase Price
Total Purchase Value
Normalized Totals


```python
gen = df.groupby('Gender')
id_count = gen["Item ID"].count()
price_mean= round(gen["Price"].mean(),2)
total_purchase = gen["Price"].sum()
norm_price = round(total_purchase/id_count,2)
```


```python
combined = pd.DataFrame({"Purchase Count": id_count, "Average Purchase Price": price_mean, "Total Purchase Value":total_purchase,
                         "Normalized Totals": norm_price})
```


```python
combined
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Normalized Totals</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>3.18</td>
      <td>3.18</td>
      <td>13</td>
      <td>41.38</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2.88</td>
      <td>2.88</td>
      <td>64</td>
      <td>184.60</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>2.12</td>
      <td>2.12</td>
      <td>1</td>
      <td>2.12</td>
    </tr>
  </tbody>
</table>
</div>



## Age Demographics


The below each broken into bins of 4 years (i.e. <10, 10-14, 15-19, etc.)
Purchase Count
Average Purchase Price
Total Purchase Value
Normalized Totals


```python
bins = [0,10,15,20,25,30,35,40]
names = ['<10','10-14','15-19','20-24','25-29','30-34','35-40']
pd.cut(df["Age"], bins, labels=names)
```




    0     15-19
    1     20-24
    2     15-19
    3     15-19
    4     20-24
    5       <10
    6     35-40
    7     25-29
    8     15-19
    9     35-40
    10    20-24
    11    35-40
    12    15-19
    13    30-34
    14      <10
    15    20-24
    16    20-24
    17      <10
    18    10-14
    19    20-24
    20    30-34
    21    10-14
    22    15-19
    23    15-19
    24    20-24
    25    15-19
    26      <10
    27    20-24
    28    15-19
    29    20-24
          ...  
    48    20-24
    49    15-19
    50    20-24
    51    25-29
    52    20-24
    53    15-19
    54    20-24
    55    15-19
    56    15-19
    57    20-24
    58    25-29
    59    35-40
    60    20-24
    61    20-24
    62    15-19
    63    10-14
    64    20-24
    65    20-24
    66    20-24
    67    20-24
    68    20-24
    69    30-34
    70    20-24
    71    20-24
    72    20-24
    73    30-34
    74    35-40
    75    10-14
    76    20-24
    77    15-19
    Name: Age, Length: 78, dtype: category
    Categories (7, object): [<10 < 10-14 < 15-19 < 20-24 < 25-29 < 30-34 < 35-40]




```python
df["Age_Group"] = pd.cut(df["Age"], bins, labels=names)
```


```python
Age_df = df.groupby('Age_Group')
item = Age_df["Item ID"].count()
avg_p = Age_df["Price"].mean().round(2)
total_p = Age_df["Price"].sum()
normal_p = (total_p/item).round(2)
```


```python
player = Age_df["SN"].unique()
players = [len(x) for x in player]
players_perc = (players/(df["SN"].count()))*100
player_df = pd.DataFrame({"Total Count": players, "Players Percentage": players_perc.round(2)})
play_df = (player_df)
play_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Players Percentage</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6.41</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5.13</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>25.64</td>
      <td>20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>38.46</td>
      <td>30</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.13</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7.69</td>
      <td>6</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6.41</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
item_df = pd.DataFrame({"Purchase Count": item, "Average Purchase Price": avg_p, 
                        "Total Purchase Value": total_p, "Normalized Totals": normal_p})
items_df = (item_df)
items_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Normalized Totals</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Age_Group</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>2.76</td>
      <td>2.76</td>
      <td>5</td>
      <td>13.82</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>3.05</td>
      <td>3.05</td>
      <td>4</td>
      <td>12.21</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>2.73</td>
      <td>2.73</td>
      <td>20</td>
      <td>54.69</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>3.04</td>
      <td>3.04</td>
      <td>33</td>
      <td>100.42</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>2.69</td>
      <td>2.69</td>
      <td>4</td>
      <td>10.77</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>2.35</td>
      <td>2.35</td>
      <td>7</td>
      <td>16.47</td>
    </tr>
    <tr>
      <th>35-40</th>
      <td>3.94</td>
      <td>3.94</td>
      <td>5</td>
      <td>19.72</td>
    </tr>
  </tbody>
</table>
</div>



## Top Spenders

Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
SN
Purchase Count
Average Purchase Price
Total Purchase Value


```python
SN = df.groupby('SN')
id_count = SN["Item ID"].count()
price_Avg= round(SN["Price"].mean(),2)
total_purchase = SN["Price"].sum()
top_spend = pd.DataFrame({"Purchase Count": id_count, "Average Purchase Price": price_Avg, 
                        "Total Purchase Value": total_purchase})
top_s = (top_spend)
top_5 = top_s.sort_values(by="Total Purchase Value", ascending=False)
top_5.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Sundaky74</th>
      <td>3.70</td>
      <td>2</td>
      <td>7.41</td>
    </tr>
    <tr>
      <th>Aidaira26</th>
      <td>2.56</td>
      <td>2</td>
      <td>5.13</td>
    </tr>
    <tr>
      <th>Eusty71</th>
      <td>4.81</td>
      <td>1</td>
      <td>4.81</td>
    </tr>
    <tr>
      <th>Chanirra64</th>
      <td>4.78</td>
      <td>1</td>
      <td>4.78</td>
    </tr>
    <tr>
      <th>Alarap40</th>
      <td>4.71</td>
      <td>1</td>
      <td>4.71</td>
    </tr>
  </tbody>
</table>
</div>



## Most Popular Items

Identify the 5 most popular items by purchase count, then list (in a table):
Item ID
Item Name
Purchase Count
Item Price
Total Purchase Value


```python
itemsPop = df.groupby('Item ID')
item_name = itemsPop["Item Name"].unique()
ID = itemsPop["Item ID"].unique()
id_counts = itemsPop["Item ID"].count()
prices = round(itemsPop["Price"].mean(),2)
total_pur = itemsPop["Price"].sum()
Pop_items = pd.DataFrame({"Item ID": ID, "Item Name": item_name, "Purchase Count": id_counts, "Average Purchase Price": prices, 
                        "Total Purchase Value": total_pur})
top_pop = (Pop_items)
top_items = top_pop.sort_values(by="Purchase Count", ascending=False)
top_items.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>94</th>
      <td>3.64</td>
      <td>[94]</td>
      <td>[Mourning Blade]</td>
      <td>3</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>90</th>
      <td>4.12</td>
      <td>[90]</td>
      <td>[Betrayer]</td>
      <td>2</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>111</th>
      <td>1.79</td>
      <td>[111]</td>
      <td>[Misery's End]</td>
      <td>2</td>
      <td>3.58</td>
    </tr>
    <tr>
      <th>64</th>
      <td>2.42</td>
      <td>[64]</td>
      <td>[Fusion Pummel]</td>
      <td>2</td>
      <td>4.84</td>
    </tr>
    <tr>
      <th>154</th>
      <td>4.11</td>
      <td>[154]</td>
      <td>[Feral Katana]</td>
      <td>2</td>
      <td>8.22</td>
    </tr>
  </tbody>
</table>
</div>



## Most Profitable Items

Identify the 5 most profitable items by total purchase value, then list (in a table):
Item ID
Item Name
Purchase Count
Item Price
Total Purchase Value


```python
itemsProf = df.groupby('Item ID')
item_name_p = itemsProf["Item Name"].unique()
ID_p = itemsProf["Item ID"].unique()
id_counts_p = itemsProf["Item ID"].count()
prices_p = round(itemsProf["Price"].mean(),2)
total_pur_p = itemsProf["Price"].sum()
Prof_items_p = pd.DataFrame({"Item ID": ID_p, "Item Name": item_name_p, "Purchase Count": id_counts_p, 
                          "Average Purchase Price": prices_p, 
                        "Total Purchase Value": total_pur_p})
top_prof = (Prof_items_p)
top_prof = top_prof.sort_values(by="Total Purchase Value", ascending=False)
top_prof.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>94</th>
      <td>3.64</td>
      <td>[94]</td>
      <td>[Mourning Blade]</td>
      <td>3</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>117</th>
      <td>4.71</td>
      <td>[117]</td>
      <td>[Heartstriker, Legacy of the Light]</td>
      <td>2</td>
      <td>9.42</td>
    </tr>
    <tr>
      <th>93</th>
      <td>4.49</td>
      <td>[93]</td>
      <td>[Apocalyptic Battlescythe]</td>
      <td>2</td>
      <td>8.98</td>
    </tr>
    <tr>
      <th>90</th>
      <td>4.12</td>
      <td>[90]</td>
      <td>[Betrayer]</td>
      <td>2</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>154</th>
      <td>4.11</td>
      <td>[154]</td>
      <td>[Feral Katana]</td>
      <td>2</td>
      <td>8.22</td>
    </tr>
  </tbody>
</table>
</div>



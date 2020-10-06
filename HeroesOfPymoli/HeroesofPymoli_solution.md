#Heroes of Pymoli Solution
```python
# Modules
import pandas as pd
import numpy as np
```


```python
#set path for file
file="Resources/purchase_data.csv"
```


```python
#Read data file with pandas library
file_df=pd.read_csv(file)
file_df.head()
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Find the total number of rows in the dataframe
index=file_df.index
totalrows=len(index)
print(totalrows)
```

    780
    


```python
#find the total number of players
total_players=len(file_df["SN"].value_counts())
total_players
```




    576


# Player Count

```python
#Create a date frame for the total number of players
number_of_players=pd.DataFrame({"Total Players":[total_players]})
number_of_players
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
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>




```python
#find the number of unique items, average price, number of purchases, and total revenue
total_uitems=len(file_df["Item ID"].unique())
total_uitems
avg_price=round(file_df["Price"].mean(),2)
avg_price
total_purchases=(file_df["Purchase ID"].count())
total_purchases
total_revenue=(file_df["Price"].sum())
```

```python
#put above data in a dataframe
summary_df=pd.DataFrame({"Number of Unique Items": [total_uitems], "Average Price": [avg_price], "Number of Purchases":[total_purchases], "Total Revenue":[total_revenue]})
```

# Purchase Analysis (Total)
```python
#format the summary table using currency
summary_df.style.format({'Average Price':"${:,.2f}",
                         'Total Revenue': "${:,.2f}"})
summary_df.head()
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
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>179</td>
      <td>3.05</td>
      <td>780</td>
      <td>2379.77</td>
    </tr>
  </tbody>
</table>
</div>



# Gender Demographics
```python
#Gender Demographics

#Total count without repeating SN's
totalcount = file_df["SN"].nunique()

#filter by male, female and other
males = file_df[file_df["Gender"] == "Male"]["SN"].nunique()
females = file_df[file_df["Gender"] == "Female"]["SN"].nunique()
other = totalcount - males - females

#find percentages using calculation
maleperc = ((males/totalcount)*100)
femaleperc = ((females/totalcount)*100)
otherperc = ((other/totalcount)*100)

#Create the dataframe
gender_demo_df = pd.DataFrame({"Gender": ["Male", "Female", "Other / Non-Disclosed"], "Percentage of Players": [maleperc, femaleperc, otherperc],
                                        "Total Count": [males, females, other]}, columns = 
                                        ["Gender", "Percentage of Players", "Total Count"])
#Remove the index numbers in the DF                                        
gender_demo = gender_demo_df.set_index("Gender")

#format the Perecentages
gender_demo.style.format({"Percentage of Players": "{:.2f}%"})

gender_demo.head()

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
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>84.027778</td>
      <td>484</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>14.062500</td>
      <td>81</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.909722</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>



# Purchase Analysis (Gender)
```python
#Purchasing Analysis

#Find purchase count, average purchase price, total purchase value, and avg total purchase per person

#total purchases by filtering and .count function
totalFEMpurchase = file_df[file_df["Gender"] == "Female"]["Price"].count()
totalMALEpurchase = file_df[file_df["Gender"] == "Male"]["Price"].count()
totalOTHpurchase = file_df[file_df["Gender"] == "Other / Non-Disclosed"]['Price'].count()

#avg purchase price
avgFEMpurchase = file_df[file_df["Gender"] == "Female"]["Price"].mean()
avgMALEpurchase = file_df[file_df["Gender"] == "Male"]["Price"].mean()
avgOTHpurchase = file_df[file_df["Gender"] == "Other / Non-Disclosed"]['Price'].mean()

#total purchase value
sum_female = file_df[file_df["Gender"] == "Female"]["Price"].sum()
sum_males = file_df[file_df["Gender"] == "Male"]["Price"].sum()
sum_other = file_df[file_df["Gender"] == "Other / Non-Disclosed"]['Price'].sum()

#average total purchase per person
avgtotalFEM = sum_female/females
avgtotalMALE = sum_males/males
avgtotalOTH = sum_other/other

#stick it in a DF
purchase_analysis_df = pd.DataFrame ({"Gender":["Female", "Male", "Other/Non-Disclosed"], "Purchase Count":[totalFEMpurchase, totalMALEpurchase, totalOTHpurchase],
                                     "Average Purchase Price":[avgFEMpurchase, avgMALEpurchase,avgOTHpurchase],
                                     "Total Purchase Value":[sum_female, sum_males, sum_other],
                                     "Average Total Purchase Per Person":[avgtotalFEM, avgtotalMALE, avgtotalOTH]}, 
                                     columns = ["Gender", "Purchase Count", "Average Purchase Price", "Total Purchase Value", "Average Total Purchase Per Person"])

#set index
purchase_analy = purchase_analysis_df.set_index("Gender")

#format the columns
purchase_analy.style.format({"Average Purchase Price": "${:.2f}", "Total Purchase Value": "${:,.2f}", "Average Total Purchase Per Person": "${:.2f}"})

purchase_analy
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Average Total Purchase Per Person</th>
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
      <td>113</td>
      <td>3.203009</td>
      <td>361.94</td>
      <td>4.468395</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>652</td>
      <td>3.017853</td>
      <td>1967.64</td>
      <td>4.065372</td>
    </tr>
    <tr>
      <th>Other/Non-Disclosed</th>
      <td>15</td>
      <td>3.346000</td>
      <td>50.19</td>
      <td>4.562727</td>
    </tr>
  </tbody>
</table>
</div>


# Age Demographics

```python
#age demographics

#find the min and max age of the data
maxage=file_df["Age"].max()
minage=file_df["Age"].min()

#create bins for age
bins = [0, 9.9, 14.9, 19.9, 24.9, 29.9, 34.9, 39.9, 100]

#Create labels for the bins
bin_groups = ["<10", "10-14", "15-19", "20-24","25-29", "30-34", "35-39", "40+"]

#categorize existing players
file_df["Age Summary"]=pd.cut(file_df["Age"], bins, labels=bin_groups)
file_df.head()

#group the data by age groups
grouped_ages=file_df.groupby(["Age Summary"])

#count players only once
grouped_count= grouped_ages["SN"].nunique()

#find percentages
age_percentage = grouped_count/total_players*100
age_percentage

#create a dataframe with the results

age_demographics_df = pd.DataFrame ({"Total Count": grouped_count,
                                    "Percentage of Players": age_percentage})
age_demographics_df['Percentage of Players']= age_demographics_df['Percentage of Players'].astype(float).map("{:.2f}%".format)

age_demographics_df
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
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Age Summary</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>17</td>
      <td>2.95%</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>22</td>
      <td>3.82%</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>107</td>
      <td>18.58%</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>258</td>
      <td>44.79%</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>77</td>
      <td>13.37%</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>52</td>
      <td>9.03%</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>31</td>
      <td>5.38%</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>12</td>
      <td>2.08%</td>
    </tr>
  </tbody>
</table>
</div>



# Purchase Analysis (Age)
```python
#Purchase Analysis by age 

#bin the purchase_data file by age

#Calculations to find Purchase Count, Avg Purchase Price, Purchase Total per Person
PC = grouped_ages["Purchase ID"].count()
APPA = grouped_ages["Price"].mean()
TPV = grouped_ages["Price"].sum()
ATPPP = TPV/grouped_count

#create a summary df
Purchase_Analysis_Age = pd.DataFrame ({"Purchase Count": PC, 
                                       "Average Purchase Price": APPA, 
                                       "Total Purchase Value": TPV, 
                                       "Avg Total Purchase Per Person":ATPPP})
Purchase_Analysis_Age['Average Purchase Price']= Purchase_Analysis_Age['Average Purchase Price'].astype(float).map("${:.2f}".format)
Purchase_Analysis_Age['Total Purchase Value']= Purchase_Analysis_Age['Total Purchase Value'].astype(float).map("${:,.2f}".format)
Purchase_Analysis_Age['Avg Total Purchase Per Person']= Purchase_Analysis_Age['Avg Total Purchase Per Person'].astype(float).map("${:,.2f}".format)
Purchase_Analysis_Age
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase Per Person</th>
    </tr>
    <tr>
      <th>Age Summary</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>23</td>
      <td>$3.35</td>
      <td>$77.13</td>
      <td>$4.54</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>28</td>
      <td>$2.96</td>
      <td>$82.78</td>
      <td>$3.76</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
      <td>$3.04</td>
      <td>$412.89</td>
      <td>$3.86</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
      <td>$3.05</td>
      <td>$1,114.06</td>
      <td>$4.32</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
      <td>$2.90</td>
      <td>$293.00</td>
      <td>$3.81</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
      <td>$2.93</td>
      <td>$214.00</td>
      <td>$4.12</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
      <td>$3.60</td>
      <td>$147.67</td>
      <td>$4.76</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
      <td>$2.94</td>
      <td>$38.24</td>
      <td>$3.19</td>
    </tr>
  </tbody>
</table>
</div>



# Top Spenders
```python
#Top Spenders

#group the file by SN 
baller_stats = file_df.groupby("SN")

#total purchases by name
big_baller_count = baller_stats["Purchase ID"].count()

#avg purchase by SN
big_baller_price = baller_stats["Price"].mean()

#total purchase value by SN
big_baller_TPV = baller_stats["Price"].sum()

#create a dataframe and sort the list 
Top_Spenders_df = pd.DataFrame({"Purchase Count": big_baller_count, 
                                "Average Purchase Price": big_baller_price, 
                                "Total Purchase Value": big_baller_TPV})
sorted_Top_Spenders = Top_Spenders_df.sort_values(["Total Purchase Value"], ascending = False).head()

sorted_Top_Spenders['Average Purchase Price']= sorted_Top_Spenders['Average Purchase Price'].astype(float).map("${:.2f}".format)
sorted_Top_Spenders['Total Purchase Value']= sorted_Top_Spenders['Total Purchase Value'].astype(float).map("${:,.2f}".format)
sorted_Top_Spenders
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
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
      <th>Lisosia93</th>
      <td>5</td>
      <td>$3.79</td>
      <td>$18.96</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>4</td>
      <td>$3.86</td>
      <td>$15.45</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>3</td>
      <td>$4.61</td>
      <td>$13.83</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>4</td>
      <td>$3.40</td>
      <td>$13.62</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>3</td>
      <td>$4.37</td>
      <td>$13.10</td>
    </tr>
  </tbody>
</table>
</div>



# Most Popular Items
```python
#Most popular items

popular_items = file_df[["Item ID", "Item Name", "Price"]]
popular_items = popular_items.set_index(["Item ID", "Item Name"])
popular_items = popular_items.groupby(["Item ID", "Item Name"])

popular_items.head()


#calculations

popular_items_count = popular_items["Price"].count()

popular_items_total = popular_items["Price"].sum()

popular_items_avg = popular_items_total / popular_items_count

#dataframe

popular_items_df = pd.DataFrame({"Purchase Count": popular_items_count, 
                                "Item Price": popular_items_avg,
                                "Total Purchase Value": popular_items_total})

sorted_popular_items = popular_items_df.sort_values(["Purchase Count"], ascending = False).head()

sorted_popular_items["Item Price"]= sorted_popular_items["Item Price"].astype(float).map("${:.2f}".format)
sorted_popular_items['Total Purchase Value']= sorted_popular_items['Total Purchase Value'].astype(float).map("${:,.2f}".format)

sorted_popular_items
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
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>92</th>
      <th>Final Critic</th>
      <td>13</td>
      <td>$4.61</td>
      <td>$59.99</td>
    </tr>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>132</th>
      <th>Persuasion</th>
      <td>9</td>
      <td>$3.22</td>
      <td>$28.99</td>
    </tr>
    <tr>
      <th>108</th>
      <th>Extraction, Quickblade Of Trembling Hands</th>
      <td>9</td>
      <td>$3.53</td>
      <td>$31.77</td>
    </tr>
  </tbody>
</table>
</div>


# Most Profitable Items

```python
#Most Profitable Items

sorted_popular_items_TPV = popular_items_df.sort_values (["Total Purchase Value"], ascending = False).head()

sorted_popular_items_TPV

sorted_popular_items_TPV["Item Price"]= sorted_popular_items_TPV["Item Price"].astype(float).map("${:.2f}".format)
sorted_popular_items_TPV['Total Purchase Value']= sorted_popular_items_TPV['Total Purchase Value'].astype(float).map("${:,.2f}".format)

sorted_popular_items_TPV
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
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>92</th>
      <th>Final Critic</th>
      <td>13</td>
      <td>$4.61</td>
      <td>$59.99</td>
    </tr>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>8</td>
      <td>$4.35</td>
      <td>$34.80</td>
    </tr>
  </tbody>
</table>
</div>



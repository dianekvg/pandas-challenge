
# Heroes of Pymoli Sales Analysis
==================================================


```python
import pandas as pd
import os
```


```python
#load (2) JSON; view file 1 headers
json_path1 = os.path.join("Resources","purchase_data.json")
json_path2 = os.path.join("Resources","purchase_data2.json")
pd1 = pd.read_json(json_path1)
pd2 = pd.read_json(json_path2)
pd1.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Get row count - file 1
pd1_totrows = pd1['SN'].count()
print (pd1_totrows)
```

    780
    


```python
#Check columns - file 1
pd1.columns
```




    Index(['Age', 'Gender', 'Item ID', 'Item Name', 'Price', 'SN'], dtype='object')




```python
#View file 2 headers
pd2.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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




```python
#Get row count - file 2
pd2_totrows = pd2['SN'].count()
print (pd2_totrows)
```

    78
    


```python
#Check columns - file 2
pd2.columns
```




    Index(['Age', 'Gender', 'Item ID', 'Item Name', 'Price', 'SN'], dtype='object')




```python
#Get total rows - both files
total_rows = pd1_totrows + pd2_totrows
print (total_rows)
```

    858
    


```python
#Union 2 files; view headers
files = [pd1, pd2]
allsales = pd.concat(files)
allsales.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Get row count - all sales
allsales_totrows = allsales['SN'].count()
print (allsales_totrows)
```

    858
    


```python
#Set age bins
allsales['Age Group'] = "<10"
allsales['Age Group'][allsales['Age'] > 9] = '10-14'
allsales['Age Group'][allsales['Age'] > 14] = '15-19'
allsales['Age Group'][allsales['Age'] > 19] = '20-24'
allsales['Age Group'][allsales['Age'] > 24] = '25-29'
allsales['Age Group'][allsales['Age'] > 29] = '30-34'
allsales['Age Group'][allsales['Age'] > 34] = '35-39'
allsales['Age Group'][allsales['Age'] > 39] = '40+'
index = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]
```

    C:\Users\Diane\Anaconda3\lib\site-packages\ipykernel_launcher.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      This is separate from the ipykernel package so we can avoid doing imports until
    C:\Users\Diane\Anaconda3\lib\site-packages\ipykernel_launcher.py:4: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      after removing the cwd from sys.path.
    C:\Users\Diane\Anaconda3\lib\site-packages\ipykernel_launcher.py:5: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      """
    C:\Users\Diane\Anaconda3\lib\site-packages\ipykernel_launcher.py:6: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    C:\Users\Diane\Anaconda3\lib\site-packages\ipykernel_launcher.py:7: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      import sys
    C:\Users\Diane\Anaconda3\lib\site-packages\ipykernel_launcher.py:8: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    C:\Users\Diane\Anaconda3\lib\site-packages\ipykernel_launcher.py:9: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      if __name__ == '__main__':
    


```python
#Check columns - all sales
allsales.columns
```




    Index(['Age', 'Gender', 'Item ID', 'Item Name', 'Price', 'SN', 'Age Group'], dtype='object')




```python
#Get total sales
totsales = allsales['Price'].sum()
print (totsales)
```

    2514.4299999999967
    

# Player Count


```python
#Total number of players
pc = {'Total Players': [allsales['SN'].nunique()]}
playercount = pd.DataFrame(data=pc)
playercount
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>612</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis - Totals


```python
#Number of Unique Items, Average Purchase Price, Total Number of Purchases, Total Revenue
pa = {'Number of Unique Items':[allsales['Item ID'].nunique()],'Average Purchase Price':[allsales['Price'].mean()],'Total Number of Purchases':[allsales['SN'].count()],'Total Revenue':[allsales['Price'].sum()]}
purchasinganalysis = pd.DataFrame(data=pa)
purchasinganalysis['Average Purchase Price'] = purchasinganalysis['Average Purchase Price'].map('${:,.2f}'.format)
purchasinganalysis['Total Revenue'] = purchasinganalysis['Total Revenue'].map('${:,.2f}'.format)
purchasinganalysis = purchasinganalysis[['Number of Unique Items', 'Average Purchase Price', 'Total Number of Purchases', 'Total Revenue']]
purchasinganalysis
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average Purchase Price</th>
      <th>Total Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>184</td>
      <td>$2.93</td>
      <td>858</td>
      <td>$2,514.43</td>
    </tr>
  </tbody>
</table>
</div>



# Gender Demographics


```python
#Percentage and Count of Male, Female, Other/Non-Disclosed Players
allbuyers = allsales.drop_duplicates(subset=['SN'], keep='first')
gendersummary = allbuyers.groupby([ "Gender"]).count()
gendersummary = gendersummary.iloc[:,[0, 1]]
gendersummary = gendersummary.rename(columns={'Age': 'Count'})
gendersummary = gendersummary.rename(columns={'Item ID': 'Percentage'})
allplayers = allbuyers['SN'].count()
gendersummary['Percentage'] = (gendersummary['Percentage']/(allplayers))*100
gendersummary['Percentage'] = gendersummary['Percentage'].map('{:,.1f}%'.format)
gendersummary
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Count</th>
      <th>Percentage</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>108</td>
      <td>17.6%</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>495</td>
      <td>80.9%</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>9</td>
      <td>1.5%</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis by Gender


```python
#Purchase Count, Average Purchase Price, Total Purchase Value, Normalized Totals by gender
gendersalescount = allsales.groupby( [ "Gender"] ).count()
gendersalescount = gendersalescount.iloc[:,[0,1]]
gendersalescount = gendersalescount.rename(columns={'Age': 'Purchase Count'})
gendersalescount = gendersalescount.rename(columns={'Item ID': 'Average Purchase Price'})
gendersalestotal = allsales.groupby( [ "Gender"] ).sum()
gendersalestotal = gendersalestotal.iloc[:,[2]]
gendersalestotal = gendersalestotal.rename(columns={'Price': 'Total Purchase Value'})
purchasinganalysis = gendersalescount.join(gendersalestotal, how='outer')
purchasinganalysis['Average Purchase Price'] = (purchasinganalysis['Total Purchase Value']/purchasinganalysis['Average Purchase Price'])
purchasinganalysis = purchasinganalysis.join(gendersummary, how='outer')
purchasinganalysis = purchasinganalysis.iloc[:,[0,1,2,3]]
purchasinganalysis = purchasinganalysis.rename(columns={'Count': 'Normalized Totals'})
purchasinganalysis['Normalized Totals'] = (purchasinganalysis['Total Purchase Value']/purchasinganalysis['Normalized Totals'])
purchasinganalysis['Normalized Totals'] = purchasinganalysis['Normalized Totals'].map('${:,.2f}'.format)
purchasinganalysis['Total Purchase Value'] = purchasinganalysis['Total Purchase Value'].map('${:,.2f}'.format)
purchasinganalysis['Average Purchase Price'] = purchasinganalysis['Average Purchase Price'].map('${:,.2f}'.format)
purchasinganalysis
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
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
      <td>149</td>
      <td>$2.85</td>
      <td>$424.29</td>
      <td>$3.93</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>697</td>
      <td>$2.94</td>
      <td>$2,052.28</td>
      <td>$4.15</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>12</td>
      <td>$3.15</td>
      <td>$37.86</td>
      <td>$4.21</td>
    </tr>
  </tbody>
</table>
</div>



# Age Demographics


```python
#Purchase Count, Average Purchase Price, Total Purchase Value and Normalized Totals by age bin
agesummary = allbuyers.groupby(["Age Group"]).count()
agegrouptotals = agesummary.iloc[:,[0]]
agegrouptotals = agegrouptotals.rename(columns={'Age': 'Count'})
agegrouptotals = pd.DataFrame(data=agegrouptotals, index=index)
agesummary2 = allsales.groupby( ["Age Group"] ).count()
agegroupsales = agesummary2.iloc[:,[0]]
agegroupsales = agegroupsales.rename(columns={'Age': 'Purchase Count'})
agegroupsales = pd.DataFrame(data=agegroupsales, index=index)
purchasinganalysis2 = agegrouptotals.join(agegroupsales, how='outer')
agesummary3 = allsales.groupby( ["Age Group"] ).sum()
agegroupsalestotals = agesummary3.iloc[:,[2]]
agegroupsalestotals = agegroupsalestotals.rename(columns={'Price': 'Total Purchase Value'})
agegroupsalestotals = pd.DataFrame(data=agegroupsalestotals, index=index)
purchasinganalysis2 = purchasinganalysis2.join(agegroupsalestotals, how='outer')
purchasinganalysis2['Average Purchase Price'] = (purchasinganalysis2['Total Purchase Value']/purchasinganalysis2['Purchase Count'])
purchasinganalysis2 = purchasinganalysis2.rename(columns={'Count': 'Normalized Totals'})
purchasinganalysis2['Normalized Totals'] = (purchasinganalysis2['Total Purchase Value']/purchasinganalysis2['Normalized Totals'])
purchasinganalysis2['Normalized Totals'] = purchasinganalysis2['Normalized Totals'].map('${:,.2f}'.format)
purchasinganalysis2['Total Purchase Value'] = purchasinganalysis2['Total Purchase Value'].map('${:,.2f}'.format)
purchasinganalysis2['Average Purchase Price'] = purchasinganalysis2['Average Purchase Price'].map('${:,.2f}'.format)
purchasinganalysis2 = purchasinganalysis2[['Purchase Count', 'Average Purchase Price', 'Total Purchase Value', 'Normalized Totals']]
purchasinganalysis2
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>33</td>
      <td>$2.95</td>
      <td>$97.28</td>
      <td>$4.63</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>38</td>
      <td>$2.79</td>
      <td>$105.91</td>
      <td>$4.24</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>144</td>
      <td>$2.89</td>
      <td>$416.83</td>
      <td>$3.90</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>372</td>
      <td>$2.92</td>
      <td>$1,087.66</td>
      <td>$4.00</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>134</td>
      <td>$2.96</td>
      <td>$396.44</td>
      <td>$4.26</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>71</td>
      <td>$2.97</td>
      <td>$211.14</td>
      <td>$4.14</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>48</td>
      <td>$2.93</td>
      <td>$140.77</td>
      <td>$4.40</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>18</td>
      <td>$3.24</td>
      <td>$58.40</td>
      <td>$5.31</td>
    </tr>
  </tbody>
</table>
</div>



# Top Spenders


```python
grpsn = allsales.groupby( [ "SN"] ).sum()
sntotsales = grpsn.iloc[:,[2]]
sntotsales = sntotsales.rename(columns={'Price': 'Total Purchase Value'})
grpsn2 = allsales.groupby( [ "SN"] ).count()
sncountsales = grpsn2.iloc[:,[0]]
sncountsales = sncountsales.rename(columns={'Age': 'Purchase Count'})
topspenders = sncountsales.join(sntotsales, how='outer')
topspenders['Average Purchase Price'] = topspenders['Total Purchase Value']/topspenders['Purchase Count']
topspenders['Average Purchase Price'] = topspenders['Average Purchase Price'].map('${:,.2f}'.format)
topspenders = topspenders[['Purchase Count', 'Average Purchase Price', 'Total Purchase Value']]
top5spenders = topspenders.sort_values(['Total Purchase Value'], ascending=False)
top5spenders =  topspenders.nlargest(5, 'Total Purchase Value')
top5spenders['Total Purchase Value'] = top5spenders['Total Purchase Value'].map('${:,.2f}'.format)
top5spenders
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <th>Undirrala66</th>
      <td>5</td>
      <td>$3.41</td>
      <td>$17.06</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>4</td>
      <td>$3.77</td>
      <td>$15.10</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>4</td>
      <td>$3.39</td>
      <td>$13.56</td>
    </tr>
    <tr>
      <th>Sondim43</th>
      <td>4</td>
      <td>$3.25</td>
      <td>$13.02</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>4</td>
      <td>$3.18</td>
      <td>$12.74</td>
    </tr>
  </tbody>
</table>
</div>



# Most Popular Items


```python
grpop = allsales.groupby( [ "Item ID"] ).count()
popitems = grpop.iloc[:,[0]]
popitems = popitems.rename(columns={'Age': 'Purchase Count'})
items = allsales.drop_duplicates(subset=['Item ID'], keep='first')
itemslookup = items.iloc[:,[2,3,4]]
itemslookup = itemslookup.set_index('Item ID')
top5items = popitems.join(itemslookup, how='outer')
top5items = top5items.rename(columns={'Price': 'Item Price'})
top5items['Total Purchase Value'] = top5items['Item Price'] * top5items['Purchase Count']
top5items = top5items[['Item Name', 'Purchase Count', 'Item Price', 'Total Purchase Value']]

top5itemscount = top5items.sort_values(['Purchase Count'], ascending=False)
top5itemscount = top5itemscount.nlargest(5, 'Purchase Count')
top5itemscount['Item Price'] = top5itemscount['Item Price'].map('${:,.2f}'.format)
top5itemscount['Total Purchase Value'] = top5itemscount['Total Purchase Value'].map('${:,.2f}'.format)
top5itemscount
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>84</th>
      <td>Arcane Gem</td>
      <td>12</td>
      <td>$2.23</td>
      <td>$26.76</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>11</td>
      <td>$2.35</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Trickster</td>
      <td>10</td>
      <td>$2.07</td>
      <td>$20.70</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Bonecarvin Battle Axe</td>
      <td>9</td>
      <td>$2.46</td>
      <td>$22.14</td>
    </tr>
    <tr>
      <th>154</th>
      <td>Feral Katana</td>
      <td>9</td>
      <td>$2.19</td>
      <td>$19.71</td>
    </tr>
  </tbody>
</table>
</div>



# Most Profitable Items


```python
top5itemsprof = top5items.sort_values(['Total Purchase Value'], ascending=False)
top5itemsprof = top5itemsprof.nlargest(5, 'Total Purchase Value')
top5itemsprof['Item Price'] = top5itemsprof['Item Price'].map('${:,.2f}'.format)
top5itemsprof['Total Purchase Value'] = top5itemsprof['Total Purchase Value'].map('${:,.2f}'.format)
top5itemsprof
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>Retribution Axe</td>
      <td>9</td>
      <td>$4.14</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>107</th>
      <td>Splitter, Foe Of Subtlety</td>
      <td>9</td>
      <td>$3.61</td>
      <td>$32.49</td>
    </tr>
    <tr>
      <th>108</th>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>9</td>
      <td>$3.39</td>
      <td>$30.51</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Spectral Diamond Doomblade</td>
      <td>7</td>
      <td>$4.25</td>
      <td>$29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Orenmir</td>
      <td>6</td>
      <td>$4.95</td>
      <td>$29.70</td>
    </tr>
  </tbody>
</table>
</div>



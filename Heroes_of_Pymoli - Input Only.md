
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


```python
#Get row count - file 1
pd1_totrows = pd1['SN'].count()
print (pd1_totrows)
```


```python
#Check columns - file 1
pd1.columns
```


```python
#View file 2 headers
pd2.head()
```


```python
#Get row count - file 2
pd2_totrows = pd2['SN'].count()
print (pd2_totrows)
```


```python
#Check columns - file 2
pd2.columns
```


```python
#Get total rows - both files
total_rows = pd1_totrows + pd2_totrows
print (total_rows)
```


```python
#Union 2 files; view headers
files = [pd1, pd2]
allsales = pd.concat(files)
allsales.head()
```


```python
#Get row count - all sales
allsales_totrows = allsales['SN'].count()
print (allsales_totrows)
```


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


```python
#Check columns - all sales
allsales.columns
```


```python
#Get total sales
totsales = allsales['Price'].sum()
print (totsales)
```

# Player Count


```python
#Total number of players
pc = {'Total Players': [allsales['SN'].nunique()]}
playercount = pd.DataFrame(data=pc)
playercount
```

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

# Most Profitable Items


```python
top5itemsprof = top5items.sort_values(['Total Purchase Value'], ascending=False)
top5itemsprof = top5itemsprof.nlargest(5, 'Total Purchase Value')
top5itemsprof['Item Price'] = top5itemsprof['Item Price'].map('${:,.2f}'.format)
top5itemsprof['Total Purchase Value'] = top5itemsprof['Total Purchase Value'].map('${:,.2f}'.format)
top5itemsprof
```

# Pandas Jupyter Notebook

## Background


![Fantasy](Images/Fantasy.png)

Analyze the data for an independent gaming company for their most recent fantasy game Heroes of Pymoli as a Lead Analyst.

Like many others in its genre, the game is free-to-play, but players are encouraged to purchase optional items that enhance their playing experience.
As a first task, the company would like to generate a report that breaks down the game's purchasing data into meaningful insights.

The final report should include each of the following:

### Player Count

* Total Number of Players
 ```python
#get the count
playerCount = df.SN.nunique()

#create table
playerCount_df = pd.DataFrame()
playerCount_df["Total Players"] = [playerCount]

#print
playerCount_df
```
<img width="100" alt="圖片" src="https://user-images.githubusercontent.com/70195202/116376317-be72cf80-a7d5-11eb-9103-ffc4c4e8ff06.png">


### Purchasing Analysis (Total)

* Number of Unique Items
* Average Purchase Price
* Total Number of Purchases
* Total Revenue
```python
#get the number
uniqItem = df["Item Name"].nunique()
avePrice = df.Price.mean()
numPurchasing = df["Purchase ID"].count() 
totRev = df.Price.sum()


#create summary table
purchasingAnalysis = pd.DataFrame()
purchasingAnalysis["Number of Unique Items"] = [uniqItem]
purchasingAnalysis["Average Price"] = [avePrice]
purchasingAnalysis["Number of Purchases"] = [numPurchasing]
purchasingAnalysis["Total Revenue"] = [totRev]

#format the number
purchasingAnalysis["Average Price"] = purchasingAnalysis["Average Price"].map("${:.2f}".format)
purchasingAnalysis["Total Revenue"] = purchasingAnalysis["Total Revenue"].map("${:.2f}".format)

purchasingAnalysis
```
<img width="448" alt="圖片" src="https://user-images.githubusercontent.com/70195202/116376849-3fca6200-a7d6-11eb-9ffa-11905da3cbe1.png">


### Gender Demographics

* Percentage and Count of Male Players
* Percentage and Count of Female Players
* Percentage and Count of Other / Non-Disclosed
```python
people_df = df.groupby(['SN','Gender']).size().reset_index().rename(columns={0:'count'})
#make the columns first
genderCount = people_df.Gender.value_counts()
genderPerc = genderCount / len(people_df)

#make the table
genderTable = pd.DataFrame()
genderTable["Total Count"] = genderCount
genderTable["Percentage of Players"] = genderPerc * 100

#format
genderTable["Percentage of Players"] = genderTable["Percentage of Players"].map("{:.2f}%".format)

#print
genderTable
```
<img width="325" alt="圖片" src="https://user-images.githubusercontent.com/70195202/116377038-6ab4b600-a7d6-11eb-8855-0993e71303cc.png">


### Purchasing Analysis (Gender)

* The below each broken by gender
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Average Purchase Total per Person by Gender

### Age Demographics

* The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.)
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Average Purchase Total per Person by Age Group

### Top Spenders

* Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
  * SN
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value

### Most Popular Items

* Identify the 5 most popular items by purchase count, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value

### Most Profitable Items

* Identify the 5 most profitable items by total purchase value, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value


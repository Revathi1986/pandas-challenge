Note
Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.
1
# Dependencies and Setup
2
​
3
​
4
import pandas as pd
5
​
6
# File to Load (Remember to Change These)
7
file_to_load = "Resources/purchase_data.csv"
8
​
9
# Read Purchasing File and store into Pandas data frame
10
data = pd.read_csv(file_to_load)
11
data_df = pd.DataFrame(data)
12
data_df.head(100)
Purchase ID	SN	Age	Gender	Item ID	Item Name	Price
0	0	Lisim78	20	Male	108	Extraction, Quickblade Of Trembling Hands	3.53
1	1	Lisovynya38	40	Male	143	Frenzied Scimitar	1.56
2	2	Ithergue48	24	Male	92	Final Critic	4.88
3	3	Chamassasya86	24	Male	100	Blindscythe	3.27
4	4	Iskosia90	23	Male	131	Fury	1.44
...	...	...	...	...	...	...	...
95	95	Ilassast39	18	Male	164	Exiled Doomblade	1.63
96	96	Lisassala98	16	Male	56	Foul Titanium Battle Axe	2.92
97	97	Aiduecal76	20	Male	134	Undead Crusader	4.50
98	98	Chadossa89	23	Male	132	Persuasion	3.19
99	99	Haisrisuir60	23	Male	92	Final Critic	4.19
100 rows × 7 columns

1
data_df.count()
Purchase ID    780
SN             780
Age            780
Gender         780
Item ID        780
Item Name      780
Price          780
dtype: int64
1
​
2
​
Player Count
Display the total number of players
1
player_data = data[['SN','Age','Gender']].drop_duplicates()
2
player_data
3
​
SN	Age	Gender
0	Lisim78	20	Male
1	Lisovynya38	40	Male
2	Ithergue48	24	Male
3	Chamassasya86	24	Male
4	Iskosia90	23	Male
...	...	...	...
773	Hala31	21	Male
774	Jiskjask80	11	Male
775	Aethedru70	21	Female
777	Yathecal72	20	Male
778	Sisur91	7	Male
576 rows × 3 columns

1
​
2
player_data = data[['SN','Age','Gender']].drop_duplicates()
3
player_data
4
​
5
total_players= player_data["SN"].count()
6
print(total_players)
7
​
8
​
9
​
576
1
player_data = data[['SN','Age','Gender']].drop_duplicates()
2
player_data
3
​
4
​
5
​
SN	Age	Gender
0	Lisim78	20	Male
1	Lisovynya38	40	Male
2	Ithergue48	24	Male
3	Chamassasya86	24	Male
4	Iskosia90	23	Male
...	...	...	...
773	Hala31	21	Male
774	Jiskjask80	11	Male
775	Aethedru70	21	Female
777	Yathecal72	20	Male
778	Sisur91	7	Male
576 rows × 3 columns

1
data_df.value_counts()
Purchase ID  SN              Age  Gender  Item ID  Item Name                                  Price
779          Ennrian78       24   Male    50       Dawn                                       4.60     1
243          Quaranmol58     24   Male    83       Lifebender                                 3.33     1
265          Lirtirra37      25   Male    172      Blade of the Grave                         3.14     1
264          Saesrideu94     35   Male    119      Stormbringer, Dark Blade of Ending Misery  4.32     1
263          Aeral43         24   Male    78       Glimmer, Ender of the Moon                 4.40     1
                                                                                                      ..
517          Aerithnuphos61  39   Male    128      Blazeguard, Reach of Eternity              4.91     1
516          Aidain51        39   Female  35       Heartless Bone Dualblade                   3.45     1
515          Haillyrgue51    7    Male    40       Second Chance                              2.52     1
514          Yasur85         21   Male    21       Souleater                                  1.10     1
0            Lisim78         20   Male    108      Extraction, Quickblade Of Trembling Hands  3.53     1
Length: 780, dtype: int64
1
​
Purchasing Analysis (Total)
data_df.shape

1
data_df.count()
Purchase ID    780
SN             780
Age            780
Gender         780
Item ID        780
Item Name      780
Price          780
dtype: int64
1
data_df.dtypes
Purchase ID      int64
SN              object
Age              int64
Gender          object
Item ID          int64
Item Name       object
Price          float64
dtype: object
1
data_df["Price"]=pd.to_numeric(data_df["Price"])
1
data_df["Price"].dtype
dtype('float64')
1
data_df["Item ID"].value_counts
<bound method IndexOpsMixin.value_counts of 0      108
1      143
2       92
3      100
4      131
      ... 
775     60
776    164
777     67
778     92
779     50
Name: Item ID, Length: 780, dtype: int64>
1
unique_items = len(data_df["Item ID"].unique())
2
unique_items
179
1
total_purchases = data_df["Purchase ID"].count()
2
total_purchases
3
​
780
1
total_revenue = data_df["Price"].sum()
2
total_revenue
2379.77
1
average_price = total_revenue/total_purchases
2
average_price
3.0509871794871795
1
data_df = pd.DataFrame([{"Number of Unique Items": unique_items, "Average Price": average_price,
2
                                      "Number of Purchases": total_purchases, "Total Revenue": total_revenue}])
3
data_df["Average Price"] = data_df["Average Price"].map("${:,.2f}".format)
4
data_df["Total Revenue"] = data_df["Total Revenue"].map("${:,.2f}".format)
5
data_df
Number of Unique Items	Average Price	Number of Purchases	Total Revenue
0	179	$3.05	780	$2,379.77
Run basic calculations to obtain number of unique items, average price, etc.
Create a summary data frame to hold the results
Optional: give the displayed data cleaner formatting
Display the summary data frame
Gender Demographics
Percentage and Count of Male Players
Percentage and Count of Female Players
Percentage and Count of Other / Non-Disclosed
1
​
2
​
1
gender_df = pd.DataFrame(player_data["Gender"].value_counts())
2
gender_df
3
​
4
​
Gender
Male	484
Female	81
Other / Non-Disclosed	11
1
percentage_of_players = (player_data["Gender"].value_counts()/total_players)*100
2
percentage_of_players
3
​
Male                     62.051282
Female                   10.384615
Other / Non-Disclosed     1.410256
Name: Gender, dtype: float64
1
gender_df["Percentage of Players"] = percentage_of_players
2
gender_df["Percentage of Players"] = gender_df["Percentage of Players"].map("{:,.2f}%".format)
3
gender_df
4
​
Gender	Percentage of Players
Male	484	62.05%
Female	81	10.38%
Other / Non-Disclosed	11	1.41%
1
fin_df = gender_df.rename(columns={"Gender":"Total Count"})
2
fin_df
Total Count	Percentage of Players
Male	484	62.05%
Female	81	10.38%
Other / Non-Disclosed	11	1.41%
1
reorderlist = ['Female', 'Male','Other / Non-Disclosed']
2
fin_df.reindex(reorderlist)
Total Count	Percentage of Players
Female	81	10.38%
Male	484	62.05%
Other / Non-Disclosed	11	1.41%
Purchasing Analysis (Gender)
1
import pandas as pd
2
​
3
# File to Load (Remember to Change These)
4
file_to_load = "Resources/purchase_data.csv"
5
​
6
# Read Purchasing File and store into Pandas data frame
7
data = pd.read_csv(file_to_load)
8
data_df = pd.DataFrame(data)
9
data_df.head(100)
10
gender_g_p_data_df = data_df.groupby(["Gender"])
11
​
12
​
13
gender_g_p_data_df["Purchase ID"].count().head(10)
14
​
15
# Get total purchase value by gender
16
total_purchase_value = gender_g_p_data_df["Price"].sum()
17
total_purchase_value.head()
18
dlr_total_purchase_value = total_purchase_value.map("${:,.2f}".format)
19
dlr_total_purchase_value.head()
20
​
21
# Average purchase price by gender
22
avg_purchase_price = gender_g_p_data_df["Price"].mean()
23
avg_purchase_price.head()
24
dlr_avg_purchase_price = avg_purchase_price.map("${:,.2f}".format)
25
dlr_avg_purchase_price.head()
26
​
27
# Normalized totals, total purchase value divided by purchase count by gender
28
avg_total = total_purchase_value/fin_df["Total Count"]
29
avg_total = avg_total.map("${:,.2f}".format)
30
avg_total.head()
31
​
32
# Organize summary gender data, get all columns to organized Data Frame, add needed columns to it
33
org_gender_purchased_data_df = pd.DataFrame(gender_g_p_data_df["Purchase ID"].count())
34
org_gender_purchased_data_df["Average Purchase Price"] = dlr_avg_purchase_price  
35
org_gender_purchased_data_df["Total Purchase Value"] = dlr_total_purchase_value 
36
org_gender_purchased_data_df["Total number of Purchase per person"] = avg_total
37
org_gender_purchased_data_df
38
​
39
# Summary purchasing analysis DF grouped by gender, rename "Purchase ID" column, using .rename(columns={})
40
summary_gender_purchased_data_df = org_gender_purchased_data_df.rename(columns={"Purchase ID":"Purchase Count"})
41
summary_gender_purchased_data_df
Purchase Count	Average Purchase Price	Total Purchase Value	Total number of Purchase per person
Gender				
Female	113	$3.20	$361.94	$4.47
Male	652	$3.02	$1,967.64	$4.07
Other / Non-Disclosed	15	$3.35	$50.19	$4.56
Age Demographics
1
​
2
import pandas as pd
3
​
4
# File to Load (Remember to Change These)
5
file_to_load = "Resources/purchase_data.csv"
6
​
7
​
8
data = pd.read_csv(file_to_load)
9
data_df = pd.DataFrame(data)
10
data_df.head(100)
11
player_data = data[['SN','Age','Gender']].drop_duplicates()
12
player_data
13
​
14
total_players= player_data["SN"].count()
15
print(total_players)
16
​
17
age_bins = [0, 9.90, 14.90, 19.90, 24.90, 29.90, 34.90, 39.90, 99999]
18
​
19
# # Create the names for the four bins
20
group_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]
21
​
22
grp_by_age_purchase_data_df = data
23
grp_by_age_purchase_data_df["Age Summary"] = pd.cut(grp_by_age_purchase_data_df["Age"], age_bins, labels=group_names)
24
grp_by_age_purchase_data_df
25
​
26
# Creating a group based off of the bins and saving it
27
grp_by_age_purchase_data_df = grp_by_age_purchase_data_df.groupby("Age Summary")
28
grp_by_age_purchase_data_df.count()
29
​
30
# Let's work with this new dataframe
31
summary_by_age_df = pd.DataFrame(grp_by_age_purchase_data_df.count())
32
summary_by_age_df 
33
​
34
# Calculations performed on "Purchase Id"" column of summary df
35
summary_by_age_df["Purchase ID"] = (summary_by_age_df["Purchase ID"]/total_players)*100
36
summary_by_age_df 
37
​
38
# format percentages 
39
summary_by_age_df["Purchase ID"] = summary_by_age_df["Purchase ID"].map("{:,.2f}%".format)
40
summary_by_age_df
41
​
42
#  Reduce number of columns to "Age Summary", "Purcahe ID", format percentages and write into org Data Frame
43
org_summary_by_age_df = summary_by_age_df[["Purchase ID","SN"]]
44
org_summary_by_age_df
45
​
46
# Rename the columns for the final age dempgraphic df using .rename(columns={})
47
fin_grp_by_age_summary_df = org_summary_by_age_df.rename(columns={"Purchase ID":"Percentage of Players", "SN":"Total Count"})
48
fin_grp_by_age_summary_df
576
Percentage of Players	Total Count
Age Summary		
<10	3.99%	23
10-14	4.86%	28
15-19	23.61%	136
20-24	63.37%	365
25-29	17.53%	101
30-34	12.67%	73
35-39	7.12%	41
40+	2.26%	13
Top Spenders
Run basic calculations to obtain the results in the table below
Create a summary data frame to hold the results
Sort the total purchase value column in descending order
Optional: give the displayed data cleaner formatting
Display a preview of the summary data frame
1
orig_p_d_df = pd.DataFrame(data)
2
orig_p_d_df.head()
3
​
4
# Group by Spendors ( "SN" )
5
top_spendor_df = orig_p_data_df.groupby("SN")
6
top_spendor_df.count()
7
​
8
# Let's work with data sorted by SN new dataframe
9
analysis_SPENDOR_df = pd.DataFrame(grp_SN_top_spendor_df["Purchase ID"].count())
10
analysis_SPENDOR_df
11
​
12
# Get Total purchase value by SN
13
total_purchase_value_SN = top_spendor_df["Price"].sum()
14
total_purchase_value_SN
15
​
16
# Get Average purchase price by SN
17
avg_purchase_price_SN = top_spendor_df["Price"].mean()
18
avg_purchase_price_SN
19
dlr_avg_purchase_price_SN = avg_purchase_price_SN.map("${:,.2f}".format)
20
dlr_avg_purchase_price_SN
21
​
22
# Organize summary Top Spender data, get all columns to organized Data Frame, add needed columns to it
23
analysis_SPENDOR_df["Average Purchase Price"] = dlr_avg_purchase_price_SN
24
analysis_SPENDOR_df["Total Purchase Value"] = total_purchase_value_SN 
25
analysis_SPENDOR_df
26
​
27
# Summary Top Spendor analysis grouped by SN, rename "Purchase ID" column, using .rename(columns={})
28
SUM_SN_purchased_data_df = analysis_by_SPENDOR_df.rename(columns={"Purchase ID":"Purchase Count"})
29
TOP5_spendors_df=SUM_SN_purchased_data_df.sort_values("Total Purchase Value", ascending=False)
30
TOP5_spendors_df.head()
31
​
32
# Format Total Purchase Price to be in dollar form
33
dlr_total_purchase_value_SN = total_purchase_value_SN.map("${:,.2f}".format)
34
TOP5_spendors_df["Total Purchase Value"] = dlr_total_purchase_value_SN
35
TOP5_spendors_df.head()
Purchase Count	Average Purchase Price	Total Purchase Value
SN			
Lisosia93	5	$3.79	$18.96
Idastidru52	4	$3.86	$15.45
Chamjask73	3	$4.61	$13.83
Iral74	4	$3.40	$13.62
Iskadarya95	3	$4.37	$13.10
Most Popular Items
Retrieve the Item ID, Item Name, and Item Price columns
Group by Item ID and Item Name. Perform calculations to obtain purchase count, average item price, and total purchase value
Create a summary data frame to hold the results
Sort the purchase count column in descending order
Optional: give the displayed data cleaner formatting
Display a preview of the summary data frame
1
grp_top_item_df = orig_purchase_data_df.groupby(["Item ID", "Item Name"])
2
grp_top_item_df.count()
3
​
4
# Let's work with data sorted by Item new dataframe
5
analysis_ITEM_df = pd.DataFrame(grp_top_item_df["Purchase ID"].count())
6
analysis_ITEM_df
7
​
8
# Get Total purchase value by Item
9
total_purchase_value_ITEM = grp_top_item_df["Price"].sum()
10
total_purchase_value_ITEM
11
dlr_total_purchase_value_ITEM = total_purchase_value_ITEM.map("${:,.2f}".format)
12
dlr_total_purchase_value_ITEM
13
​
14
# Get purchase price by Item
15
purchase_price_ITEM = grp_top_item_df["Price"].mean()
16
purchase_price_ITEM
17
dlr_purchase_price_ITEM = purchase_price_ITEM.map("${:,.2f}".format)
18
dlr_purchase_price_ITEM
19
​
20
# Organize summary Item data, get all columns to organized Data Frame, add needed columns to it
21
analysis_ITEM_df["Item Price"] = dlr_purchase_price_ITEM
22
analysis_ITEM_df["Total Purchase Value"] = dlr_total_purchase_value_ITEM
23
analysis_ITEM_df
24
​
25
# Summary Most Popular Item analysis grouped by Item, rename "Purchase ID" column, using .rename(columns={})
26
SUM_ITEM_purchased_data_df = analysis_by_ITEM_df.rename(columns={"Purchase ID":"Purchase Count"})
27
TOP5_ITEMS_df=SUM_ITEM_purchased_data_df.sort_values("Purchase Count", ascending=False)
28
TOP5_ITEMS_df.head()
Purchase Count	Item Price	Total Purchase Value
Item ID	Item Name			
92	Final Critic	13	$4.61	$59.99
178	Oathbreaker, Last Hope of the Breaking Storm	12	$4.23	$50.76
145	Fiery Glass Crusader	9	$4.58	$41.22
132	Persuasion	9	$3.22	$28.99
108	Extraction, Quickblade Of Trembling Hands	9	$3.53	$31.77
Most Profitable Items
Sort the above table by total purchase value in descending order
Optional: give the displayed data cleaner formatting
Display a preview of the data frame
1
SUM_ITEM_purchased_data_df["Total Purchase Value"] = grp_top_item_df["Price"].sum()
2
SUM_ITEM_purchased_data_df
3
​
4
# Summary Most Popular Item analysis grouped by Item, rename "Purchase ID" column, using .rename(columns={})
5
TOP5_ITEMS_df=SUM_ITEM_purchased_data_df.sort_values("Total Purchase Value", ascending=False)
6
​
7
# Format Total Purchase Price to be in dollar form
8
dlr_total_purchase_value_ITEM = total_purchase_value_ITEM.map("${:,.2f}".format)
9
TOP5_ITEMS_df["Total Purchase Value"] = dlr_total_purchase_value_ITEM
10
TOP5_ITEMS_df.head()
Purchase Count	Item Price	Total Purchase Value
Item ID	Item Name			
92	Final Critic	13	$4.61	$59.99
178	Oathbreaker, Last Hope of the Breaking Storm	12	$4.23	$50.76
82	Nirvana	9	$4.90	$44.10
145	Fiery Glass Crusader	9	$4.58	$41.22
103	Singed Scalpel	8	$4.35	$34.80
1
​

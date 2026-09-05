# Name : Viswanadham Venkata Sai Sruthi
# Register Number : 212223100061
# Ex.No : 2


**Netflix Shows & Movies**

**Aim**

To analyze Netflix dataset and compare movies vs TV shows, top producing countries, and release year trends.

**Procedure / Algorithm**

Step 1: Load and Explore the Dataset

Step 2: Analyze Missing Values

Step 3: Perform Data Indexing and Selection

Step 4: Create New Columns

Step 5: Perform Vectorized String Operations

Step 6: Perform Aggregation and Grouping

Step 7: Perform Frequency Analysis

Step 8: Create Pivot Tables

Step 9: Perform Hierarchical Indexing (MultiIndex)

Step 10: Combine DataFrames

Step 11: Analyze Netflix Additions Over Time

Step 12: Generate Summary Report

**Program**

```
import pandas as pd
import numpy as np
url="https://raw.githubusercontent.com/allenkong221/netflix-titles-dataset/main/netflix_titles.csv"
df=pd.read_csv(url)
df.head()
df.tail()
(df.shape)
df.columns
df.info()
df.describe(include="all")
missing=df.isnull().sum()
percentage=(missing/len(df))*100
print(pd.DataFrame({"Missing Values":missing,"Percentage":percentage}))
df["director"]=df["director"].fillna("Unknown")
df["country"]=df["country"].fillna("Not Specified")
df["cast"]=df["cast"].fillna("No Cast")
df["rating"]=df["rating"].fillna(df["rating"].mode()[0])
clean_df=df.dropna(subset=["director","country"])
print(clean_df.shape)
movies=df[df["type"]=="Movie"]
movies
tvshows=df[df["type"]=="TV Show"]
tvshows
df[["title", "country", "release_year"]]
df.iloc[100:121]
df[(df["type"]=="Movie")&(df["release_year"]>2018)]
df[df["country"].str.contains("India",na=False)][["title","country"]]
df[(df["type"]=="TV Show")&(df["country"].str.contains("United States",na=False))]
df[(df["type"]=="Movie")&(df["rating"]=="PG-13")]
current_year=pd.Timestamp.now().year
df["Title Length"]=df["title"].str.len()
df["Movie Age"]=current_year-df["release_year"]
df["Is Recent Content"]=df["release_year"]>=2020
print(df.loc[df["Title Length"].idxmax(),"title"])
print(df.loc[df["Title Length"].idxmin(),"title"])
print(df["Movie Age"].mean())
print(df.loc[df["release_year"].idxmin(),["title","release_year"]])
print(df.loc[df["release_year"].idxmax(),["title","release_year"]])
df["title"].str.upper()
df["title"].str.lower()
df["title"].str.len()
df[df["title"].str.contains("Love",case=False,na=False)]["title"]
df[df["title"].str.contains("Life",case=False,na=False)]["title"]
df[df["title"].str.startswith("The",na=False)]["title"]
df[df["title"].str.endswith("Story",na=False)]["title"]
df["Primary Genre"]=df["listed_in"].str.split(",").str[0]
print(df[["title","Primary Genre"]])
print(df.groupby("type")["show_id"].count())
print(df.groupby("type")["release_year"].mean())
print(df.groupby("rating")["show_id"].count())
print(df["country"].value_counts().head(10))
print(df["director"].value_counts().head(10))
genres=df["listed_in"].str.split(", ").explode()
print(genres.value_counts().head(10))
pivot_country=pd.pivot_table(df,values="show_id",index="country",columns="type",aggfunc="count",fill_value=0)
print(pivot_country)
pivot_year=pd.pivot_table(df,values="show_id",index="release_year",columns="type",aggfunc="count",fill_value=0)
print(pivot_year)
multi_df=df.set_index(["country","type"])
multi_df.loc[("India","Movie")]
multi_df.loc[("United States","TV Show")]
movies_df=df[df["type"]=="Movie"]
tv_df=df[df["type"]=="TV Show"]
combined=pd.concat([movies_df,tv_df],ignore_index=True)
print(combined.shape)
title_director=df[["title","director"]]
title_country=df[["title","country"]]
merged=pd.merge(title_director,title_country,on="title")
print(merged.head())
df["date_added"]=pd.to_datetime(df["date_added"],errors="coerce")
df["Year Added"]=df["date_added"].dt.year
df["Month Added"]=df["date_added"].dt.month_name()
print(df.groupby(["Year Added","type"]).size().unstack(fill_value=0))
print(df.groupby(["Month Added","type"]).size().unstack(fill_value=0))
print(df["country"].value_counts().idxmax())
print(df["Year Added"].value_counts().idxmax())
print(df["rating"].value_counts().idxmax())
print(genres.value_counts().idxmax())
print((df["type"].value_counts(normalize=True)*100).round(2))
```
**Ouptut**
<img width="1085" height="890" alt="Screenshot 2026-09-05 123620" src="https://github.com/user-attachments/assets/74474c5e-a7c5-4027-87f2-4f734097a999" />
<img width="1089" height="822" alt="Screenshot 2026-09-05 123700" src="https://github.com/user-attachments/assets/ace083b4-08f3-4238-95a9-6a959468dbb0" />
<img width="1087" height="892" alt="Screenshot 2026-09-05 123732" src="https://github.com/user-attachments/assets/2d41db00-f684-4b4d-8d40-8d9f1ffb798a" />
<img width="1095" height="780" alt="Screenshot 2026-09-05 123802" src="https://github.com/user-attachments/assets/e0cd1230-9fb0-4ce0-99de-58620bdf998f" />
<img width="1096" height="736" alt="Screenshot 2026-09-05 123857" src="https://github.com/user-attachments/assets/dd5f0307-cdff-4b56-8658-034e9659236d" />
<img width="715" height="859" alt="Screenshot 2026-09-05 123942" src="https://github.com/user-attachments/assets/4e413d5c-1f4d-424f-b9c8-dda8a404a91e" />
<img width="793" height="890" alt="Screenshot 2026-09-05 124019" src="https://github.com/user-attachments/assets/545db454-c1d9-494c-9353-527bff334e01" />
<img width="978" height="913" alt="Screenshot 2026-09-05 124100" src="https://github.com/user-attachments/assets/798435d8-22dd-4057-9067-edee458c253b" />
<img width="971" height="962" alt="Screenshot 2026-09-05 124154" src="https://github.com/user-attachments/assets/e1241c62-a631-49dc-9637-c7c17911e3a2" />
<img width="968" height="744" alt="Screenshot 2026-09-05 124227" src="https://github.com/user-attachments/assets/c623f073-ec4f-4369-bd31-23f0831b6d89" />
<img width="976" height="843" alt="Screenshot 2026-09-05 124256" src="https://github.com/user-attachments/assets/a39326a6-d545-4569-af70-a7e90e31b4d9" />
<img width="971" height="961" alt="Screenshot 2026-09-05 124318" src="https://github.com/user-attachments/assets/3b01941f-1c3f-4d9e-8501-54f3e14494d6" />
<img width="703" height="220" alt="Screenshot 2026-09-05 124340" src="https://github.com/user-attachments/assets/b19d85a8-358b-44f6-8d37-3048adb40d87" />

**Result**
Helps Netflix in content planning & investments.

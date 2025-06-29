# sales_analysis
#Import python libraries
import pandas as pd
import numpy as np
#Import libraries for visualization
import matplotlib.pyplot as plt
import seaborn as sns


#import csv file
df=pd.read_csv("electronics.csv")
df


#First 5 rows of list
df.head()


#Last 5 rows of the list
df.tail()


#shape of csv data
df.shape


#check the data type and null or notnull values
df.info()


#description of data
df.describe()
t.index
df=df.fillna(0)
df


# We can see that the dataset contains 5 columns .   

# The data types of the columns are as follows:

# 1. User ID - int64

# 2. Product ID - object

# 3. Rating - int64

# 4. Timestamp - int64

# 5. Category - object

# We can see that the columns User ID and Rating are of int64 data type, while the columns Product ID and Category are of object data type.

# We can also see that there are no null values in the dataset.

# We can also see that the column Timestamp is of int64 data type, but it is actually a timestamp.

# We can convert it to a timestamp using the following code:

from datetime import datetime

pd.to_datetime(df['timestamp'])


# We can also see that the column Category is of object data type, but it is actually a string.



# We can convert it to a string using the following code:

df['category'] = df['category'].astype(str)

df['rating'] = df['rating'].astype(float)
df['user_id'] = df['user_id'].astype(str)

df['item_id'] = df['item_id'].astype(str)
df.info()


# We can also see the number of unique users and items in the dataset.

df.nunique()


# drop all duplicate values in rating category

df.rating.dropna(inplace=True)

df.rating.drop_duplicates(inplace=True)


# drop all duplicate values in brand category

df.brand.dropna(inplace=True)

df.brand.drop_duplicates(inplace=True)


# drop all duplicate values in user_attr  category

df.user_attr .dropna(inplace=True)

df.user_attr .drop_duplicates(inplace=True)
df


# check for duplicates

df.duplicated().sum()


# check for missing values

df.isnull().sum()
df=df.dropna()
df
df.drop('brand', axis=1, inplace=True)
df
df.drop('split', axis=1, inplace=True)
df
df.drop('user_attr', axis=1, inplace=True)
df
df


# The distribution of ratings 
sns.countplot(x='rating',data=df)
#what was the best year of sales
df['year']=pd.DatetimeIndex(df['timestamp']).year
df.groupby('year')['rating'].count().plot(kind='bar')
#what brand sold most in 2015.
df_15=df[df['year'] == 2015]
df_15.groupby('brand')['rating'].count().sort_values(ascending=False).head(10).plot(kind='bar')
#what product sold the most in 2016
df[df['year'] == 2016].groupby('brand')['rating'].count().sort_values(ascending=False).head(10).plot(kind='bar')
#what product sold the most in 2017
df[df['year'] == 2017].groupby('brand')['rating'].count().sort_values(ascending=False).head(10).plot(kind='bar')
#what product sold the most in 2018
df[df['year'] == 2018].groupby('brand')['rating'].count().sort_values(ascending=False).head(10).plot(kind='bar')
#How much was made in sales in the year 2015
df[df['year'] == 2015].groupby('year')['rating'].count().plot(kind='bar')


# We can see that the year 2015 had the best sales.


# what was the best month of sales
df['month'] = pd.DatetimeIndex(df['timestamp']).month
df.groupby('month')['rating'].count().plot(kind='bar')
#what product by brand name sold most?
df.groupby('brand')['rating'].count().sort_values(ascending=False).head(10).plot(kind='bar')
#what product category sold the most?
df.groupby('category')['rating'].count().sort_values(ascending=False).head(10).plot(kind='bar')


# What product by brand name sold the least?
df.groupby('brand')['rating'].count().sort_values(ascending=True).head(10).plot(kind='bar')
#what product by category sold the least?
df.groupby('category')['rating'].count().sort_values(ascending=True).head(10).plot(kind='bar')

# category percentage sales
df.groupby('category')['rating'].count().sort_values(ascending=False).head(10).plot(kind='pie')


# brand percentage sales
df.groupby('brand')['rating'].count().sort_values(ascending=False).head(10).plot(kind='pie')
# conclusion of our analysis

# We can see that the year 2015 had the best sales.

# The month of January had the best sales.

# We can see that the brands Bose and Logitech sold the most

# We can see that the category of Headphones sold the most.

# We can see that the brand name of EINCAR sold the least followed closely with DURAGADGET.

# We can see that the category of Security and Surveillance sold the least.

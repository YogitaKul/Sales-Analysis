# Sales-Analysis
Data Analytics Project
import pandas as pd
from datetime import datetime
df = pd.read_csv("E:\\SalesProject.csv",encoding = "latin-1")
#print(df.head(5))

#check for missing or null values
#isnull() - checks for null values
#sum() - add the cells with null values
print(df.isnull().sum())

#if any missing or empty values fill them with 0 for numeric & unknown for text
df['Sales'] = df['Sales'].fillna(0)
df['Quantity'] = df['Quantity'].fillna(0)
df['Region'] = df['Region'].fillna("unknown")

#remove or delete the rows where orderid is empty
df = df.dropna(subset = ['Order ID'])

#remove duplicates
df = df.drop_duplicates(subset = ['Order ID'])

#assign datatype / change datatype
#df['Order Date'] = pd.to_datetime(df['Order Date'])
#df['Ship Date'] = pd.to_datetime(df['Ship Date'])

#ensure that numeric fields have numeric data only & if not replace with NaN(not a number)
#errors = "coerce" will confirm that if alphabets are found in numeric data they will repalced with NaN(Not a Number)
df['Sales'] = pd.to_numeric(df['Sales'],errors = "coerce")
df['Quantity'] = pd.to_numeric(df['Quantity'],errors = "coerce")
df['Discount'] = pd.to_numeric(df['Discount'],errors = "coerce")
df['Profit'] = pd.to_numeric(df['Profit'],errors = "coerce")

#handle data which has too high or too low values
#df = df[(df['Sales']>1) & (df['Sales']<100000)]

#change case of particular columns
df['Region'] = df['Region'].str.lower()

#save file - craete new file with cleaned data
df.to_csv("E:\\SalesProjectCleaned.csv", index = False)

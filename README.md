# Data-Analysis : Exploratory Data Analysis of Employee Dataset Using Python
 
# importing the python libraries

import numpy as np                                #help to work on arrays or mathematical opearation
import pandas as pd                               #help to work on data frame i.e. tables
import matplotlib.pyplot as plt                   #help in creation charts and visualizing data
%matplotlib inline
import seaborn as sns                             #same as matploy etc

# to Import the excel file (whenever we are making any changes in the excel or save operation give this cmd again
df = pd.read_excel('Employee_data.xlsx')

#show details of row and column
df.shape

# will show 5 top rows with all column (adding values inside the brackets will show those many rows)

df.head()

# to get the information of data types 
df.info()

Data Cleaning steps : 

#drop unrelated / blank columns
df.drop(['Status', 'pratha'], axis=1, inplace=True)    #axis1 means entire column to be deleted, in place true mean save again

#check for null values
pd.isnull(df).sum()


# drop null values delete all values from above which identified 
df.dropna(inplace=True)

#Whatever changes we did till now to get that new sheet give below command

df.to_excel('Updated_Employee_data.xlsx', index=False)

# To change data type                          # (while changing this data make sure any column should not contain the null values)
df['Satisfaction Score'] = df['Satisfaction Score'].astype('int')


# To check data type
df['Satisfaction Score'].dtypes

# To check column details
df.columns

# to rename the column
df.rename(columns={'AD Email': 'Mail'}, inplace=True))    #this is in the form of dictionary in key value forms

# describe() method returns description of the data in the DataFrame (i.e. count, mean, std, etc)
df.describe()


# use describe() for specific columns
df[['Current Employee Rating', 'Training Cost']].describe()

----------------------------------------------------------------------------------------------------------------
# Exploratory Data Analysis
-------------

# plotting a bar chart for Current Employee Rating and it's count

ax = sns.countplot(x = 'Current Employee Rating',data = df)

for bars in ax.containers:
    ax.bar_label(bars)

-------

# plotting a bar chart for gender vs total amount

sales_gen = df.groupby(['Gender'], as_index=False)['Salary'].sum().sort_values(by='Salary', ascending=False)

sns.barplot(x = 'Gender',y= 'Salary' ,data = sales_gen)

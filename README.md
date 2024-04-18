```python
import seaborn as sns
import matplotlib.pyplot as plt
#create seaborn countplot
plt.figure(figsize=(10, 6))
my_plot = sns.countplot(data=dataFrame, x='Primary Type')

#rotate x-axis labels
my_plot.set_xticklabels(my_plot.get_xticklabels(), rotation=90)
plt.title('Count of Crime Types')
plt.show()
```

    C:\Users\Akshay\AppData\Local\Temp\ipykernel_26740\1212175330.py:8: UserWarning: set_ticklabels() should only be used with a fixed number of ticks, i.e. after set_ticks() or using a FixedLocator.
      my_plot.set_xticklabels(my_plot.get_xticklabels(), rotation=90)
    


    
![png](output_9_1.png)
```python

# Set custom color palette
custom_palette = "Set2"
# Define custom color palette
# custom_colors = ["#FF5733", "#33FF57", "#3366FF", "#FF33F3", "#33FFFF", "#FFFF33"]

# Set figure size
plt.figure(figsize=(12, 8))
ax = sns.histplot(dataFrame, x="Date", hue="Primary Type")
plt.title('Count of Crime vs Date')
sns.move_legend(ax, "upper left", bbox_to_anchor=(1,1))
plt.show()
```


    
![png](output_10_0.png)

```python
# Creating bar plot with a bigger size
crosstb = pd.crosstab(dataFrame["Primary Type"], dataFrame["Arrest"])
pl = crosstb.plot(kind="bar", stacked=True, rot=90, figsize=(12, 8))# Creating barplot
# pl = crosstb.plot(kind="bar", stacked=True, rot=90)
# Adding legend and adjusting its position
pl.legend(title='CRIME TYPE ARREST', bbox_to_anchor=(1, 1.02), loc='upper left')
plt.title('Arrest Counts by Crime Type')
# Show the plot
plt.show()
```


    
![png](output_17_0.png)
    





```python
# Load the data and parse the "Date" column as datetime
dataFrame = pd.read_csv("./chicago_crimes_2017.csv", parse_dates=["Date"])

# Extract the month and year information
dataFrame['Month'] = dataFrame['Date'].dt.strftime('%B')
dataFrame['Year'] = dataFrame['Date'].dt.year

# Aggregate the data by month
monthly_crime_count = dataFrame.groupby('Month').size()

# Plot the bar graph
plt.figure(figsize=(10, 6))  # Adjust the figure size as needed
monthly_crime_count.plot(kind='bar', rot=45)
plt.xlabel('Month')
plt.ylabel('Number of Crimes')
plt.title('Distribution of Crimes Over Time (Monthly)')
plt.show()
```
![png](output_21_1.png)





```python
# Set Seaborn dark grid style
sns.set_style("darkgrid")

# Count the frequency of each location description
location_counts = dataFrame['Location Description'].value_counts()

# Select the top 10 most frequent locations
top_locations = location_counts.head(10)

# Group the remaining locations into an "Other" category
other_count = location_counts.iloc[10:].sum()
top_locations['Other'] = other_count

# Create a bar graph to visualize the distribution of crimes across different locations
plt.figure(figsize=(10, 6))
sns.barplot(x=top_locations.index, y=top_locations.values, palette="dark")
plt.xlabel('Location Description')
plt.ylabel('Frequency of Crimes')
plt.title('Distribution of Crimes Across Different Locations')
plt.xticks(rotation=60)  # Rotate x-axis labels for better readability
plt.tight_layout()  # Adjust layout to prevent clipping of labels
plt.show()

```
![png](output_22_1.png)

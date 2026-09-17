# ECE2112-2ECEC-PA4

Made by Shaun Michael R. Remular

This Repository contains the Programming Assignment 4 for the course "Advanced Computer Programming" S.Y. 2026-2027. This project covers Module 4 - Data Wrangling and Data Visualization, including three Python problems.

## Objectives
- Use Pandas and matplotlib.pyplot to search and visualize data.
- Construct DataFrames to sift through and show specific data points
- Manipulate the DataFrame into easily identifiable data points
- Construct graphs to further simplify the process of data visualization
- Summarize the results of data wrangling into easily understandable data

code imports pandas as pd and matplotlib.pyplot as plt
board2.xlsx is imported as a data set that will be used in the data wrangling and data visualization

## A. Visayas Communication DataFrame
The problem involves creating a DataFrame named VisComm that includes only people who are from Visayas and has communication as the track. Furthermore, the problem further specifies the problem into only including Name, Gender, Math, Electronics, and Average in the data frame

The DataFrame was created as follows
````
VisComm = pd.DataFrame(ECE, columns = ['Name', 'Gender', 'Math', 'Electronics', 'Average']).loc[(ECE['Hometown']=='Visayas')&(ECE['Track']=='Communication')]
VisComm
````
It then presents the data containing only those within does specific criteria.


## B. Visayas Female DataFrame
The part one of problem B involves creating another DataFrame called VisFemale that includes only people who are from Visayas and whose gender are female.

The DataFrame was created as follows
````
VisFemale = pd.DataFrame(ECE, columns = ['Name', 'Track', 'GEAS','Electronics', 'Average']).loc[(ECE['Gender']=='Female')]
VisFemale
````

Part two of problem B further specifies to only include those who have an average of above 60, without overwriting the original VisFemale

The search was created as follows
````
VisFemale.loc[(VisFemale['Average']>60)]
````

## C. Category-Average Visualization
This problem involves four different parts, but involves taken the average of different categories under track, gender, and hometown.
1. For each feature, compute the mean of Average for every category using Pandas.
2. Display the three summary tables.
3. Create one figure containing three bar charts: mean Average by Track, by Gender, and by Hometown.
4. Below the figure, write three concise statements identifying the category with the highest sample mean for each feature.

For part 1 of problem C, the goal is to compute the mean of every category by grouping each individual component, connecting them to the average, and taking the mean.
It is given by this code.
````
meanTrack = ECE.groupby('Track')['Average'].mean()
meanGender = ECE.groupby('Gender')['Average'].mean()
meanHometown = ECE.groupby('Hometown')['Average'].mean()
````

For part 2 of the problem, the goal was to display into three unique summary tables and is given by the following code.
````
print(meanTrack, '\n')

print(meanGender, '\n')

print(meanHometown, '\n')
````

For part 3 of the problem, the plan is to create three bar graphs for each category. Each Bar graph is under the same plot under different subplots.
````
fig, ax = plt.subplots(1, 3, figsize=(20,8))
````
Afterwards, each code a bar graph is created from the results of part 2, with the subcategories serving as the index while the resulting average for each is the value. 
As an example, only the graph for track will be shown for now.
````
ax[0].bar(meanTrack.index, meanTrack.values, color = 'Red')
````
In addition to that, titles and labels are added to denote each bar graph and their axis. 
````
ax[0].set(title='Average by Track', ylabel='Average', xlabel='Track')
````
And to further clarify the differences of the data the upper and lower limit of the y-axis is changed to a range of only 60-70 to show the differences much clearer.
````
ax[0].set(ylim=[60, 70])
````


Hence the code for all three bar graphs is as follows.
````
ax[0].bar(meanTrack.index, meanTrack.values, color = 'Red')
ax[0].set(ylim=[60, 70])
ax[0].set(title='Average by Track', ylabel='Average', xlabel='Track')

ax[1].bar(meanGender.index, meanGender.values, color='Black')
ax[1].set(ylim=[60, 70])
ax[1].set(title='Average by Gender', ylabel='Average', xlabel='Gender')

ax[2].bar(meanHometown.index, meanHometown.values, color='Green')
ax[2].set(ylim=[60, 70])
ax[2].set(title='Average by Hometown', ylabel='Average', xlabel='Hometown')

fig.text(0.7,0,'Average by Hometown shows that the highest average comes from Luzon')
fig.text(0.04,0,'Average by Track shows that Communication had the overall highest average.')
fig.text(0.37,0,'Average by Gender shows men have a slightly higher average than women.')
````



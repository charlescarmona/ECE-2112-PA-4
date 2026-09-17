# ECE-2112-PA-4

**Made by: Charles John M. Carmona | 2ECE-B**

The content of this repository contains Experiment 4 for the course "Advanced Computer Programming and Algorithms" this S.Y. 2026-2027. This experiment focuses on Data Wrangling and Data Visualization using Pandas and Matplotlib, particularly filtering data using multiple conditions, creating specific DataFrames, calculating mean averages for different categories, and visualizing the results using bar graphs.

# **IMPORTING LIBRARIES AND DATASET**

Before performing the programming problems, the Pandas and Matplotlib libraries are imported. The ECE Board Exam 2 dataset is then loaded from the Excel file and stored in a DataFrame named `bdf`.

The functions used for this are the following:

- `import pandas as pd` - Imports the Pandas library and assigns `pd` as its alias.
- `import matplotlib.pyplot as plt` - Imports Matplotlib's plotting functions and assigns `plt` as its alias.
- `pd.read_excel("board2.xlsx")` - Reads the Excel file and converts it into a Pandas DataFrame.
- `bdf` - Stores and displays the ECE Board Exam 2 dataset.

```Python
import pandas as pd
import matplotlib.pyplot as plt
```

```Python
# Uploading the ECE Board Exam 2 dataset from the Excel File
bdf = pd.read_excel("board2.xlsx")
bdf
```

# **CREATING THE AVERAGE COLUMN**

This part creates a new column named `Average` by calculating the mean score of each student from Math, Electronics, GEAS, and Communication.

The functions and methods used for this are the following:

- `bdf["Average"]` - Creates a new column named Average in the DataFrame.
- `bdf[['Math', 'Electronics', 'GEAS', 'Communication']]` - Selects the four subject columns used for the calculation.
- `.mean(axis=1)` - Calculates the mean across the four selected subjects for each student.
- `axis=1` - Specifies that the calculation is performed horizontally across each row.
- `bdf` - Displays the DataFrame with the calculated Average column.

```Python
#Create the average column through the meran score
bdf["Average"] = bdf[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
bdf
```

# **A. VISAYAS COMMUNICATION DATAFRAME**

This problem creates a DataFrame named `VisComm` containing students whose Hometown is Visayas and whose Track is Communication. After applying both conditions, only the Name, Gender, Math, Electronics, and Average columns are retained. The number of rows in the resulting DataFrame is also counted and displayed.

The functions, operators, and methods used for this are the following:

- `bdf["Hometown"] == "Visayas"` - Creates a condition that selects students whose Hometown is Visayas.
- `bdf["Track"] == "Communication"` - Creates a condition that selects students whose Track is Communication.
- `&` - Acts as the AND operator, requiring both conditions to be true.
- `["Name", "Gender", "Math", "Electronics", "Average"]` - Selects only the required columns in the specified order.
- `VisComm` - Stores the resulting filtered DataFrame.
- `len(VisComm)` - Counts the total number of rows in the VisComm DataFrame.
- `print()` - Displays the number of rows.

```Python
#Create the dataframe named Viscomm with the following conditions: The student must be in Visayas and Their track must be in Communication
VisComm = bdf[(bdf["Hometown"] == "Visayas") &
          (bdf["Track"] == "Communication")][
#After filtering, retain only the required columns in the order:
          ["Name", "Gender", "Math", "Electronics", "Average"]]

#Display the Dataframe
VisComm
```

```Python
#Count and display the number of rows in VisComm
print("Number of rows:", len(VisComm))
```

# **B. VISAYAS FEMALE DATAFRAME**

This problem creates a DataFrame named `VisW` containing students whose Hometown is Visayas and whose Gender is Female. It retains only the Name, Track, GEAS, Electronics, and Average columns.

The resulting `VisW` DataFrame is then filtered to display students whose Average is at least 60 without overwriting the original DataFrame.

The functions, operators, and methods used for this are the following:

- `bdf["Hometown"] == "Visayas"` - Creates a condition that selects students whose Hometown is Visayas.
- `bdf["Gender"] == "Female"` - Creates a condition that selects female students.
- `&` - Requires both conditions to be true.
- `["Name", "Track", "GEAS", "Electronics", "Average"]` - Retains only the required columns.
- `VisW` - Stores the resulting filtered DataFrame.
- `VisW["Average"] >= 60` - Checks which students have an Average greater than or equal to 60.
- `VisW[VisW["Average"] >= 60]` - Displays only the students who meet the Average requirement without changing `VisW`.

```Python
#Create a Dataframe named VisW with the following conditions: The student must be in Visayas and must be a Female
VisW = bdf[(bdf["Hometown"] == "Visayas") &
          (bdf["Gender"] == "Female")][
#After filtering, retain only the required columns in the order:
          ["Name", "Track", "GEAS", "Electronics", "Average"]]

#Display Dataframe
VisW
```

```Python
#Display VisW students with an Average of atleast 60 and above
VisW[VisW["Average"] >= 60]
```

# **C. CATEGORY-AVERAGE VISUALIZATION**

This problem examines the recorded Average of the students according to three categorical features: Track, Gender, and Hometown. The students are grouped according to each category and their mean Average is calculated. These results are then used to create three bar graphs for comparison.

## **C.a & C.b - MEAN AVERAGE BY TRACK, GENDER, AND HOMETOWN**

The first calculation groups the students according to their Track and calculates the mean Average for each Track.

The functions and methods used for this are the following:

- `bdf.groupby("Track")` - Groups the students according to their Track.
- `["Average"]` - Selects the Average column from each group.
- `.mean()` - Calculates the mean Average of each Track.
- `.reset_index()` - Converts the grouped result into a regular DataFrame.
- `avg_track` - Stores the calculated mean Average for each Track.

```Python
#Calculate the mean Average for each of the Track
avg_track = bdf.groupby("Track")["Average"].mean().reset_index()

avg_track
```

The second calculation groups the students according to their Gender and calculates the mean Average for each Gender.

The functions and methods used for this are the following:

- `bdf.groupby("Gender")` - Groups the students according to their Gender.
- `["Average"]` - Selects the Average column.
- `.mean()` - Calculates the mean Average for each Gender.
- `.reset_index()` - Converts the grouped result into a regular DataFrame.
- `avg_gender` - Stores the calculated mean Average for each Gender.

```Python
#Calculate the Mean Average for each Gender
avg_gender = bdf.groupby("Gender")["Average"].mean().reset_index()

avg_gender
```

The third calculation groups the students according to their Hometown and calculates the mean Average for each Hometown.

The functions and methods used for this are the following:

- `bdf.groupby("Hometown")` - Groups the students according to their Hometown.
- `["Average"]` - Selects the Average column.
- `.mean()` - Calculates the mean Average for each Hometown.
- `.reset_index()` - Converts the grouped result into a regular DataFrame.
- `avg_hometown` - Stores the calculated mean Average for each Hometown.

```Python
#Calculate the Mean Average for each Hometown
avg_hometown = bdf.groupby("Hometown")["Average"].mean().reset_index()

avg_hometown
```

## **C.c - CREATING THE BAR GRAPHS**

This part uses the three calculated mean Average DataFrames to create one figure containing three bar graphs. The graphs compare the mean Average according to Track, Gender, and Hometown.

The functions and methods used for this are the following:

- `plt.subplots(1, 3, figsize = (18, 5))` - Creates one figure containing three graphs arranged in one row.
- `fig` - Represents the entire figure containing the graphs.
- `axes` - Stores the individual graph areas.
- `axes[0]` - Refers to the first graph for Track.
- `axes[1]` - Refers to the second graph for Gender.
- `axes[2]` - Refers to the third graph for Hometown.
- `.bar()` - Creates a bar graph using the category and its mean Average.
- `.set_title()` - Sets the title of each graph.
- `.set_xlabel()` - Sets the label of the x-axis.
- `.set_ylabel()` - Sets the label of the y-axis.
- `.tick_params()` - Adjusts the category labels on the x-axis.
- `rotation = 30` - Rotates the category labels by 30 degrees to improve readability.
- `.set_ylim(0, 100)` - Sets the y-axis scale from 0 to 100.
- `plt.tight_layout()` - Adjusts the spacing between the graphs.
- `plt.show()` - Displays the completed figure.

```Python
#Create three bar graphs in one figure

fig, axes = plt.subplots(1, 3, figsize = (18, 5))

# The Mean Average by Track
axes[0].bar(avg_track["Track"], avg_track["Average"])
axes[0].set_title("Mean Average by Track")
axes[0].set_xlabel("Track")
axes[0].set_ylabel("Mean Average")
axes[0].tick_params(axis = "x", rotation = 30)
axes[0].set_ylim(0, 100)

# The Mean Average by Gender
axes[1].bar(avg_gender["Gender"], avg_gender["Average"])
axes[1].set_title("Mean Average by Gender")
axes[1].set_xlabel("Gender")
axes[1].set_ylabel("Mean Average")
axes[1].set_ylim(0, 100)

# The Mean Average by Hometown
axes[2].bar(avg_hometown["Hometown"], avg_hometown["Average"])
axes[2].set_title("Mean Average by Hometown")
axes[2].set_xlabel("Hometown")
axes[2].set_ylabel("Mean Average")
axes[2].tick_params(axis = "x", rotation = 30)
axes[2].set_ylim(0, 100)

# Adjust Spacing and Display the graphs
plt.tight_layout()
plt.show()
```

## **C.d - INTERPRETATION OF THE RESULTS**

This part identifies the category with the highest mean Average for Track, Gender, and Hometown. Instead of manually entering the highest values, the program obtains them directly from the previously calculated DataFrames.

The functions and methods used for this are the following:

- `avg_track["Average"].idxmax()` - Finds the index of the highest mean Average in `avg_track`.
- `avg_gender["Average"].idxmax()` - Finds the index of the highest mean Average in `avg_gender`.
- `avg_hometown["Average"].idxmax()` - Finds the index of the highest mean Average in `avg_hometown`.
- `.loc[]` - Retrieves the row located at the index of the highest value.
- `highest_track` - Stores the Track with the highest mean Average.
- `highest_gender` - Stores the Gender with the highest mean Average.
- `highest_hometown` - Stores the Hometown with the highest mean Average.
- `f"..."` - Creates a formatted string containing values from the calculated results.
- `:.2f` - Displays the calculated Average up to two decimal places.
- `print()` - Displays the three statements.

```Python
# Look for the category with the highest mean Average
highest_track = avg_track.loc[avg_track["Average"].idxmax()]
highest_gender = avg_gender.loc[avg_gender["Average"].idxmax()]
highest_hometown = avg_hometown.loc[avg_hometown["Average"].idxmax()]

# Display all of the three statements
print(
    f"{highest_track['Track']} has the highest mean Average"
    f"among the track categories at {highest_track['Average']:.2f}"
)
print(
    f"{highest_gender['Gender']} has the highest mean Average"
    f"among the gender categories at {highest_gender['Average']:.2f}"
)
print(
    f"{highest_hometown['Hometown']} has the highest mean Average"
    f"among the hometown categories at {highest_hometown['Average']:.2f}"
)
```



**I APPRECIATE FOR TAKING THE TIME TO READ THIS**

Click the link below to see the full main Python program:


# **Readme File Version History:**

September 17, 2026 - initial Readme Content uploaded

September 17, 2026 - final Readme Content uploaded

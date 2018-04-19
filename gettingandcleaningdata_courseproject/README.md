# README for Course project for the Coursera/Johns Hopkins Getting And Cleaning Data course

Please also examine the Code book provided in the file CodeBook.md. It explains the objective of this project, the input data used and the output data that is generated by the script described below.

## Usage summary ##
In short, run the run_analysis.R script in the data directory (called 'UCI HAR Dataset' when unzipped with the usual Bash unzip, see below) by sourcing the file in R and running run_analysis().

## The script: run_analysis.R ##
The script, written in R and called run_analysis.R, should do the following:

1.  The data set has been divided in two pieces, see the code book. Merge back together.
2.  Select only the data for measurements related to mean and standard deviation.
3.  Make sure activities are labelled with text, and that the measurements have descriptive names.
4.  Write a new data set that has the average of each feature, for each activity for each subject.
5.  The data should be written to a .txt file, without rownames.

The script itself contains detailed comments on what is going on in the script. Summary:

1. Check working directory to make sure there is data to be read. If the wd is not the data directory but the dir() function finds a directory by that name, the script tries to change to it. If everything fails, the script stops.
2. Read in the X test and train data and concatenate them by row. This data set has a column for each feature and 10299 observations.
3. Read in the list of feature names and use them as column names for the X data.
4. Select all columns/features related to mean and standard deviation. In the script I discuss some choices that I made regarding the regular expression I used.
5. Add appropriate labels to the data set. The number of columns, 561, were brought down to 66 mean/sd related features. Two new columns need to be added (to the front): the subject the measurement was taken from and the activity this subject was doing. First, the y data is read and concatenated. Next the activity labels are read. The y data are numeric activity labels. They are converted to text by converting them to a factor and then altering the levels to text labels. Next, the subject data is read and concatenated. Now, both the activity text labels and subject labels can be added to the front of the X data. Lastly, the column names for the newly added columns are changed to something appropriate.
6. Calulate the average for each feature, for each subject, for each activity. This means the data is grouped by activity and subject, which yields 18 rows: 30 subjects * 6 activities. For each of this 180 combinations (which occur many times in the 10299 observations) the mean of each feature (column) is calculated. Result: 180 rows and 68 columns.
7. Write the new data set to a .txt file.

## Script requirements ##
To make life a little bit easier, I used the dplyr package. The script does not check if it is installed, rather it warns that loading the package will be attempted and that an error is for the user (probably install the package using install.packages("dplyr") from within R).

The data should be downloaded and unzipped before using run_analysis.R. The script assumes the working directory is the data directory and that the files inside did not change name or directory structure. The script will check if the file 'activity_labels.txt' is present. If it is not, it will check for the presence of a file (directory) called 'UCI HAR Dataset'. This directory name was created by simply unzipping the downloaded (wget) zip file using:

```
unzip getdata%2Fprojectfiles%2FUCI\ HAR\ Dataset.zip
```

with unzip version '20 April 2009 (v6.0)' (according to the man page) run from Bash on LXLE (Ubuntu 12.04.5 LTS).

## Run the script ##
I use:

```
> setwd("path/to/UCI\ HAR\ Dataset")
> source("../run_analysis.R") # that's where my script lives
> run_analysis()
```

from within R.

## Known issues ##
The script assumes a Unix-like OS, I did not take into account Windows-style file paths.

As described above, the script assumes the data directory to be called 'UCI HAR Dataset' and the contents of this directory to be unchanged after unzipping the downloaded data.
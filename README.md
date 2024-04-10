# Bike Sharing Assignment
This assignment is about building a Multipe Linear Regression Model for a bike rental company called BoomBikes in the US.  Company had a considerable dips in their revenues due to the Corona pandemic. It aims to come up with a business model to accelerate its revenue and to find out what variables are significant in predicting the demand for shared bikes.


## Table of Contents
* [Project Details and Approach](#project-details-and-approach)
* [Technologies Used](#technologies-used)
* [Conclusions](#conclusions)
* [Acknowledgements](#acknowledgements)


## Project Details and Approach
The primary objective of the project is to come up with a best fit linear regression model that will identify the variables and their correlation coefficients which contribute towards predicting the value of target variable - number of bike rentals. This model would help the company's management to make informed decisions and to come up with strategies to increase their revenue.  

The data set provided includes data for 2 years (2018 and 2019) which contains the day of the week, the month, year, season (Spring, Summer, Fall, Winter), whether the day is a holiday or a weekday, whether it is a working day, what the temparture and feeling temperature is for that day, humidity, weather situation (Clear, Cloudy, Light to moderate rain/snow, Heavy rain/snow), windspeed. Additionally, the data set contained the number of bike rentals - how much of it were from registered customers with the company and how much was of casual nature. The count of these two values were also provided.

From the given data set, the following approach was taken to build the model:
  Step 1: Reading and Understanding the given data 
       -  There were 730 rows and 16 columns provided in the data set and there were no null values present in any of the columns.
       -  Identified which columns were not relevant for the modeling. For instance, index column called instant was not releavat and so was dteday which contained only the dates
        - Similary the column cnt is just a sum of columns Casual and Registered. Hence Casual and Registered columns need not be present for the analysis

  Step 2: Cleaning Data
       - Drop the columns that are not required - instant, dteday, casual, registered

  Step 3: Visualizing the Data
        - Check for any outliers in the indepedent variables with continuous variables - temp,atemp,hum,windspeed
        - Check for relationship between these independent variables to find out if there is any linearity amongst tehm
        - Do a Pair plot analysis to find relationship between all numeric variables in the dataset
        - How the data in categorical variables - season, yr, mnth, holiday, weekday, workingday, weathersit are present and if there are any outliers
        
          After performing the above analysis, concluded that:
          a. Fall Season (with value 3) seems to have highest demand amongst all seasons
          b. Demand for bikes have increased year-on-year
          c. September month seems to have highest demand for bike rentals
          d. Demand for bikes are less during holidays
          e. Number of Bike rentals does not seem to vary much whether it is a weekday or not
          f. Clear weathersit (value=1) has the higest demand
          g. Demands are rising steadily from Jan to Sep and decreases afterwards.

   Step 4: Data Preparation for multi-linear regression modelling
          - Identify categorical variables for which dummy variables need to be created - season, mnth, weekday, weathersit
          - Create those dummary varaibles and add to the original dataset
          - In all, season had 3 dummy variables created, mnth had 11, weekday had 5 and weathersit had 3. This is after dropping one of the variables in each one, as they are redundant. 
           - After the dummy variable creation on these categorical varaibles, the original columns are also dropped from the main dataframe

    Step 5:  Splitting the Data into Training and Testing Sets
          - The data was split into training and test data sets with a 70:30 ratio
          - Applied the min-max scalar approach to bring the independent variables with continous values - temp, atemp, hum, windspeed and cnt
          - Plotted a heatmap among all numeric variables to find the correlation between each of them
          - Based on this, observed that temp and atemp variables are correlated at 99% with each other and about 64% and 65% percent with the target variable - cnt

    Step 6: Building the Model
           - The model building happened on the training dataset
           - Started with one variable - atemp and did a scatter plot against the target variable - cnt and found that they are linear. We got the R-square value of 0.418 in the first attempt.
           - In the next step, added temp variable and ran the model and got the R-Squared value of 0.419
           - In the third step, added yr variable and the model produced the R-square value of 0.696
           - After this, included all numeric variables in the data set and ran the model. The R-square value was 0.853. 
           - In the next step, did a VIF check on these variables to look for any abnormality in the data such as multicollienearity
           - There were variables with VIF value as Infinity and removed the 1st variable - thu from the dataset
           - After re-running the model again, there were no VIF value showing Infinity but there were variables which had higer p-values
           - The iteration continued for 17 times until all the p-values were in acceptable range and VIF values (<5>).
           - The final model had a R-Squared values of 0.782

    Step 7: Residual Analysis of the train data
            - Plotted the histogram on the error terms with a mean of 0
            - Ensured that the values are normally distributed
    Step 8: Making Predictions Using the Final Model
            - So far, all the analysis were done on Training set. Applied the scalar min-max approach for the same variables on the test data set
            - Predicted the model thus derived on the test dataset
     Step 9: Model Evaluation  
            - Plotted scatter plot on the test data set aginst the predicted dataset and found that they are linear in nature
            - This is a evidence that model thus derived should be an acceptable one
     Step 10: Find R square score for the test set
             - R-square value of the test data set after applying the model came out to be 0.773
             - The difference between the training and test dataset was 0.782 - 0.773 = 0.09, which is in the acceptable range
             - Hence concluded that this is the best fit model based on the anlaysis done   


## Conclusions
After completing the analysis, the following observations were interpreted:

a. Company should focus on fall season and then by summer where the co-efficients are high

b. Bike rentals are significant during the months of August to September. Management can make a note of this and strategize marketing around these months to promote sales for rentals

c. Model predicted that the number of rentals have gone up from 2018 to 2019. If the company can maintain focus, they could expect higher number of rentals in subsequent years

d. Saturday of the week seems to have spike in rentals

e. Weather situation of mist and light rain will have an impact on the rentals. Company can consider this while running advertisement campaign to boost sales

f. People have rented bikes during working days. Management can look into this aspect as well.


## Technologies Used
- python 3.11.5
- numpy 1.24.3
- pandas 2.0.3
- matplotlib 3.7.2
- seaborn 0.12.2
- Jupyter Notebook 6.5.4
- scikit-learn 1.3.0
- statsmodels 0.14.0

## Acknowledgements
References 
- stackoverflow and geekforgeek websites for python examples
- Course materials from upGrad curriculam


## Contact
Manikandan Krishnamurthy Vembu (https://github.com/manikvgithub)

# Effects of Customers on Bike Rental Patterns
## Data Exploration - Ford GoBike System Data Analysis
### *Jhonatan Nagasako*
#### *28-FEB-2021*

-----
# A. INTRODUCTION

This notebook will focus on the **data EXPLORATION** of Ford GoBike System. Data source can be found via [Udacity provided link to Google Docs/Drive](https://docs.google.com/document/d/e/2PACX-1vQmkX4iOT6Rcrin42vslquX2_wQCjIa_hbwD0xmxrERPSOJYDtpNc_3wwK_p9_KpOsfA6QVyEHdxxq7/pub?embedded=True).

This data set includes information about individual rides made in a bike-sharing system covering the greater San Francisco Bay area.
* Note that this dataset will require some data wrangling in order to make it tidy for analysis. There are multiple cities covered by the linked system, and multiple data files will need to be joined together if a full year’s coverage is desired.

Questions to consider:
1. As a customer, when is it a good time to schedule a bike ride to avoid the rush (high influx of customers)?
2. As a shop owner, how should you strategically schedule your employees to ensure enough staff is present to assist customers?
3. As a shop owner, how can I exploit customer renting patterns to adjust prices of rides (e.g., bike-use-time/hr) or create discounts?

*The analysis endeavored below will address these questions, specifically in the conclusion section of this report*
-----

## Investigation Overview

In this investigation in to the Ford GoBike system (i.e., bike renting service), I'm most interested in figuring out critical times and dates which high frequency of customers is expected. Thus, allowing strategies to be developed to create targeted marketing and lean staffing schedules.

The following features that will have the strongest effect in developing these strategies is by analyzing
1. Age
2. Gender
3. Ride duration
4. Days bikes rented
5. Times bikes rented

New features were created for time and date as required. The final cleaned and tidied data was exported as a `master.csv file`, then read back into the report as a `df`.

## Dataset Overview

There are 183,215 ride entries in the dataset with 27 features (see above for details). Most variables are categorical in nature (specifically a data type of string). Data extraction of date, date day, and time (hr, min, etc.) was broken apart from the `start_time` and `end_time`.

Also, the following assumptions were made for the data. First, the data only considers a two month span, Feb and Mar. secondly, the ride's start-days vs end-days were practically the same day. Lastly, the analysis of different locations which rides occurred is out of scope of this data project.

-----

## Univariate Exploration
## Figure 0 - Age Distribution of Riders

1. The data was trimmed to 100 years old based on research of oldest living person. As expected, that data is right skewed. Interestingly enough, the 95 percentiles was 55 years old, despite the maximum being 100 years old. The 5th percentile rider age was 22 years old. The mean age of riders (regardless of gender) was about 34.2 years old.
2. No transformations additional transformations was required for the data analysis.
3. There was ages with "0 years old" and also astronomically old ages calculated.
4. Data was filtered to remove ages less than 1 years hold and trimmed to 100 year old (based on research of the 2010 U.S. Census Bureu). Ages with 0 years old calculated is unlikely to have the ability to ride a bike... This was supported by the fact that the 5th percentile rider's age was 22 years old. Additionally, for the scope of this report 100 years old was chosen based on the fact that the 95th percentile rider's age was 55 years old.

## Figure 1 - Top Days to START a Bike Ride

1. The day of the week was reviewed to determine what day had the highest in flux of customers. Most notably Tuesday through Thursday were the most popular days to rent bikes--Thursday being the most with 35176 customers overall. Conversely, Saturday through Monday were the least--Saturday being the least with 15,377 customers.
2. No transformations additional transformations was required for the data analysis.
3. It was unusual to see the weekend (Sat and Sun) as the lowest count of customers. As compared to Thursday, which is in the middle of the work week--perhaps the job title of customer should be collected to understand if customers are "working professionals" vs "students".
4. No additional cleaning was required for the dataset after initial cleaning, details shown in Section 2 - Assessing Data (Cleaning and Tidying)

## Figure 2 - Top Times to START a Bike Ride

1. Unusual points seen with the data that there were customers renting bikes as late as 12am (925 customers) and early as 5am (896 customer--which was the min time count). The average of these two times compared to the 5pm (21,874 customers--which was the max time count), was almost 12 times least popular.
2. No transformations additional transformations was required for the data analysis.  
3. The top 5 times to rent bikes, in order: 5pm, 8am, 6pm, 9am, and 4pm. So looking at this dataset from a different perspective, popular morning times were between 8am-9am, then later in the afternoon/evening popular times were between 4pm-6pm.
4. Additional cleaning of the time data was required. Initially this data was set as a string. The time string was then stripped to its hour portion.

## Figure 3 - Top Times to END a Bike Ride

1. Interestingly, the data distribution was almost the same as shown in Figure 2. The only difference in order was between, while data was sorted max to min, column 6 to column 11 (as shown by the red lines on the bar chart). This indicates that the time of rides were typically completed within the same hour.    
2. No transformations additional transformations was required for the data analysis.
3. Similarly, the data distribution was almost the same as shown in Figure 2. The only difference in order was between, while data was sorted max to min, column 6 to column 11 (as shown by the red lines on the bar chart).    
4. Additional cleaning of the time data was required. Initially this data was set as a string. The time string was then stripped to its hour portion. This indicates that the time of rides were typically completed within the same hour.

## Figure 4 - Time Spent Riding Bike

1. This analysis was a verification step to the posit stated from the discussion of Figure 3. Figure 4 confirms that most ride durations on average was about 12.1 minutes long. The 5th percentile ride duration being 2.8 minutes, and the 95th percentile ride duration being 26.2 minutes.
2. No transformations additional transformations was required for the data analysis.
1. When review the feature of time, hours was not reviewed in greater detail because Figure 4 confirms that most ride durations on average was about 12.1 minutes long. In fact, the 5th percentile ride duration being 2.8 minutes, and the 95th percentile ride duration being 26.2 minutes. Therefore, it was more meaningful to do a distribution of ride duration as minutes instead of hours.
2. No additional cleaning was required for the dataset after initial cleaning, details shown in Section 2 - Assessing Data (Cleaning and Tidying)    


-----
## Bivariate Exploration
First, it was interesting to note that the few customers that identified their gender indicated a gender of "other". However, the data scientist respects the gender identity of those participating in the bike renting service.

When reviewing gender to the age of the customer population, as shown in Figures 5, there appears no discernable difference between the different genders. The female population may be representative of the total mean of about 35 years old, and slightly higher when compared to male and other classifications. However, a t-test is required to confirm if these differences are statistically significant.

When reviewing gender to the ride duration population, as shown in Figures 6, similarities in spread between female and other classifications was noted. Average ride time between female and other classifications being about 9.5 minutes. When comparing to the male population, the male group tended to have shorter rides. However, a standard t-test would need to be performed for confirmation.  

Other features, such as location of where bikes were rented was out of scope for this report. Therefore, exploratory analysis only focused on the feature(s) of interest--as stated at the beginning of the analysis.    

Figure reference for bivariate exploration
Figure 5 - Age Distribution of Different Genders
Figure 6 - Duration of Ride Distribution of Different Genders

-----
## Multivariate exploration

Multivariate exploration of subscriber vs non-subscriber, in respects to time and day bikes were rented, verifies prior observations noted in univariate discussion. Comparing Figure 2 (the univariate analysis of the distribution of times when bikes were rented) to Figure 7, the multivariate analysis confirms that most customers tend to rent bikes between 8am-9am, then later in the afternoon/evening popular times were between 4pm-6pm. However, when making the count of customers as the z-axis, and plotting those counts on a time-rented to day-rented x-y plan, it is striking to see that this assertion applies generally to Wednesdays to Fridays. Furthermore, when comparing Figure 1 (the univariate analysis of the top days to rent bikes) the multivariate analysis shown in Figure 7 shows almost no riders renting bikes on Tuesdays (which was the second most popular day customers rented bikes)! This observation can be explored further in a future analysis of the data.

The observations noted above is applicable to both customer (non-subscriber) and subscriber riders. The only difference notated was that customer (or non-subscribers) tend to rent bikes more frequently on the weekends (Saturday and Sunday) as opposed to riders with a subscription.

Taking the extension of this analysis above and applying it to the identified genders in this study indicates similar heatmaps between males and females, as shown in Figure 8. The male and female heatmap, compared to Figure 7, tend to follow the heatmap pattern of a subscriber identification. The other gender classification tended to be more spread and did not have the same heatmap shape of the males and females. This may indicate that the other classification is a part of both the non-subscriber and subscriber identification groups. This observation can be explored further in a future analysis of the data.

Figure reference for bivariate exploration
Figure 7 - Age Distribution of Different Genders
Figure 8 - Duration of Ride Distribution of Different Genders
-----

## Conclusion

In conclusion, when review the question asked at the initial phase of this study, the data scientist has the following recommendations for the following questions below.

Questions to consider and recommendations:
1. As a customer, when is it a good time to schedule a bike ride to avoid the rush (high influx of customers)?
    - Customers that want to have a leisure ride with the least amount of people riding bikes should consider renting bikes on Saturdays and Sundays.


2. As a shop owner, how should you strategically schedule your employees to ensure enough staff is present to assist customers?
    - The owner should consider having staff members ready for high customer rate seen between Wednesday to Thursdays. However, further data and analysis is required to determine if Tuesdays is truly a high frequency rental day. Discounts can be applied to Saturdays and Sundays to encourage customers to rent on the weekend.


3. As a shop owner, how can I exploit customer renting patterns to adjust prices of rides (e.g., bike-use-time/hr) or create discounts?
    - The owner can explore targeted advertisement to attract age groups around 18 and 25. Further data is required, but this age group may have potential revenue when review Figure 5. Additionally, targeted advertisement to genders may not be required because the spread of these types of customers are similar, albeit additional statistical t-tests are required to determine if this would in fact be significant.
    - The shop owner should also consider and review internally why subscribers to bike services tend to rent bikes less on the weekends. Further data is required, but this lower renting participation rate from subscribers, as shown in Figure 7, maybe indicative that subscribers are working professionals that uses these bikes to work Monday-Friday.

-----
# End of Data Project!

Made with ❤️ by Jhon!

Further impovements include...
1. Validation statements using `assert` clauses to confirm that data manipuation is correct during cleaning stage
2. More plots exploring data
3. Adding helpful annotations to plots
4. Hypothesis Testing, to determine the statisticaly significance of various features (age, gender, etc.) to determine if different times/dates affect customer interaction
5. Multivariate and univariate comparison and confirmation

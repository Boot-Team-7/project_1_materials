# MY PARENTS KICKED ME OUT! Where do I go now?

## Table of Contents

* [Background Story](#background-story)
* [Data Team](#data-team)
* [Inital Data Exploration & Gathering](#initial-data-exploration-and-data-gathering)
* [Analysis](#analysis)
* [Recommendations](#recommendations)
* [List of Data Sets Used](#references) 


## Background Story:  

In our latest "Ask the Data Experts" blog, we received the following question from Paul, who just got kicked out of his parent's house in Decatur, Georgia:

> "Having spent many years with my parents, they finally decided to kick me out! :worried: But where do I go now? Do I stay in Georgia or move to another State? Should I look for a studio or a 1 bedroom apartment? Would you all be able to use data to help me with some recommendations?" - Paul (29 years old)

When digging further into Paul's preferences, he mentioned the following:
- Affordability is important.
- Open to living with or without roomates.
- Most of his friends and family live in Georgia, but he's open to moving to another state if needed.
- Wants to feel safe
- Paul is a homebody - but he wants to make sure there's things to do whenever he feels like getting out of the house! 

## Data Team: 

To help answer Paul's question, we've assembled a team of 9 of our best data experts:
- Maheen Abdulwaheed
- Huda Alghazouli 
- Andres Almaraz
- Gautam Iyer
- William M Mills
- Ashley Moore
- Sarje Page
- Vinika Patel
- Sheyla Perez Nazco

## Initial Data Exploration and Data Gathering: 

Our initial data exploration phase started by exploring some of the data sets available on the United States' Office of Policy Development and Research [website](https://www.huduser.gov/portal/about/mission_and_background.html). 

In this website, we were able to find the following [data sets](https://www.huduser.gov/portal/datasets/50per.html#2022), which contain median rent estimates for all of the different counties in the United States (and its territories). The rent estimates are for studios, 1 bedrooms, 2 bedrooms, 3 bedrooms and 4 bedrooms. 

Since we wanted to give Paul the most up to date information, we focused on 2020-2022 data. We saved the different csv files (2020, 2021, 2022) in the following [folder](/Consolidated_new/UTF/). 

## Analysis

### Setting Up the Data

The first step that we took in our [Jupyter Notebook](/Consolidated_new/Project_Group_7.ipynb) was to read the 3 different CSV files (2020-2022):

- `rents_2020 = pd.read_csv("UTF/FY2020_50_County_rev.csv")`
- `rents_2021 = pd.read_csv("UTF/FY2021_50_County.csv")`
- `rents_2022 = pd.read_csv("UTF/FY2022_FMR_50_county_rev.csv")`

We were then able to merge the 3 CSVs files into one DataFrame by merging 2020 with 2021, and then merging 2020-2021 with 2022:
- `rent_20_21_22 = pd.merge(rent_20_21, rents_2022, how="left", on=["state", "county", "cousub"])`

We also loaded the following [file](/Consolidated_new/Other_Files/rent.csv), which contains the same data but formatted in a different way. We converted this DataFrame into a new summary DF (rent_summary_sy), which groups the average rents by state and year. This will be used later in the analysis to calculate the YoY % change in rent.

### Data Cleaning

After merging the data, we reduced the DataFrame to only the necessary columns, renamed the columns, and dropped null values from the data. 

After we cleaned our data, we were left with the following 20 columns:
- **state**  →  displays state ID 
- **county**  →  displays county ID
- **county name**  →  displays name of the county
- **state initial**  →  displays initial of the state (e.g. TX stands for Texas)
- **studio_2020**  →  median rent price for a studio in 2020
- **studio_2021**  →  median rent price for a studio in 2021
- **studio_2021**  →  median rent price for a studio in 2022
- **bedroom_1_2020**  →  median rent price for a 1 bedroom in 2020
- **bedroom_1_2021**  →  median rent price for a 1 bedroom in 2021
- **bedroom_1_2022**  →  median rent price for a 1 bedroom in 2022
- **bedroom_2_2020**  →   rent price for a 2 bedroom in 2020
- **bedroom_2_2021**  →  median rent price for a 2 bedroom in 2021
- **bedroom_2_2022**  →  median rent price for a 2 bedroom in 2022
- **bedroom_3_2020**  →  median rent price for a 3 bedroom in 2020
- **bedroom_3_2021**  →   rent price for a 3 bedroom in 2021
- **bedroom_3_2022**  →  median rent price for a 3 bedroom in 2022
- **bedroom_4_2020**  →  median rent price for a 4 bedroom in 2020
- **bedroom_4_2021**  →  median rent price for a 4 bedroom in 2021
- **bedroom_4_2022**  →  median rent price for a 4 bedroom in 2022
- **pop_2017** ->  county population (as of 2017)

Our new cleaned DataFrame was exported into a csv [file](/Consolidated_new/Merged_Data/rent20-22.csv):
- `cleaned_rent_20_21_22.to_csv("Merged_Data/rent20-22.csv")`

### Analysis

### If Paul decides to live alone, should he go for a studio or a one bedroom apartment?

The first question that we wanted to help Paul with was whether he should go for a studio or one bedroom apartment. We know that affordability is important to Paul, but he also wants to live comfortable, is it worth it to get a one bedroom apartment?

In order to help answer this question, we calculated the average rent per number of bedrooms, focusing on 2021 data, and created a bar plot: 

![image](/Consolidated_new/Screenshots/Screenshot%201.png)

    As expected, the average rent for a one bedroom is more expensive than a studio apartment. However, the increase in rent is only 10%. Therefore, we recommend Paul goes for a one bedroom apartment so that he can live more comfortable. 

**First Recommendation**: Paul should move to a 1 bedroom if he decides to live alone.

### What is the variability in rent prices for the different bedroom types (studio, 1, 2, 3 or 4 bedroom)? 

We were also curious about the variability of the different bedroom types. Is there more variability in 4 bedrooms compared to 1 bedrooms? 

To answer this question, we created a boxplot that shows rent price for each number of bedrooms:

![image](/Consolidated_new/Screenshots/Screenshot%202.png)

    Based on the boxplots, studios and 1 bedrooms have less variability in rent prices. 4 bedrooms have the highest variability. 

### How have rent prices changed per state YoY? (% Increase)

Since we want to ensure that Paul moves to an affordable state, we analyzed how rent prices had increased YoY (2020 vs. 2021) for 1 bedrooms across each of the states. We visualized this using a bar plot:

![image](/Consolidated_new/Screenshots/Screenshot%203.png)

    From 2020 to 2021, the majority of states experienced a YoY increase in rent prices, with the exception of AK, SD, VT, WV and WY. California and Rhode Island had the biggest YoY increase in rent, indicating that these wouldn't be good options for Paul if affordability is very important. While Georgia's rent prices also increased YoY, they did so a slower pace than many other states. 

### What are the top 5 most expensive states by rent price? What are the top 5 least expensive states by rent price? 

While YoY changes in rent prices are important, we also checked which states were the most and least affordable. We created an average rent for all of the different bedroom types and figured out the 5 most expensive and 5 least expensive states (using groupby functions).  

Top 5 Most Expensive States by Rent Price:

![image](/Consolidated_new/Screenshots/Screenshot%204.png)

    Hawaii, DC, Massachussets, California and New Jersey were the 5 most expensive states based on rent estimates for 2021. 

Top 5 Most Affordable States by Rent Price:

![image](/Consolidated_new/Screenshots/Screenshot%205.png)

    Puerto Rico, Arkansas, Mississipi, Missouri and Kentucky are the least 5 expensive states based on rent estimates for 2021.

We also wanted to plot the most and least expensive states for 1 bedrooms into a heatmap. We imported a [file](/Consolidated_new/Other_Files/state_coordinates.csv) containing the different coordinates (lat, lng) for each of the states. We merged the coordinates with the state DataFrame and used the gmaps API.

Top 5 Most Expensive States Plotted on Heatmap:

![image](/Consolidated_new/Screenshots/Screenshot%207.png)

Top 5 Most Affordable States Plotted on Heatmap:

![image](/Consolidated_new/Screenshots/Screenshot%208.png)

**Second Recommendation**: Paul would prefer to stay in GA, since his friends and family live there. While Georgia's rent prices did increase YoY, they did so at a slower pace than many of the other states. Georgia is also not in the list of the 5 most expensive states. Based on all of these factors, we recommend Paul stays in Georgia.

### Within Georgia, what are the most expensive and least expensive counties based on the median rents of 1 bedrooms? 

Georgia has 156 counties, a lot of information for just one chart. Therefore, we created 3 different bar charts, organized into alphabetical order.

Median 1 Bedroom Rent for the First 50 Counties (Appling to Echols County):

![image](/Consolidated_new/Screenshots/Screenshot%209.png)

Median 1 Bedroom Rent for the Second 50 Counties (Effingham to Mitchell County):

![image](/Consolidated_new/Screenshots/Screenshot%2010.png)

Median 1 Bedroom Rent for the Last 56 Counties (Montgomery to Worth County):

![image](/Consolidated_new/Screenshots/Screenshot%2011.png)


Based on the bar charts above, there are some counties that may not be suitable for Paul (e.g. Fulton) as they have a high median rent price for 1 bedrooms.

### Within Georgia, what are the most expensive and least expensive counties based on the median rents of 1 bedrooms? 







## Recommendations


## References
- US Department of Housing and Urban Development (2022). 50TH PERCENTILE RENT ESTIMATES 2019-2022. Retrieved July 21, 2022, from https://www.huduser.gov/portal/datasets/50per.html#2022
- Google Developers (2012, January 20). Public Data - States. Retrieved July 21, 2022, from https://developers.google.com/public-data/docs/canonical/states_csv
- List of Georgia Counties with County Seats (2014). Retrieved July 26,2022, from https://www.downloadexcelfiles.com/ge_en/download-excel-file-list-counties-georgia#.YuhfpOzMKw4
- Georgia Bureau of Investigation (2022, March 2). 2020 Summary Report Uniform Crime Reporting (UCR) Program Georgia Crime Information Center. Retrieved July 21, 2022, from https://gbi.georgia.gov/services/crime-statistics
- ASQ.org (2022). Nominal Group Technique. Retrieved July 21, 2022, from https://asq.org/quality-resources/nominal-group-technique#:~:text=Nominal%20group%20technique%20(NGT)%20is,idea%20they%20feel%20is%20best.

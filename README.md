# MY PARENTS KICKED ME OUT! Where do I go now?

## Table of Contents

* [Background Story](#background-story)
* [Data Team](#data-team)
* [Inital Data Exploration & Gathering](#initial-data-exploration-and-data-gathering)
* [Analysis](#analysis)
* [Recommendations](#recommendations)
* [Team Coordination](#team-coordination)
* [List of Data Sets Used](#data-sets-used) 


## Background Story:  

In our latest "Ask the Data Experts" blog, we received the following question from Paul, who just got kicked out of his parent's house in Decatur, Georgia:

> "Having spent many years with my parents, they finally decided to kick me out! :worried: But where do I go now? Do I stay in Georgia or move to another State? Should I look for a studio or a 1 bedroom apartment? Would you all be able to use data to help me with some recommendations?" - Paul (29 years old)

When digging further into Paul's preferences, he mentioned the following:
- Affordability is important.
- Open to living with or without roomates.
- Most of his friends and family live in Georgia, but he's open to moving to another state. 
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

Since we wanted to give Paul the most up to date information, we focused on 2020-2022 data. We saved the different csv files (2020, 2021, 2022) in the following [folder](/50TH-Percentile-Rent-Estimates-Data/UTF/). 

## Analysis

### Setting Up the Data

The first step that we took in our [Jupyter Notebook](/Consolidated/Project------Kicked%20OUT!!.ipynb) was to read the 3 different CSV files (2020-2022):

- `rents_2020 = pd.read_csv("UTF/FY2020_50_County_rev.csv")`
- `rents_2021 = pd.read_csv("UTF/FY2021_50_County.csv")`
- `rents_2022 = pd.read_csv("UTF/FY2022_FMR_50_county_rev.csv")`

We were then able to merge the 3 CSVs files into one DataFrame by merging 2020 with 2021, and then merging 2020-2021 with 2022:
- `rent_20_21_22 = pd.merge(rent_20_21, rents_2022, how="left", on=["state", "county", "cousub"])`

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

## Recommendations

## Team Coordination

## Data Sets Used

## References
- US Department of Housing and Urban Development (2022). 50TH PERCENTILE RENT ESTIMATES 2019-2022. Retrieved July 21, 2022, from https://www.huduser.gov/portal/datasets/50per.html#2022
- Google Developers (2012, January 20). Public Data - States. Retrieved July 21, 2022, from https://developers.google.com/public-data/docs/canonical/states_csv

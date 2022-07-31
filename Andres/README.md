## Seeing if the population affects the rent prices in Georgia
## Population vs. Rent Price 2021
## I dont want to see people and want low rent costs/I like people and dont care about the prices
At the start, using the cleaned data for 2020-2022 that was made and filtered the dataframe to 
only Georgia rows. *The first thing I did after that was create a boxplot for the rent prices 
for the amount of bedrooms there were to it. Orginally I wanted to have the boxplots combined with 
population, but I learned that wouldn't work so I left it how it is now. (This can be removed)* 
From the dataframe, I focused on the rent prices on 2021 of each bedroom amount compared to the 
county's population they are in. With that I made a scatter plot with a regression line to 
see if there was a correlation between those two aspects. From this I saw that all the graphs had 
a linearly postive correlation between bedroom rent prices and population. However, they all had a 
r value between .50-.53 meaning that there is not a strong nor weak. Which leads me to say, that 
the correlation strength is not quite strong enough to stand behind. From there, using gmaps to 
get the coordinates of each of the counties to use to make a heat map by popluation. I also 
added markers of the top and bottom five rent prices for one bedroom places to their county.

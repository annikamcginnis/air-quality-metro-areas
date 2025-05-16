# Calculating average PM2.5 levels per the largest metro areas in the U.S. and creating an Observable heat map: [Visualization](https://observablehq.com/d/d4fc67b6f2c423ef)

## Goal
- To understand the general trends in particulate matter (PM2.5) air pollution in major metropolitan areas in the U.S., especially those that have experienced the highest recent population growth
- To explore creating a heat map using Observable

## Main Findings
- As PM2.5 regulations under the National Ambient Air Quality Standards (NAAQS) have become more stringent, with new limits set in 1997, 2006, 2012, and 2024, the average levels of PM2.5 in most major metropolitan areas (> 1 million population in the 2023 ACS survey) have decreased significantly. In the Baltimore-Columbia-Towson area for example, average annual rates of PM2.5 declined by 84 percent from 1999 to 2024.
- There appears to be a slightly slower decrease in air pollution for cities that have experienced more population growth in the last 10 years (2014-2023) compared to cities that experienced less growth.

## Data Collection
- I sourced population data for 2023 from the [U.S. Census Bureau](https://data.census.gov/table?q=B01003&g=010XX00US$31000M1&y=2014) from the 2014 and 2023 ACS 5-Year Estimates Detailed Tables for Metropolitan areas.
- I sourced PM2.5 air quality monitoring data from Environmental Protection Agency data on PM2.5 FRM/FEM Mass (88101). Each row is a separate monitor and monitoring period across the entire United States. Separate data files were downloaded for each year from 1980-2024.

I merged the population data for 2014 and 2023 using fuzzy matching to match metro areas that had slightly revised names. 
I merged together the annual datasets for EPA PM2.5 monitoring data from 1980-2024. 

## Data Analysis and Visualization
I used the following languages, libraries, and applications in my data cleaning, analysis and visualization: 
- Python
- Pandas
- fuzzywuzzy
- JavaScript
- Observable

I conducted my data analysis in Python using the Pandas library. I filtered the metro area data by areas with greater than 1 million population in 2023. I created a new variable calculating population percentage change from 2014-2023 and sorted the dataframe by this variable.

I used fuzzy matching to merge together the population data and the air quality data with an accuracy score of greater than 92 percent, based on my assessment of individual matches. 

I filtered by metropolitan areas greater than 1 million and by 24-HOUR readings, grouped by state and year, and calculated the average air quality reading for each state per year. 
I sorted this dataframe in order of population growth from 2014-2023.

In Observable, I forked [this heat map project](https://observablehq.com/@observablehq/plot-impact-of-vaccines) that replicated a Wall Street Journal visualization. I modified the JavaScript code to visualize average PM2.5 levels per major metropolitan area per year to create [this visualization](https://observablehq.com/d/d4fc67b6f2c423ef), where darker years represent higher PM2.5 values. I added in lines for the years when federal PM2.5 regulations were strengthened. 

## Reflection

This project gave me a chance to improve my skills in sourcing and combining census data with other data. I needed to use the main census website instead of Census Explorer because I needed data from multiple years. I also tried fuzzy matching for the first time, and it was a learning experience. At first, my similarity score was set too low (around 85%) and I realized many places were being wrongly matched. I tried out a few different scores until it appeared most matches were accurate. However, there could have been some that were missed. I lost about 13 major metro areas when I fuzzy matched the metro areas from the census data with the monitoring data from EPA. This needs more work to understand if those metro areas were not included in the EPA data, were under different names that fuzzy matching couldn't match, were divided into different geographies, or were somehow missed in the original EPA data merging.

I also explored using Observable and JavaScript for the first time here. It was relatively easy (with some AI support) to understand and apply the basics of JavaScript by forking and modifying an existing visualization. I saw that I needed to first format my data in long format, which I did in Python. This was also the first time I tried making a heat map, and although the result isn't as stark as the vaccines visual, I think it still shows a pretty clear trend in air quality reduction. I considered shortening the names of the metro areas, but I didn't want to simplify them so much to lose the multi-cities information (when a metro area covers several major cities and towns) - so for the moment I left them with their full names, but I'm open to revising this.

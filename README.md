# Madison Landlord Lookup Tool

This project scraped property owner and value information from the city of Madison Wisconsin Assessor's Office website, cleaned it, plotted it using Mapbox and then deployed it to Heroku.

## Scraping Data

The City of Madison Assessor's Office website allows you to search and obtain data for any commercial or residential property in Madison. In order to ensure that I got data on all available properties, I searched for every single number and letter in the owner lookup tool. This returned a list of all property owners that start with that letter or number. I then manually saved the HTML information on these search results as "A Names", "B Names", etc.. in the data folder. 

Using the Jupyter Notebook called "Data Consolidation", I then looped through all of the search results to find the web addresses for each property's webpage. Another py script in the Jupyter Notebook will visit each of these addresses and extract the owner name, property value, address, property type (Apartment, Condo, etc..) and property class (commerical, residential, etc..). 

## Cleaning Data

In order to properly clean the data, the notebook goes through steps of filling missing values with zeros and removing the dollar sign from the property values. For the purposes of this project, I combined both Condos and Apartments as "Apartments". This is because the owners of these condos according to the Assessor's website are often the owners of the building.

The most important aspect of the cleaning was finding a proper mapping for owner names. This is challenging because you'll often the same owner with different names depending on the building. Some of these are typos, but most of them are a result of displaying additional information in the owner name, like the address or name of the property manager (who usually works for the property management company). This was the most labor intensive aspect of the project, and I couldn't find a better way to accomplish this except looking for key characters that would indicate something like this happening (# was often used before an address or property manager name) or searching for the biggest rental companies I knew in Madison and seeing if they had a consistent naming pattern. 

Once this owner name cleaning was done, I was able to calculate the number of units from each apartment by parsing the building information. And then I summed the total number of buildings, units, and property value for each owner name. 

At this point, I had to make a decision about which properties should be included in this dataset. I didn't want to include private personal properties, but I still wanted to make sure I was including houses that got split into floors and were leased out, as constitute a majority of the units around campus. For these reasons, I included any apartments or single family homes that were either owned by somebody with multiple properties or had a value over $1 million. This isn't a perfect metric, as there are obviously private homes worth more than $1 million in Madison, but it was the only way I found to ensure the inclusion of large apartment complexes that were, for whatever reason, classified as single family homes. 



## Plotting with Mapbox

## Publishing to Heroku



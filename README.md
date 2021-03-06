# Meeting NYC Women Where They Are: Optimizing Street Team Placement through Exploratory Data Analysis

## Abstract 

WomenTechWomenYes (WTWY) is looking to efficiently place their street teams at NYC subway stations in order to build awareness through email collection prior to their upcoming gala. Using background research from the book *Invisible Women* by Caroline Criado Perez, I focused on identifying stations with high ridership in close proximity to schools and daycares - areas that are commonly visited in women's urban travel patterns. I used MTA turnstile data and location data from stations, schools, and daycares to optimize the WTWY street team schedule. 

To dig deeper into this project, please see:
* The [Jupyter Notebook containing all project code](https://github.com/ninaksweeney/Metis_Project_1/blob/main/Project1_Notebook.ipynb) 
* Final presentation [slides/visuals](https://github.com/ninaksweeney/Metis_Project_1/blob/main/Project1_Presentation.pdf)

## Design

The main goals of WTWY are to build awareness among interested & passionate individuals, fill the upcoming gala, and potentially expose future donors to the cause. I made the decision to focus my efforts on reaching women first - a strategy that could potentially fulfill all three objectives - by ensuring that WTWY is present in women's typical 'trip-chaining' locations. **Trip-chaining**, which comes about as women complete 75% of the world's unpaid care work, is the tendency to do multiple errands in one trip or commute - like grocery shopping or dropping off children at school. By looking at both ridership numbers and proximity to schools and daycares, WTWY can reach a diverse group of women where they already are throughout the week. 

## Data

The [MTA Turnstile dataset](http://web.mta.info/developers/turnstile.html) has a total of 7,335,276 rows belonging to 379 unique subway stations. It gives cumulative entry and exit numbers from each unique turnstile over 4-hour periods. In order to give relevant recommendations and reflect the reality of Covid-19 on both public transit and schooling, I decided to work with turnstile data from Jan-Sept 2021.  

I also incorporated location data for subway stations, schools, and daycares. I matched the [subway station location data](http://web.mta.info/developers/developer-data-terms.html#data) with my turnstile dataset on station name and unique line, giving me latitude and longitude coordinates for 215 total stations. I then filtered the [school latitude/longitude data](https://data.cityofnewyork.us/Education/2019-2020-School-Locations/wg9x-4ke6) to reflect only the age groups that might need to be picked up/dropped off, as well as only open schools. Similarly, I filtered the [daycare latitude/longitude data](https://data.ny.gov/Human-Services/Child-Care-Regulated-Programs-Map/s8uq-s4wq) down to open daycares in New York City proper. 

## Algorithms

After completing some basic exploration and data cleaning in SQL and Pandas, I broke each station out by its line name in order to analyze the locations more granularly. The data had many anomalies, including some turnstiles that counted backwards, and others with unrealistically high entry & exit counts, which I solved for in Pandas. After calculating entries/exits per 4-hour period at each turnstile, I was able to aggregate across turnstile, station, and day, making for a cleaner dataset.   

To begin exploratory data analysis, I first found the most popular stations in the dataset, defining 'ridership' as exits from the station. I used those top 10 stations to get a sense of the patterns in the system, a key insight being that weekends have much lower ridership than weekdays. Given that we're focused on schools and daycares, and want to respect the time of the WTWY staff, I focused specifically on weekdays.  

Next, I added in the station location data, matching on both station name and line. With latitude and longitude connected to each station, I was able to find the proximity of schools and daycares to each station. I defined 'nearby' as within .3 miles as the bird flies, and counted the school/daycare facilities 'nearby' each station. A distribution of those counts showed that most stations have less than 20 facilities nearby, while a select few have more than 80. 

I chose the top 12 stations for WTWY by combining ideal stations (daily ridership > 5000 and nearby facilities >20), with a select few additional stations that are surrounded by schools and daycares (daily ridership > 3500 and nearby facilities > 80). Mapping those stations & facilities in Geopandas shows us that they are spread around Manhattan and the Bronx.   

Finally, I looked at these 12 stations' ridership by time of day, noticing that certain stations might yield more exposure at certain times of day, with higher activity in the afternoon. As a final deliverable, I created an optimal schedule based on ridership volume and school drop off/pickup times for WTWY to test out with their street teams. 


## Tools

* SQLAlchemy and SQLite to query and read turnstile data into Pandas 
* Numpy, Pandas, and Geopy for data manipulation
* Seaborn and Matplotlib for visualizations
* Geopandas for mapping latitude/longitude 

## Communication

I completed a 5-minute presentation of my findings for the client, including both ideal recommendations and more basic starting points that may be more realistic for the WTWY team's bandwidth. Slides and visuals for this project are included in this repository. Future work may include optimizing the street team schedule according to the team's time & day preferences, analyzing success at each station to re-evaluate the schedule, and incorporating demographic location for more accurate targeting. 

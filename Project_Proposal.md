# Project Proposal 
## Optimizing Street Team Deployment According to Gendered Trip-Chaining Behavior  

### Background
In the 2019 book Invisible Women, Caroline Criado Perez argues for the recognition of urban travel as a gendered experience. While men tend to commute to the city center and back, women bear the brunt of the majority of unpaid care work, and therefore are more likely to *trip-chain* - that is, link together multiple errands in one trip, such as picking up a child or tending to an elderly parent.  

WomenTechWomenYes is looking for a data-driven strategy to optimize the effectiveness of street teams placed at subway stations. In short, their goals are to: 
* Gather as many emails as possible to fill the gala with passionate supporters
* Build awareness and reach 
* Introduce WTWY to individuals who may contribute to the cause  

Using MTA Turnstile data and our understanding of women's trip-chaining behaviors, our team plans to target a wide swath of NYC women by identifying the NYC subway locations with: 
1. The highest daily traffic during reasonable daytime hours 
2. The closest proximity to early-age schools and childcare facilities where women may pick up or drop off children during their commute
3. The most consistent traffic volume throughout the day 
<br/><br/>

### Research Question:
How might we optimize the placement of street teams at NYC subway stations to reach individuals who may be interested in, passionate about, and ideally willing to contribute to, the WTWY mission?
<br/><br/>

### Data Description:
- [MTA Turnstile Data](http://web.mta.info/developers/turnstile.html) - at least three months of data showing the volume of subway activity per turnstile, per station in 4 hour increments
- [MTA Station Location Data](http://web.mta.info/developers/developer-data-terms.html#data) - at the given link, navigate to the MTA NYC Transit header, then 'Station Locations'. Latitude, Longitude, and Station Name will be used to anchor the turnstile data geographically in relation to other institutions. 
- [2019-2020 School Location Data](https://data.cityofnewyork.us/Education/2019-2020-School-Locations/wg9x-4ke6) - Latitude & Longitude will be used to find the proximity of subway stations to NYC schools with students who are likely to be picked up by a parent. 
- [Childcare Regulated Programs Data](https://data.ny.gov/Human-Services/Child-Care-Regulated-Programs-Map/s8uq-s4wq) - at the given link, click 'Export' in the top right corner. Latitude & Longitude will be used to find the proximity of subway stations to NYC childcare facilities where parents are likely to pick up children. 


In this project, an individual unit of analysis will be a subway station, and turnstile data will be compiled to show the activity at a given station over the course of a day or a week. School & Childcare data will be used to show the proximity of our subway stations to typical 'trip-chaining' locations during a woman's commute. Features we plan to work with are: 
* Latitude & Longitude
* Turnstile Unit Number
* Turnstile Exit & Entry volume
* Station Names 
* Line Names 
* Date
* Time   

### Tools: 
To meet the tools requirements of this project, we plan to: 
* Enter the raw MTA turnstile data into a SQL database
* Query the database using SQLAlchemy so the data is in a digestable form to glean insights at a station level 
* Complete an analysis of turnstile activity in pandas, as well as proximity to other services 
* Visualize the most valuable locations for the WTWY team based on all attributes   

One tool that is currently unfamiliar that we will use is `geopy.distance`, which we have tested and think it will work well to show the distance in miles between our stations & schools/daycare centers using lat/long coordinates. 

### MVP Goal: 
The MVP of this project will include: 
* An understanding of the highest-volume subway stations, and highest-volume traffic times at those stations
* An initial understanding of station proximity to schools & daycare facilities 



### Introduction

For the first project of the [Metis Data Science Bootcamp](https://www.thisismetis.com/), our group performed exploratory data analysis (EDA) on [New York MTA turnstile data](http://web.mta.info/developers/turnstile.html).



#### Project 1 Team Members

* Una Bayasgalan

* Jacky Lu

* Isaac Wang



##### Project Motivation

Our client is Yankee Doodle. Yankee Doodle is a sports bar looking to expand their catering and delivery business due to the coronavirus. In particular, they want to advertise their Ultimate Deluxe party platter on digitital kiosks in New York's MTA stations to Yankees fans.

Yankee Doodle wants to know the following:

1) Should they advertise in MTA stations?

2) If so, what are the top 5 stations they should advertise in?

We will see which stations have a noticeable difference in MTA turnstile activity (entries & exits) on dates the Yankees have a home game compared to non-game days.

##### Project Submission Directory

Project 1 MTA Work Jupyter Notebook: 

* contains raw data, the data cleaning process, and external data merging
* Code is organized as follows:
  * Prepare DataFrame for raw turnstile data during Yankees 2019 baseball season
  * Create cleaned DataFrame to calculate daily entries and exits and remove negative or higher than threshold values
  * Create DataFrame for Yankee home game dates
  * Create DataFrame for MTA Kiosk stations
  * Merge external data into cleaned DataFrame and save as a pickle file

Project 1 MTA Analysis Jupyter Notebook: 

* contains work to use cleaned data to plot graphs for data visualization
* Code is organized as follows:
  * Open the pickle file with cleaned data
  * Prepare DataFrames for average entries & exits (activity) on game days vs. non game days
  * Plot top 10 and bottom 10 stations by Game:Non-Game Activity Ratio in a histogram
  * Plot Game and Non-Game Day histograms for Yankee Stadium station
  * Plot split violin plots for 5 representative stations to compare activity distributions

slides folder:

* contains our presentation in ppt and PDF format

images folder: 

* contains data visualization graphs for the presentation

pickled_data folder: 

* contains pickle files to quickly access raw and cleaned DataFrames
* unfortunately, this data was too large to include in the GitHub submission

##### Data Science Analysis

1. Data Collection

   [Raw MTA turnstile data](http://web.mta.info/developers/turnstile.html) from March 23, 2019 to October 19, 2019 (Yankees 2019 baseball season) was collected. Extra data sources included obtaining the [Yankees 2019 full game schedule](https://www.mlb.com/yankees/schedule/2019/fullseason) and a [list of MTA stations with digital kiosks](http://web.mta.info/nyct/OntheGoAds/MTA_Kiosk_Ridership_OTG.pdf) available for advertisements.

   

2. Data Cleaning

   Turnstile column names were stripped of extra spaces.

   Turnstile data where the daily entries or exits were calculated to be negative or above a reasonable threshold were removed. The threshold was 86,400 entries per day, which is the same as 1 entry per second.

   Turnstile data where the next day's entries or exits is null were also removed to ensure consistency with our calculations.

3. Extra Data Sources

   Yankees 2019 full game schedule can be found [here](https://www.mlb.com/yankees/schedule/2019/fullseason) 

   We only need the home game dates, so we filtered the game schedules by home game and downloaded to [Google Sheets](https://docs.google.com/spreadsheets/d/1jrYnZN8lfO_pnJ8AFaxkOnoni_EdLOO7Vj3RHeImaMc/edit#gid=89819907). We cleaned the raw data by keeping only the dates column and removing unnecessary information that was in the date cells. We put the dates into a list called "Home_Game" and merged with our main DataFrame.

   In addition to the Yankees home game data, we discovered PDF of MTA stations with digital kiosks available for advertisements.

   The map of the MTA stations with kiosks can be found [here](http://web.mta.info/nyct/OntheGoAds/MTA_Kiosk_Ridership_OTG.pdf).

   We transcribed the list of kiosk stations using the original list of station names in our turnstile data to ensure the names would be the same. We put the names into a dictionary, with the key being "Station" and the values being names of stations. After joining on station name, we created an additional column called "Has_Kiosk", which either have a True or Null value based on the join.

​	

4. Data Calculations

   Daily entries and exits (activity) per station were calculated. The data was filtered on stations that have a digital kiosk. The data was then segmented into days the Yankees had a home game and days they didn't.

   We wanted to know which stations have higher activity on days when the Yankees have a home game.

   For each station, an average daily activity total (entries + exits) was calculated for Yankee game and non-game days. A ratio between the two values was also calculated. If the ratio for a station was much greater than 1, that station had more entries and exits on game days compared to non-game days. If the ratio was around 1, that station had similar entries and exits for game days versus non-game days.



5. Data Analysis & Conclusion

   Only one station, 161/Yankee Stadium had a high activity game:non-game day ratio around 1.7. Around 17 people enter this station on Yankee game days for every 10 people who use this station on non-game days. Almost every other station had a ratio around 1, which meant a similar amount of people use the station on game days versus non-game days. Interestingly, the Mets-Willets station had a much smaller ratio around 0.8. A lot less people enter this station on Yankee game days than normal. 

   

   Our conclusion is that Yankee Doodle should advertise at 161/Yankee Stadium station only. Our data doesn't support advertising at any other stations, and they didn't shouldn't advertise at the Mets-Willets station if they want to advertise to Yankees fans.



6. Data Visualization

| Graph                            | Description                                                  |
| -------------------------------- | ------------------------------------------------------------ |
| bottom_10_active_stations.png    | Bar graph for Game:Non-Game Day Activity Ratios for Bottom 10 active stations |
| top_10_active_stations.png       | Bar graph for Game:Non-Game Day Activity Ratios for Top 10 active stations |
| yankee_stadium_combined_hist.png | Overlaid histograms of Yankee game day and non-game average entries/exits for Yankee Stadium station |
| yankee_stadium_game_hist.png     | Histogram for average entries/exits at Yankee stadium station during game days |
| yankee_stadium_no_game_hist.png  | Histogram for average entries/exits at Yankee stadium station during non-game days |
| yankee_violin_plots.png          | Split violin plots for 5 stations comparing the distribution of activity during game days versus non-game days |

##### Design Decisions

MTA kiosk data was found in a PDF format. Because there were only around 60 stations with kiosks, we decided it was easier to manually transcribe the PDF into a dictionary of station names.

Ratios were chosen to compare game day and non game day activity instead of absolute differences because ratios make it easier to compare popular stations with less popular stations.



##### Additional Notes

Techniques

* Data Visualization
* Exploratory Data Analysis



Programs

* Jupyter Notebook
* Matplotlib
* Numpy
* Pandas
* Seaborn



Language

* Python




# valorant-scraper

# About the Project

<aside>
🖥️ This personal project was conceived last March 2022 during the peak of the recently held **Valorant Champions Tour 2022 Stage 1** in the North American region. This project was inspired by my passion for playing Valorant and watching the best teams perform and display their mechanical and strategical prowess. This project has two goals:

- To primarily collect the data from the recent event and convert it into something that can be used for statistical analysis. The preliminary output of this project is a Jupyter Notebook script that produces an uncleaned CSV file.
- To analyse the performance of each team based on the specific Valorant agent roles (Controller, Duelist, Initiator, Sentinel), and create a dataframe based on these queries.

### Github Link:

</aside>

# Collecting the Data | `beautifulsoup`

Since there is no publicly available datasets in the form of CSV or spreadsheets for any Valorant events, I had to collect the data myself. Luckily, websites such as **[vlr.gg](http://vlr.gg)** collects data from these events and displays them on their website. So the first phase of the project was to scrape these data using `beautifulsoup`, a web-scraping library built for Python. 

To begin with, I first retrieved the URL for the event in the VLR website. I set the option to display all 300+ matches in the event leading up to the last one. I collected the URL of each match, and for each match URL, I retrieved the match data. This involves navigating through the HTML tree of the website, and identifying which elements represent the data that I’m looking for. 

Each match consists of at least 2 games to determine the winner, depending on the event. So in order to represent this as a database, I created two CSV files to write on. One file for the **matches** with the match URL as its primary key, and another file for the **games** in each match, with the same key. 

# Preliminary Cleanup | `Google Sheets`

I imported the CSV files in a spreadsheet software (Google Sheets) to cleanup the data, and detect aberrations in the dataset. These include matches where there were not enough players to play the game or games where the data was not available. I simply deleted these entries since there was only a few of them. I exported the final CSV files for use later.

# Engineering Data | `pandas` | `numpy` |

The next part of the project was to identify the following:

- **Match Win-Rate** of each team that participated in the event
- **Round Win-Rate** of each team that participated in the event
- **ACS and KAST** of each team’s agent role

In order to do this, a Jupyter notebook script was created that does the following: 

1. Create a dataframe with `team_id` as the key
2. Join the `matches_NA` and `games_NA` dataframes in an aggreagated dataframe `df_aggregate`
3. Query the match win-rate of each team from `df_aggregate`
4. Query the round win-rate of each team from `df_aggregate`
5. Query the performance of each team from `df_aggregate` based on the following roles:
    - Controller
    - Duelist
    - Sentinel
    - Initiator
6. Output a `pandas` dataframe with the relevant queries

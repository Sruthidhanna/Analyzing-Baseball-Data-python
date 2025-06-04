# 📚Analyzing Baseball Data 

This Python project introduces the basics of data analysis using historical Major League Baseball (MLB) statistics.
You will analyze data from two provided CSV files:
1. Master_2016.csv: Contains player information, including a unique playerID, first name, and last name.
2. Batting_2016.csv: Contains season-by-season batting stats indexed by playerID.

The goal is to write Python code that computes common batting statistics using this data. You'll build on previous experience working with CSV files and dictionaries to extract insights from large datasets. While the data is baseball-specific, the analysis techniques are broadly applicable to data science.

--------

# Project description
The project consists of multiple problems. Each problem will utilize functions you wrote for the previous problems. You can also download all of the files used when testing your code as a zip file.

### Working with the CSV files
As the format of the CSV files that store the baseball data could change (or you could acquire data from somewhere else), the functions that operate directly on the data will all take an "info" dictionary that provides information about the files. That way, you do not need to use constants within your code to access the CSV files and their columns. If the name of a particular column changes, for instance, you can simply update the info structure appropriately and all of your code will continue to work. Furthermore, if you have a CSV file that uses different field separators, you can tailor the info structure appropriately to deal with that without needing to change any of your other code. The info dictionaries contain the following keys, all of which are strings (the use of these keys will become apparent as you work on the project, you may want to refer back to this information as you work on the different parts of the project):

🔹"masterfile": the name of the master CSV file that includes columns with player IDs and names.
🔹"battingfile": the name of the CSV file that includes columns with player IDs and batting data.
🔹"separator": the delimiter character used in the two CSV files.
🔹"quote": the quote character used in the two CSV files.
🔹"playerid": the name of the column header for player IDs in both the master and batting CSV files.
🔹"firstname": the name of the column header for player's first names in the master CSV file.
🔹"lastname": the name of the column header for player's last names in the master CSV file.
🔹"yearid": the name of the column header for the year in the batting CSV file.
🔹"atbats": the name of the column header for at-bats data in the batting CSV file.
🔹"hits": the name of the column header for hits data in the batting CSV file.
🔹"doubles": the name of the column header for doubles data in the batting CSV file.
🔹"triples":  the name of the column header for triples data in the batting CSV file.
🔹"homeruns":  the name of the column header for home runs data in the batting CSV file.
🔹"walks": the name of the column header for walks data in the batting CSV file.
🔹"battingfields": a list of column header names that correspond to batting data in the batting CSV file.

### Part 1 - Compute players with top batting statistics by year
 Your task for this part of the project will be to write four functions that can used in combination to compute the top players based on a provided statistical formula for a given year.  These functions will select a subset of the data and compute the provided statistic on this data.

First, you will write filter_by_year. This function should filter a list of batting statistics dictionaries to return a new list of batting statistics dictionaries that consist only of those statistics in the input which correspond to the given year. Each batting statistics dictionary in the input corresponds to the statistics for a single player for a single year. A batting statistics dictionary is a dictionary whose keys (all strings) include a player id, a year, various batting statistics, and possibly other information. As you only need the name of the "year" column for this function, it is given as an input (yearid). This function should not modify the batting statistics dictionaries in any way, rather it should simply return a list that is similar to the input list of statistics, only it is potentially smaller (assuming that the input contains statistics from multiple years).

Next, you will write top_player_ids. This function should compute the top numplayers players with the given compound statistic computed by formula. The input formula function will return a floating point number corresponding to the compound statistic for the given input batting statistics dictionary. The batting statistics are again given as a list of batting statistics dictionaries of the same format that was used by 
filter_by_year. You will need to pass the baseball info dictionary to the statistics formula so that it can access the appropriate data out of the batting statistics dictionaries. The top_player_ids function should return a list of tuples, where the first element of the tuple is a player ID and the second element is the statistic for that player computed by formula. This list should be sorted in descending order based upon the value of the computed statistic.

Note, that in general, there could be ties whereby two players have exactly the same value for the computed statistic. In general, you would have to decide what to do in that case. For baseball statistics, returning the tied players in any order is probably not a problem. However, if you are computing the top 10 players and the 10th and 11th player are tied, you would arguably want to return a list with both of them in it as tied for 10th place. For the purposes of this project, however, we are going to ignore ties and the machine grader (OwlTest) will not test any situations in which there are ties. In fact, the values of the computed statistic will always be different by at least 0.00001. So, you do not need to write any code to deal with the case where there is a tie. Just keep in mind that if you are doing similar types of analyses in the future, you should think about what you want to do if there are ties.

Next, you will write  lookup_player_names. This function should take a list of tuples in the same form that is returned from top_player_ids. From that information, this function should create a list of strings of the form "x.xxx --- FirstName LastName".  For example, "0.325 --- Scott Rixner".  The floating point statistics must be converted to a consistent format with one digit before and three digits after the decimal point.

Finally, you will write compute_top_stats_year. This function takes a baseball info dictionary, a compound statistics formula, the number of top players to find, numplayers, and a year. It should use that information to return a list of strings of the same form as returned by lookup_player_names that correspond to the numplayers players from the given year with the highest compound statistic computed by formula.

### Part 2 - Compute players with top batting statistics by career
Your task for this part of the project will be to write two more functions that can used along with the other four functions to compute the top players based on a provided statistical formula for their entire career.  These functions will aggregate the yearly data in data that spans and player's career and then compute the provided statistic on this data.  

First, you will write aggregate_by_player_id. The batting statistics are again given as a list of batting statistics dictionaries of the same format that was used by the functions in Part 1. The column name for the player ID field is given as playerid, and the fields input is a list of the names of the columns that should be aggregated. Note that the fields input is necessary because not all of the batting statistics can (or should) be aggregated. For example, it doesn't make sense to sum up the years of the statistics! This function should produce a dictionary of dictionaries. The outer dictionary should map player IDs to batting statistics dictionaries. The batting statistics dictionaries should have keys for playerid and all of the field names in fields, all mapped to the appropriate values. The batting statistics should be the sum of all of the statistics within the statistics input that correspond to each playerid. So, for example, if the input contains data for two years of a particular player, the output should contain one entry for that player with the statistics that are the sum of those two years. 

Finally, you will write compute_top_stats_career. This function is very similar to compute_top_stats_year, but you will first need to aggregate the statistics for each player so that you are operating on career statistics, instead of statistics for a particular year. It should return a list of strings of the same form as returned by lookup_player_names that correspond to the numplayers players with the highest compound statistic computed by formula for their careers.

# Key Features

1. Modular CSV Processing: Uses an info dictionary for flexible file and column configuration.
2. Part 1 – Yearly Stats:
🔸filter_by_year: Filters data by year.
🔸top_player_ids: Ranks players using a custom stat formula.
🔸lookup_player_names: Converts player IDs to formatted name + stat strings.
🔸compute_top_stats_year: Combines the above to show top players for a year.
3. Part 2 – Career Stats:
🔸aggregate_by_player_id: Aggregates stats across all years for each player.
🔸compute_top_stats_career: Finds top players over their full careers.
4. Custom Stat Functions: Pass any formula to compute and rank player performance.
5. Consistent Output Format: "x.xxx --- First Last" for clear, readable results.
6. Data Science Focus: Emphasizes real-world techniques like filtering, aggregating, and ranking tabular data.

----------


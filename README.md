# Election Analysis

## Overview of Election-Audit

### Purpose
Seth and Tom from the Colorado board of elections have requested help writing a python script that can be used to analyze their CSV election data. To help them complete the audit, we need to write a script that could complete the following tasks: 

1.  Calculate the total number of votes cast.
2.  Retrieve a complete list of candidates who received votes.
3.  Determine the percentage of votes each candidate received based on the total number of votes.
4.  Calculate the total number of votes each candidate received.
5.  Determine the winner of the election based on the popular vote.

## Resources
- Data Source: election_results.csv
- Software used: Python 3.9.7 and Visual Studio Code 1.60

## Election-Audit Results
The analysis of the election shows that:

- Total number of Votes: 369,711

- Votes per County:
  - Jefferson received a total of 38,855 votes (10.5%). 
  - Denver received a total of 306,055 votes (82.8%).
  - Arapahoe received a total of 24,801 votes (6.7%). 

- Largest County Turnout:
  - Denver has the largest country turnout with 82.8% of the vote (306,55 votes).
  
- Votes per Candidate: 
  - Charles Casper Stockham received a total of 85,213 votes (23.0%).
  - Diana DeGette received a total of 272,892 votes (73.8%).
  - Raymon Anthony Doane received a total of 11,606 votes (3.1%).

- Winner of the Election: 
  - Diana DeGette won the Colorado election with 272,892 votes (73.8%). 

## Election-Audit Summary

The script that was written during the creation of this audit can be used to analyze other election spreadsheets in the future with a little bit of editing. 

First, we’d need to import and change the file path to whichever election the Colorado commission board wished to analyze. The `file_to_load` variable would need to be changed to connect to the desired election file, and `file_to_save` would need to be changed to the location where they'd want to keep text file that contains all the election data results.

    # Add our dependencies.
    import csv
    import os

    # Add a variable to load a file from a path.
    file_to_load = os.path.join("Resources", "election_results.csv")
    # Add a variable to save the file to a path.
    file_to_save = os.path.join("analysis", "election_analysis.txt")

Then, we'd have to continue changing parts of the code that is looking for specific data in the file. If the header is in a different row, or if it's absent from the file entirely, then we'd have to edit the `header` variable. 

    # Read the header
    header = next(reader)

This also applies to the candidate and county name for each row (if the files are identical in format, we might not have to fix this variable).

        # Get the candidate’s name from each row.
        candidate_name = row[2]

        # 3: Extract the county name from each row.
        county_name = row[1]
        
Code could possibly be removed, edited, or added to discover certain things about the election. For example, the code used for counting the votes per candidate was also used for counting the votes per county. The only elements that changed where the variables associated with the data: `candidate_name` and `county_name` respecitbly. 

        # If the candidate does not match any existing candidate add it to the candidate list
        if candidate_name not in candidate_options:

            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1

        # 4a: Write an if statement that checks that the county does not match any existing county in the county list.
        if county_name not in county_list:

            # 4b: Add the existing county to the list of counties.
            county_list.append(county_name)

            # 4c: Begin tracking the county's vote count.
            county_votes[county_name] = 0

        # 5: Add a vote to that county's vote count.
        county_votes[county_name] += 1
        
If there was an element like this that the board wanted to count (Ex: Counting votes per region), we could simply add, remove, or change the code to show the outcomes the Colorado board of elections want to see. 

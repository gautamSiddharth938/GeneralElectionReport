
# General Election Result Report

### Dashboard Link : https://app.powerbi.com/groups/me/reports/6677a1f2-7705-4f91-83fa-91059b60160c/9576308da85eeae25a55?experience=power-bi&bookmarkGuid=3b0fbc8b531a4306c1d0

## Problem Statement

The General Election Result Report Dashboard provides a detailed and interactive visualization of election outcomes across various constituencies. This dashboard is designed to offer a comprehensive overview of voting patterns, party performance, and voter demographics. Multiple stats like independent candidates, Total votes, NOTA votes, Total prties, Top parties dashboard gives a overall better information about general elections.

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in few of the columns errors & empty values were present.
- Step 5 : Replaced the null values or - value with 0. 
- Step 6 : A new column been inserted to capitalize each word of candidates column and renamed it to Candidates name.         
- Step 7 : Measure table was vreated to store measures and new measure was created to find total count of Candidates.

Following DAX expression was written for the same,
        
        Total Candidates = 
DISTINCTCOUNT(LokSabha_2024_Results[Candidate])
- Step 8 : New measure was created to find  Total count of Parties,
 
 Following DAX expression was written to find Total count of parties,
 
        Total Parties = 
DISTINCTCOUNT(LokSabha_2024_Results[Party])
- Step 9 : New measure was created to calculate All Seats.
 
 Following DAX expression was written to find All Seats,
 
         All Seats = DISTINCTCOUNT(LokSabha_2024_Results[Constituency])
- Step 10 : New measure was created to calculate All Votes.
 
 Following DAX expression was written to find All Votes,
 
         All Votes = 
CALCULATE(
    [Total Votes], 
    ALL(
        LokSabha_2024_Results
    )
) 
- Step 11 : New measure was created to calculate Independent Candidates.
 
 Following DAX expression was written to find Independent Candidates,
 
         Independent Candidates = 
CALCULATE(
    [Total Candidates], 
    LokSabha_2024_Results[Party] = "Independent")  
- Step 12 : New measure was created to calculate Independent Winner Candidates.
 
 Following DAX expression was written to find Independent Winner Candidates,
 
        Independent Winner Candidates = 
CALCULATE(
    [Independent Candidates],
    LokSabha_2024_Results[Result] = "Won")
- Step 13 : New measure was created to calculate NOTA Votes.
 
 Following DAX expression was written to find NOTA Votes,
 
        Nota Votes = 
CALCULATE(
    [Total Votes], 
    LokSabha_2024_Results[Candidate] = "NOTA")
- Step 14 : New measure was created to calculate Total Seats.
 
 Following DAX expression was written to find Total Seats,
 
        Total Seats = 
CALCULATE(
    [Total Candidates], 
    LokSabha_2024_Results[Result] = "Won")  
- Step 15 : New measure was created to calculate Total Votes.
 
 Following DAX expression was written to find Total Votes,
 
        Total Votes = 
SUM(LokSabha_2024_Results[Total Votes])
- Step 16 : New measure was created to calculate Total Winners.
 
 Following DAX expression was written to find Total Winners,
 
        Total Winners = 
CALCULATE(
    [Total Candidates], 
    LokSabha_2024_Results[Result] = "Won"
    ) 
- Step 17 : New measure was created to calculate % of Total Votes.
 
 Following DAX expression was written to find % of Total Votes,
 
        % of Total Votes = 
DIVIDE([Total Votes], [All Votes])     
- Step 18 : New measure was created to calculate Total EVM Votes.
 
 Following DAX expression was written to find Total EVM Votes,
 
        Total EVM Votes = SUM(LokSabha_2024_Results[EVM Votes]) 
- Step 19 : New measure was created to calculate BJP Candidates.
 
 Following DAX expression was written to find BJP Candidates,
 
        BJP Candidates = 
CALCULATE(
    [Total Candidates], 
    LokSabha_2024_Results[Party] = "Bharatiya Janata Party")   
- Step 20 : New measure was created to calculate BJP Total Seats.
 
 Following DAX expression was written to find BJP Total Seats,
 
        BJP Total Seats = 
CALCULATE(
    [BJP Candidates], 
    LokSabha_2024_Results[Result] = "Won")
- Step 21 : New measure was created to calculate INC Candidates.
 
 Following DAX expression was written to find INC Candidates,
 
        INC Candidates = 
CALCULATE(
    [Total Candidates], 
    LokSabha_2024_Results[Party] = "Indian National Congress")      
- Step 22 : New measure was created to calculate INC Total Seats.
 
 Following DAX expression was written to find INC Total Seats,
 
        INC Total Seats = 
CALCULATE(
    [INC Candidates], 
    LokSabha_2024_Results[Result] = "Won")                               
- Step 23 : In the report view, under the view tab, theme was selected.
- Step 24 : Four card visuals were added to the canvas, one representing Total Seats, next one representing Total Parties followed by Total Votes and Nota Votes respectively.
           A matrix were added below cards representing states with Total Candidates and Indepedent Candidates.
           A tree map was added into canvas at the right end representing heirarchy of state followed by Constituency and Total Votes.
- Step 25 : Two Donut charts was also added to the report design area representing Total Votes by Parties(% of total votes) and Total Seats by Parties. While creating this visual Top Filtering been added to show top 3 in both charts. 
- Step 26 : Two Cards were added below tree map and donut charts representing Highest Voted Candidates and Votes. 
 
- Step 27 : The report was then published to Power BI Service.
 
 
![Publish_Message]![Screenshot 2024-07-20 214044](https://github.com/user-attachments/assets/9341b7bb-8753-4e31-ba3b-788f0bdd4eff)

# Snapshot of Dashboard (Power BI Service)

![dashboard_snapo]![Screenshot 2024-07-20 220329](https://github.com/user-attachments/assets/03a6b352-1d78-4458-9e1c-eb66c72a3acb)

 
 # Report Snapshot (Power BI DESKTOP)

 
![Dashboard_upload] ![Opera Snapshot_2024-07-20_220740_app powerbi com](https://github.com/user-attachments/assets/297a8ea0-6018-49dc-b49a-a65cc10475a3)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Number of States And Union Territories = 36

   Number of constituencies = 540

   Number of Parties = 746

   Number of candidates = 8099

   Number of Independent Candidates = 3831


           thus, Number of parties are higher than number of Seats.
           
### [2] Some Stats

    a) Highest Voted Candidates - Rakibul Hussain
    b) Lowest Voted Candidates - MukeshKumar ChandraKant Dalal
    c) NOTA votes - 6,372,220
    d) Total Votes - 645,363,445
    e) EVM Votes - 641,618,937
    f) State with Highest Candidates - Maharastra(1114)
    g) State with Lowest Candidates - Ladakh(4)
    h) State with Highest constituencies - Uttar Pradesh(80 Seats, 166 Parties)
    i) State with Lowest Constituencies - Andaman & Nicobar Islands(1 Seats, 9 Parties)
    j) Party with Highest Seats - Bharatiya Janata Party(240, 37% of Votes)
    k) Party with Lowest Seats - Aazad Samaj Party(Kanshi Ram)(1, 0% of Votes)
    l) Party with Highest Candidates - Bahujan Samaj Party(487)
    m) Party with Lowest Candidates - Adarsh Sangram Party(1) 
  
  while Creating Measures and dashboard few stats which can be important. 
  

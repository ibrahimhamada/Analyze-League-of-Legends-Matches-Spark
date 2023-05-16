# Analyze-League-of-Legends-Matches-Spark
*Mini Project 2 of the Big Data Analytics Course Offered in Fall 2022 @ Zewail City*

[League of Legends](https://leagueoflegends.fandom.com/wiki/League_of_Legends_Wiki) (abbreviated LoL or League) is a multiplayer online battle arena video game
developed and published by Riot Games. Originally inspired by Valve’s Defense of the Ancients
(DotA), the game has followed a freemium model since its release on October 27, 2009. League
of Legends is often cited as the world's largest e-sport, with an international competitive scene.

In this project, we are showing the results of analyzing a dataset of 52941 ranked matches of LoL game.

The obtained results are concerned with the following aspects: Champion win, pick, and ban
rates, Champion Synergies or duos, Item win, pick rates, Item Synergies, and Item suggestion.


## Data Collection:
We started by collecting data from the Riot Games API. We collected a total of “140822” matches, then we filtered out all non-ranked matches to end up with “52941” ranked matches. 
We ran different iterations using different API keys in order to increase the obtained data given that each API key is valid for only 24 hours with RATE LIMITS of 20 requests every 1 seconds and 100 requests every 2 minutes. The data collection pipeline is as follows:

   1) Get summoner’s names : In each iteration, we collected 1000 different summoners from the 'euw1' server and 'europe' region. The summoners’ ranks are distributed based on the rank distribution of the Game. We can see that each tier has a percentage of the game, so we took a sample of players according to the distribution of each rank.
   
   2) Get matches IDs each summoner played: After getting summoners names, we obtained their unique identifier (puuid) by calling the API responsible for getting (puuid) given a summoner name. Then, we extracted different matches that each summoner participated in. We got the matches IDs for each summoner by queuring the matches API.
   
   3) Get matches information from match ids: This step is considered as the bottleneck of the whole process since it took very much time. We extracted the information of each match given the IDs that were extracted in the previous step.
   
   4) Get Champions information: In this step, we retrieved the JSON file that contains all champions information to use it in the requirements such as: champion win rates, champion pick rates, champion ban rates, and champion synergies.
   
   5) Get Items information: In this step, we retrieved the JSON file that contains all items information to use it in the requirements such as: Item win rates, item pick rates, item synergies, and item suggestion.



## Data Analysis:
In this stage, the obtained JSON files from the data collection process are preprocessed before starting analyzing the data.

   1) Obtaining ranked matches only:

Since it is not necessary for all ranked summoners to play only ranked matches, we filtered out all non-ranked matches. We explored the documentation and found that “queueId” is responsible for determining the match type. Additionally, we found that matches with “queueId = 420” are the ranked matches, so we filtered them out of the total matches.

![image](https://github.com/ibrahimhamada/Analyze-League-of-Legends-Matches-Spark/assets/58476343/10e6c77a-12a0-4e14-bbf9-935a89eb9ecc)

   2) Calculating some values:

We found the total number of matches using the count() function. We found teams count based on the fact that each match is played with 2 teams. We found the participants count given the fact that each team consists of 10 members.

After that, we started dealing with ranked_matches rdd to find the requirements as follows:

## Requirements:

### I) Requirement 1: (Champion pick rate, Champion win rate, and Champion ban rate)

![image](https://github.com/ibrahimhamada/Analyze-League-of-Legends-Matches-Spark/assets/58476343/1ed7d025-112a-4f43-bb73-98801d05fcee)

![image](https://github.com/ibrahimhamada/Analyze-League-of-Legends-Matches-Spark/assets/58476343/45ab3338-45f3-43dc-92ab-46afe1b097d6)

![image](https://github.com/ibrahimhamada/Analyze-League-of-Legends-Matches-Spark/assets/58476343/c0595401-0c2b-4c76-b991-20b0ded12c6e)


### II) Requirement 2: (Champion Synergies or duos)
 
![image](https://github.com/ibrahimhamada/Analyze-League-of-Legends-Matches-Spark/assets/58476343/8067488b-da49-427d-ad68-88ada07495f2)

   
### III) Requirement 3: (Item win rates, item pick rates)
   
![image](https://github.com/ibrahimhamada/Analyze-League-of-Legends-Matches-Spark/assets/58476343/829bb6a6-c5ac-42dd-913c-3edd54172eab)

![image](https://github.com/ibrahimhamada/Analyze-League-of-Legends-Matches-Spark/assets/58476343/40e95d2b-437e-4ec7-a504-7d3252928ef9)

### IV) Requirement 4: (Item Synergies (item with champion, item with class))
 
![image](https://github.com/ibrahimhamada/Analyze-League-of-Legends-Matches-Spark/assets/58476343/a86aae79-2617-4040-8547-ed51d8b71b8e)

![image](https://github.com/ibrahimhamada/Analyze-League-of-Legends-Matches-Spark/assets/58476343/981ad353-63f1-4b24-9a41-3abffa41ced2)

### V) Requirement 5: (Item suggestion)
 
    Item Suggestion for Champion “Ekko” with win rate 100% :
    a) Doran's Shield
    b) Gargoyle Stoneplate
    c) Seraph's Embrace
    d) Navori Quickblades
    e) Abyssal Mask

    Item Suggestion for Champion “Ezreal” with win rate 100% :
    a) Gustwalker Hatchling
    b) Gargoyle Stoneplate
    c) Mosstomper Seedling
    d) Spectral Sickle
    e) Leeching Leer
   
   
### VI) Extra Requirement: (Best lane for champion / win rates of different lanes for champions)

![image](https://github.com/ibrahimhamada/Analyze-League-of-Legends-Matches-Spark/assets/58476343/e29dc56a-0bbb-43dc-aa99-20412670051c)

![image](https://github.com/ibrahimhamada/Analyze-League-of-Legends-Matches-Spark/assets/58476343/4135312b-923a-4c26-a70a-2ef8abbfe57f)




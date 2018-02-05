# Baseball-Project
Source: Wikipedia
The 2002 Oakland A's
The Oakland Athletics' 2002 season was the team's 35th in Oakland, California. It was also the 102nd season in franchise history. The Athletics finished first in the American League West with a record of 103-59.
The Athletics' 2002 campaign ranks among the most famous in franchise history. Following the 2001 season, Oakland saw the departure of three key players (the lost boys). Billy Beane, the team's general manager, responded with a series of under-the-radar free agent signings. The new-look Athletics, despite a comparative lack of star power, surprised the baseball world by besting the 2001 team's regular season record. The team is most famous, however, for winning 20 consecutive games between August 13 and September 4, 2002.[1] The Athletics' season was the subject of Michael Lewis' 2003 book Moneyball: The Art of Winning an Unfair Game (as Lewis was given the opportunity to follow the team around throughout that season)
###This project is based off the book written by Michael Lewis (later turned into a movie).
![moneyball](https://cloud.githubusercontent.com/assets/16123495/22365119/a875df88-e42a-11e6-82d2-0f8cdb75c6f5.jpg)
###Moneyball Book
The central premise of book Moneyball is that the collective wisdom of baseball insiders (including players, managers, coaches, scouts, and the front office) over the past century is subjective and often flawed. Statistics such as stolen bases, runs batted in, and batting average, typically used to gauge players, are relics of a 19th-century view of the game and the statistics available at that time. The book argues that the Oakland A's' front office took advantage of more analytical gauges of player performance to field a team that could better compete against richer competitors in Major League Baseball (MLB).
Rigorous statistical analysis had demonstrated that on-base percentage and slugging percentage are better indicators of offensive success, and the A's became convinced that these qualities were cheaper to obtain on the open market than more historically valued qualities such as speed and contact. These observations often flew in the face of conventional baseball wisdom and the beliefs of many baseball scouts and executives.

By re-evaluating the strategies that produce wins on the field, the 2002 Athletics, with approximately US 44 million dollars in salary, were competitive with larger market teams such as the New York Yankees, who spent over US$125 million in payroll that same season.
![salary](https://cloud.githubusercontent.com/assets/16123495/22365258/5a1cacb2-e42b-11e6-9e9f-b3a87104855d.png)
Because of the team's smaller revenues, Oakland is forced to find players undervalued by the market, and their system for finding value in undervalued players has proven itself thus far. This approach brought the A's to the playoffs in 2002 and 2003.
In this project we'll work with some data and with the goal of trying to find replacement players for the ones lost at the start of the off-season - During the 2001–02 offseason, the team lost three key free agents to larger market teams: 2000 AL MVP Jason Giambi to the New York Yankees, outfielder Johnny Damon to the Boston Red Sox, and closer Jason Isringhausen to the St. Louis Cardinals.
The main goal of this project is for you to feel comfortable working with R on real data to try and derive actionable insights!

I am using Sean Lahaman's Website a very useful source for baseball statistics. The documentation for the csv files is located in the readme2013.txt file. You may need to reference this to understand what acronyms stand for.

Moneyball_project.R
irinamahmudjanova

Wed Jan 18 15:51:32 2017

    library(dplyr)
    ## 
    ## Attaching package: 'dplyr'
    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag
    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union
    batting <- read.csv('Batting.csv')
    head(batting)
    ##    playerID yearID stint teamID lgID  G G_batting AB R H X2B X3B HR RBI SB
    ## 1 aardsda01   2004     1    SFN   NL 11        11  0 0 0   0   0  0   0  0
    ## 2 aardsda01   2006     1    CHN   NL 45        43  2 0 0   0   0  0   0  0
    ## 3 aardsda01   2007     1    CHA   AL 25         2  0 0 0   0   0  0   0  0
    ## 4 aardsda01   2008     1    BOS   AL 47         5  1 0 0   0   0  0   0  0
    ## 5 aardsda01   2009     1    SEA   AL 73         3  0 0 0   0   0  0   0  0
    ## 6 aardsda01   2010     1    SEA   AL 53         4  0 0 0   0   0  0   0  0
    ##   CS BB SO IBB HBP SH SF GIDP G_old
    ## 1  0  0  0   0   0  0  0    0    11
    ## 2  0  0  0   0   0  1  0    0    45
    ## 3  0  0  0   0   0  0  0    0     2
    ## 4  0  0  1   0   0  0  0    0     5
    ## 5  0  0  0   0   0  0  0    0    NA
    ## 6  0  0  0   0   0  0  0    0    NA
####Use str() to check the structure. Pay close attention to how columns that start with a number get an 'X' in front of them! You'll need to know this to call those columns!
    
    str(batting)
    ##  $ playerID : Factor w/ 18107 levels "aardsda01","aaronha01",..: 1 1 1 1 1 1 1 2 2 2 ...
    ##  $ yearID   : int  2004 2006 2007 2008 2009 2010 2012 1954 1955 1956 ...
    ##  $ stint    : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ teamID   : Factor w/ 149 levels "ALT","ANA","ARI",..: 117 35 33 16 116 116 93 80 80 80 ...
    ##  $ lgID     : Factor w/ 6 levels "AA","AL","FL",..: 4 4 2 2 2 2 2 4 4 4 ...
    ##  $ G        : int  11 45 25 47 73 53 1 122 153 153 ...
    ##  $ G_batting: int  11 43 2 5 3 4 NA 122 153 153 ...
    ##  $ AB       : int  0 2 0 1 0 0 NA 468 602 609 ...
    ##  $ R        : int  0 0 0 0 0 0 NA 58 105 106 ...
    ##  $ H        : int  0 0 0 0 0 0 NA 131 189 200 ...
    ##  $ X2B      : int  0 0 0 0 0 0 NA 27 37 34 ...
    ##  $ X3B      : int  0 0 0 0 0 0 NA 6 9 14 ...
    ##  $ HR       : int  0 0 0 0 0 0 NA 13 27 26 ...
    ##  $ RBI      : int  0 0 0 0 0 0 NA 69 106 92 ...
    ##  $ SB       : int  0 0 0 0 0 0 NA 2 3 2 ...
    ##  $ CS       : int  0 0 0 0 0 0 NA 2 1 4 ...
    ##  $ BB       : int  0 0 0 0 0 0 NA 28 49 37 ...
    ##  $ SO       : int  0 0 0 1 0 0 NA 39 61 54 ...
    ##  $ IBB      : int  0 0 0 0 0 0 NA NA 5 6 ...
    ##  $ HBP      : int  0 0 0 0 0 0 NA 3 3 2 ...
    ##  $ SH       : int  0 1 0 0 0 0 NA 6 7 5 ...
    ##  $ SF       : int  0 0 0 0 0 0 NA 4 4 7 ...
    ##  $ GIDP     : int  0 0 0 0 0 0 NA 13 20 21 ...
    ##  $ G_old    : int  11 45 2 5 NA NA NA 122 153 153 ...
    ## Make sure you understand how to call the columns by using the $ symbol.
    ## Call the head() of the first five rows of AB (At Bats) column
    head(batting$AB, 5)
    ## [1] 0 2 0 1 0
##Call the head of the doubles (X2B) column
    
    head(batting$X2B)
    ## [1] 0 0 0 0 0 0
    batting$BA <- batting$H / batting$AB
    tail(batting$BA,5)
    ## [1] 0.1230769 0.2746479 0.1470588 0.2745098 0.2138728
####Now do the same for some new columns! On Base Percentage (OBP) and Slugging Percentage (SLG). Hint: For SLG, you need 1B (Singles), this isn't in your data frame. However you can calculate it by subtracting doubles,triples, and home runs from total hits (H): 1B = H-2B-3B-HR
####Create an OBP Column
####Create an SLG Column

    # On Base Percentage
    batting$OBP <- (batting$H + batting$BB + batting$HBP)/(batting$AB + batting$BB + batting$HBP + batting$SF)

    # Creating X1B (Singles)
    batting$X1B <- batting$H - batting$X2B - batting$X3B - batting$HR

    # Creating Slugging Average (SLG)
    batting$SLG <- ((1 * batting$X1B) + (2 * batting$X2B) + (3 * batting$X3B) + (4 * batting$HR) ) / batting$AB

####Check the structure of your data frame using str()

    str(batting)
    ## 'data.frame':    97889 obs. of  28 variables:
    ##  $ playerID : Factor w/ 18107 levels "aardsda01","aaronha01",..: 1 1 1 1 1 1 1 2 2 2 ...
    ##  $ yearID   : int  2004 2006 2007 2008 2009 2010 2012 1954 1955 1956 ...
    ##  $ stint    : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ teamID   : Factor w/ 149 levels "ALT","ANA","ARI",..: 117 35 33 16 116 116 93 80 80 80 ...
    ##  $ lgID     : Factor w/ 6 levels "AA","AL","FL",..: 4 4 2 2 2 2 2 4 4 4 ...
    ##  $ G        : int  11 45 25 47 73 53 1 122 153 153 ...
    ##  $ G_batting: int  11 43 2 5 3 4 NA 122 153 153 ...
    ##  $ AB       : int  0 2 0 1 0 0 NA 468 602 609 ...
    ##  $ R        : int  0 0 0 0 0 0 NA 58 105 106 ...
    ##  $ H        : int  0 0 0 0 0 0 NA 131 189 200 ...
    ##  $ X2B      : int  0 0 0 0 0 0 NA 27 37 34 ...
    ##  $ X3B      : int  0 0 0 0 0 0 NA 6 9 14 ...
    ##  $ HR       : int  0 0 0 0 0 0 NA 13 27 26 ...
    ##  $ RBI      : int  0 0 0 0 0 0 NA 69 106 92 ...
    ##  $ SB       : int  0 0 0 0 0 0 NA 2 3 2 ...
    ##  $ CS       : int  0 0 0 0 0 0 NA 2 1 4 ...
    ##  $ BB       : int  0 0 0 0 0 0 NA 28 49 37 ...
    ##  $ SO       : int  0 0 0 1 0 0 NA 39 61 54 ...
    ##  $ IBB      : int  0 0 0 0 0 0 NA NA 5 6 ...
    ##  $ HBP      : int  0 0 0 0 0 0 NA 3 3 2 ...
    ##  $ SH       : int  0 1 0 0 0 0 NA 6 7 5 ...
    ##  $ SF       : int  0 0 0 0 0 0 NA 4 4 7 ...
    ##  $ GIDP     : int  0 0 0 0 0 0 NA 13 20 21 ...
    ##  $ G_old    : int  11 45 2 5 NA NA NA 122 153 153 ...
    ##  $ BA       : num  NaN 0 NaN 0 NaN ...
    ##  $ OBP      : num  NaN 0 NaN 0 NaN ...
    ##  $ X1B      : int  0 0 0 0 0 0 NA 85 116 126 ...
    ##  $ SLG      : num  NaN 0 NaN 0 NaN ...
####  Load the Salaries.csv file into a dataframe called sal using read.csv

    sal <- read.csv('Salaries.csv')

####Use summary to get a summary of the batting data frame and notice the minimum year in the yearID column. Our batting data goes back to 1871! Our salary data starts at 1985, meaning we need to remove the batting data that occured before 1985.
Use subset() to reassign batting to only contain data from 1985 and onwards
 
     summary(batting)
    ##       playerID         yearID         stint           teamID     
    ##  mcguide01:   31   Min.   :1871   Min.   :1.000   CHN    : 4720  
    ##  henderi01:   29   1st Qu.:1931   1st Qu.:1.000   PHI    : 4621  
    ##  newsobo01:   29   Median :1970   Median :1.000   PIT    : 4575  
    ##  johnto01 :   28   Mean   :1962   Mean   :1.077   SLN    : 4535  
    ##  kaatji01 :   28   3rd Qu.:1995   3rd Qu.:1.000   CIN    : 4393  
    ##  ansonca01:   27   Max.   :2013   Max.   :5.000   CLE    : 4318  
    ##  (Other)  :97717                                  (Other):70727  
    ##    lgID             G            G_batting            AB       
    ##  AA  : 1890   Min.   :  1.00   Min.   :  0.00   Min.   :  0.0  
    ##  AL  :44369   1st Qu.: 13.00   1st Qu.:  7.00   1st Qu.:  9.0  
    ##  FL  :  470   Median : 35.00   Median : 32.00   Median : 61.0  
    ##  NL  :49944   Mean   : 51.65   Mean   : 49.13   Mean   :154.1  
    ##  PL  :  147   3rd Qu.: 81.00   3rd Qu.: 81.00   3rd Qu.:260.0  
    ##  UA  :  332   Max.   :165.00   Max.   :165.00   Max.   :716.0  
    ##  NA's:  737                    NA's   :1406     NA's   :6413   
    ##        R                H               X2B            X3B        
    ##  Min.   :  0.00   Min.   :  0.00   Min.   : 0.0   Min.   : 0.000  
    ##  1st Qu.:  0.00   1st Qu.:  1.00   1st Qu.: 0.0   1st Qu.: 0.000  
    ##  Median :  5.00   Median : 12.00   Median : 2.0   Median : 0.000  
    ##  Mean   : 20.47   Mean   : 40.37   Mean   : 6.8   Mean   : 1.424  
    ##  3rd Qu.: 31.00   3rd Qu.: 66.00   3rd Qu.:10.0   3rd Qu.: 2.000  
    ##  Max.   :192.00   Max.   :262.00   Max.   :67.0   Max.   :36.000  
    ##  NA's   :6413     NA's   :6413     NA's   :6413   NA's   :6413    
    ##        HR              RBI               SB                CS        
    ##  Min.   : 0.000   Min.   :  0.00   Min.   :  0.000   Min.   : 0.000  
    ##  1st Qu.: 0.000   1st Qu.:  0.00   1st Qu.:  0.000   1st Qu.: 0.000  
    ##  Median : 0.000   Median :  5.00   Median :  0.000   Median : 0.000  
    ##  Mean   : 3.002   Mean   : 18.47   Mean   :  3.265   Mean   : 1.385  
    ##  3rd Qu.: 3.000   3rd Qu.: 28.00   3rd Qu.:  2.000   3rd Qu.: 1.000  
    ##  Max.   :73.000   Max.   :191.00   Max.   :138.000   Max.   :42.000  
    ##  NA's   :6413     NA's   :6837     NA's   :7713      NA's   :29867   
    ##        BB               SO              IBB              HBP        
    ##  Min.   :  0.00   Min.   :  0.00   Min.   :  0.00   Min.   : 0.000  
    ##  1st Qu.:  0.00   1st Qu.:  2.00   1st Qu.:  0.00   1st Qu.: 0.000  
    ##  Median :  4.00   Median : 11.00   Median :  0.00   Median : 0.000  
    ##  Mean   : 14.21   Mean   : 21.95   Mean   :  1.28   Mean   : 1.136  
    ##  3rd Qu.: 21.00   3rd Qu.: 31.00   3rd Qu.:  1.00   3rd Qu.: 1.000  
    ##  Max.   :232.00   Max.   :223.00   Max.   :120.00   Max.   :51.000  
    ##  NA's   :6413     NA's   :14251    NA's   :42977    NA's   :9233    
    ##        SH               SF             GIDP           G_old       
    ##  Min.   : 0.000   Min.   : 0.0    Min.   : 0.00   Min.   :  0.00  
    ##  1st Qu.: 0.000   1st Qu.: 0.0    1st Qu.: 0.00   1st Qu.: 11.00  
    ##  Median : 1.000   Median : 0.0    Median : 1.00   Median : 34.00  
    ##  Mean   : 2.564   Mean   : 1.2    Mean   : 3.33   Mean   : 50.99  
    ##  3rd Qu.: 3.000   3rd Qu.: 2.0    3rd Qu.: 5.00   3rd Qu.: 82.00  
    ##  Max.   :67.000   Max.   :19.0    Max.   :36.00   Max.   :165.00  
    ##  NA's   :12751    NA's   :42446   NA's   :32521   NA's   :5189    
    ##        BA             OBP             X1B              SLG       
    ##  Min.   :0.000   Min.   :0.00    Min.   :  0.00   Min.   :0.000  
    ##  1st Qu.:0.148   1st Qu.:0.19    1st Qu.:  1.00   1st Qu.:0.179  
    ##  Median :0.231   Median :0.29    Median :  9.00   Median :0.309  
    ##  Mean   :0.209   Mean   :0.26    Mean   : 29.14   Mean   :0.291  
    ##  3rd Qu.:0.275   3rd Qu.:0.34    3rd Qu.: 48.00   3rd Qu.:0.397  
    ##  Max.   :1.000   Max.   :1.00    Max.   :225.00   Max.   :4.000  
    ##  NA's   :13520   NA's   :49115   NA's   :6413     NA's   :13520
      batting <- subset(batting,yearID >= 1985)
  
#### Now use summary again to make sure the subset reassignment worked, your yearID min should be 1985
    summary(batting)
    ##       playerID         yearID         stint          teamID     
    ##  moyerja01:   27   Min.   :1985   Min.   :1.00   SDN    : 1313  
    ##  mulhote01:   26   1st Qu.:1993   1st Qu.:1.00   CLE    : 1306  
    ##  weathda01:   26   Median :2000   Median :1.00   PIT    : 1299  
    ##  maddugr01:   25   Mean   :2000   Mean   :1.08   NYN    : 1297  
    ##  sierrru01:   25   3rd Qu.:2007   3rd Qu.:1.00   BOS    : 1279  
    ##  thomeji01:   25   Max.   :2013   Max.   :4.00   CIN    : 1279  
    ##  (Other)  :35498                                 (Other):27879  
    ##  lgID             G           G_batting            AB       
    ##  AA:    0   Min.   :  1.0   Min.   :  0.00   Min.   :  0.0  
    ##  AL:17226   1st Qu.: 14.0   1st Qu.:  4.00   1st Qu.:  3.0  
    ##  FL:    0   Median : 34.0   Median : 27.00   Median : 47.0  
    ##  NL:18426   Mean   : 51.7   Mean   : 46.28   Mean   :144.7  
    ##  PL:    0   3rd Qu.: 77.0   3rd Qu.: 77.00   3rd Qu.:241.0  
    ##  UA:    0   Max.   :163.0   Max.   :163.00   Max.   :716.0  
    ##                             NA's   :1406     NA's   :4377   
    ##        R                H               X2B              X3B        
    ##  Min.   :  0.00   Min.   :  0.00   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.:  0.00   1st Qu.:  0.00   1st Qu.: 0.000   1st Qu.: 0.000  
    ##  Median :  4.00   Median :  8.00   Median : 1.000   Median : 0.000  
    ##  Mean   : 19.44   Mean   : 37.95   Mean   : 7.293   Mean   : 0.824  
    ##  3rd Qu.: 30.00   3rd Qu.: 61.00   3rd Qu.:11.000   3rd Qu.: 1.000  
    ##  Max.   :152.00   Max.   :262.00   Max.   :59.000   Max.   :23.000  
    ##  NA's   :4377     NA's   :4377     NA's   :4377     NA's   :4377    
    ##        HR              RBI               SB                CS        
    ##  Min.   : 0.000   Min.   :  0.00   Min.   :  0.000   Min.   : 0.000  
    ##  1st Qu.: 0.000   1st Qu.:  0.00   1st Qu.:  0.000   1st Qu.: 0.000  
    ##  Median : 0.000   Median :  3.00   Median :  0.000   Median : 0.000  
    ##  Mean   : 4.169   Mean   : 18.41   Mean   :  2.811   Mean   : 1.219  
    ##  3rd Qu.: 5.000   3rd Qu.: 27.00   3rd Qu.:  2.000   3rd Qu.: 1.000  
    ##  Max.   :73.000   Max.   :165.00   Max.   :110.000   Max.   :29.000  
    ##  NA's   :4377     NA's   :4377     NA's   :4377      NA's   :4377    
    ##        BB               SO              IBB               HBP        
    ##  Min.   :  0.00   Min.   :  0.00   Min.   :  0.000   Min.   : 0.000  
    ##  1st Qu.:  0.00   1st Qu.:  1.00   1st Qu.:  0.000   1st Qu.: 0.000  
    ##  Median :  3.00   Median : 12.00   Median :  0.000   Median : 0.000  
    ##  Mean   : 14.06   Mean   : 27.03   Mean   :  1.171   Mean   : 1.273  
    ##  3rd Qu.: 21.00   3rd Qu.: 42.00   3rd Qu.:  1.000   3rd Qu.: 1.000  
    ##  Max.   :232.00   Max.   :223.00   Max.   :120.000   Max.   :35.000  
    ##  NA's   :4377     NA's   :4377     NA's   :4378      NA's   :4387    
    ##        SH               SF              GIDP           G_old      
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.00   Min.   :  0.0  
    ##  1st Qu.: 0.000   1st Qu.: 0.000   1st Qu.: 0.00   1st Qu.: 11.0  
    ##  Median : 0.000   Median : 0.000   Median : 1.00   Median : 32.0  
    ##  Mean   : 1.465   Mean   : 1.212   Mean   : 3.25   Mean   : 49.7  
    ##  3rd Qu.: 2.000   3rd Qu.: 2.000   3rd Qu.: 5.00   3rd Qu.: 77.0  
    ##  Max.   :39.000   Max.   :17.000   Max.   :35.00   Max.   :163.0  
    ##  NA's   :4377     NA's   :4378     NA's   :4377    NA's   :5189   
    ##        BA             OBP             X1B              SLG       
    ##  Min.   :0.000   Min.   :0.000   Min.   :  0.00   Min.   :0.000  
    ##  1st Qu.:0.136   1st Qu.:0.188   1st Qu.:  0.00   1st Qu.:0.167  
    ##  Median :0.233   Median :0.296   Median :  6.00   Median :0.333  
    ##  Mean   :0.205   Mean   :0.262   Mean   : 25.66   Mean   :0.304  
    ##  3rd Qu.:0.274   3rd Qu.:0.342   3rd Qu.: 42.00   3rd Qu.:0.423  
    ##  Max.   :1.000   Max.   :1.000   Max.   :225.00   Max.   :4.000  
    ##  NA's   :8905    NA's   :8821    NA's   :4377     NA's   :8905
    
#### Using the merge() function to merge the batting and sal data frames by c('playerID','yearID'). Call the new data frame combo
    combo <- merge(batting,sal,by=c('playerID','yearID'))
    
#### Using summary to check the data
    summary(combo)
    ##       playerID         yearID         stint          teamID.x    
    ##  moyerja01:   27   Min.   :1985   Min.   :1.000   LAN    :  940  
    ##  thomeji01:   25   1st Qu.:1993   1st Qu.:1.000   PHI    :  937  
    ##  weathda01:   25   Median :1999   Median :1.000   BOS    :  935  
    ##  vizquom01:   24   Mean   :1999   Mean   :1.098   NYA    :  928  
    ##  gaettga01:   23   3rd Qu.:2006   3rd Qu.:1.000   CLE    :  920  
    ##  griffke02:   23   Max.   :2013   Max.   :4.000   SDN    :  914  
    ##  (Other)  :25250                                  (Other):19823  
    ##  lgID.x           G            G_batting            AB       
    ##  AA:    0   Min.   :  1.00   Min.   :  0.00   Min.   :  0.0  
    ##  AL:12292   1st Qu.: 26.00   1st Qu.:  8.00   1st Qu.:  5.0  
    ##  FL:    0   Median : 50.00   Median : 42.00   Median : 85.0  
    ##  NL:13105   Mean   : 64.06   Mean   : 57.58   Mean   :182.4  
    ##  PL:    0   3rd Qu.:101.00   3rd Qu.:101.00   3rd Qu.:336.0  
    ##  UA:    0   Max.   :163.00   Max.   :163.00   Max.   :716.0  
    ##                              NA's   :906      NA's   :2661   
    ##        R                H               X2B              X3B        
    ##  Min.   :  0.00   Min.   :  0.00   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.:  0.00   1st Qu.:  1.00   1st Qu.: 0.000   1st Qu.: 0.000  
    ##  Median :  9.00   Median : 19.00   Median : 3.000   Median : 0.000  
    ##  Mean   : 24.71   Mean   : 48.18   Mean   : 9.276   Mean   : 1.033  
    ##  3rd Qu.: 43.00   3rd Qu.: 87.25   3rd Qu.:16.000   3rd Qu.: 1.000  
    ##  Max.   :152.00   Max.   :262.00   Max.   :59.000   Max.   :23.000  
    ##  NA's   :2661     NA's   :2661     NA's   :2661     NA's   :2661    
    ##        HR              RBI               SB                CS       
    ##  Min.   : 0.000   Min.   :  0.00   Min.   :  0.000   Min.   : 0.00  
    ##  1st Qu.: 0.000   1st Qu.:  0.00   1st Qu.:  0.000   1st Qu.: 0.00  
    ##  Median : 1.000   Median :  8.00   Median :  0.000   Median : 0.00  
    ##  Mean   : 5.369   Mean   : 23.56   Mean   :  3.568   Mean   : 1.54  
    ##  3rd Qu.: 7.000   3rd Qu.: 39.00   3rd Qu.:  3.000   3rd Qu.: 2.00  
    ##  Max.   :73.000   Max.   :165.00   Max.   :110.000   Max.   :29.00  
    ##  NA's   :2661     NA's   :2661     NA's   :2661      NA's   :2661   
    ##        BB               SO              IBB               HBP        
    ##  Min.   :  0.00   Min.   :  0.00   Min.   :  0.000   Min.   : 0.000  
    ##  1st Qu.:  0.00   1st Qu.:  2.00   1st Qu.:  0.000   1st Qu.: 0.000  
    ##  Median :  6.00   Median : 20.00   Median :  0.000   Median : 0.000  
    ##  Mean   : 17.98   Mean   : 33.52   Mean   :  1.533   Mean   : 1.614  
    ##  3rd Qu.: 29.00   3rd Qu.: 55.00   3rd Qu.:  2.000   3rd Qu.: 2.000  
    ##  Max.   :232.00   Max.   :223.00   Max.   :120.000   Max.   :35.000  
    ##  NA's   :2661     NA's   :2661     NA's   :2662      NA's   :2670    
    ##        SH               SF              GIDP            G_old       
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   :  0.00  
    ##  1st Qu.: 0.000   1st Qu.: 0.000   1st Qu.: 0.000   1st Qu.: 20.00  
    ##  Median : 0.000   Median : 0.000   Median : 2.000   Median : 47.00  
    ##  Mean   : 1.786   Mean   : 1.554   Mean   : 4.127   Mean   : 61.43  
    ##  3rd Qu.: 2.000   3rd Qu.: 2.000   3rd Qu.: 7.000   3rd Qu.:101.00  
    ##  Max.   :39.000   Max.   :17.000   Max.   :35.000   Max.   :163.00  
    ##  NA's   :2661     NA's   :2662     NA's   :2661     NA's   :3414    
    ##        BA             OBP             X1B             SLG       
    ##  Min.   :0.000   Min.   :0.000   Min.   :  0.0   Min.   :0.000  
    ##  1st Qu.:0.160   1st Qu.:0.208   1st Qu.:  0.0   1st Qu.:0.200  
    ##  Median :0.242   Median :0.305   Median : 13.0   Median :0.351  
    ##  Mean   :0.212   Mean   :0.270   Mean   : 32.5   Mean   :0.317  
    ##  3rd Qu.:0.276   3rd Qu.:0.346   3rd Qu.: 59.0   3rd Qu.:0.432  
    ##  Max.   :1.000   Max.   :1.000   Max.   :225.0   Max.   :4.000  
    ##  NA's   :5618    NA's   :5562    NA's   :2661    NA's   :5618   
    ##     teamID.y     lgID.y         salary        
    ##  CLE    :  935   AL:12304   Min.   :       0  
    ##  PIT    :  932   NL:13093   1st Qu.:  255000  
    ##  PHI    :  931              Median :  550000  
    ##  SDN    :  923              Mean   : 1879256  
    ##  LAN    :  921              3rd Qu.: 2150000  
    ##  CIN    :  912              Max.   :33000000  
    ##  (Other):19843
    
#### I will use subset() function to get a data frame called lost_players from the combo data frame consisting of those 3 players. And try to figure out how to use %in% to avoid a bunch of or statements!
    lost_players <- subset(combo,playerID %in% c('giambja01','damonjo01','saenzol01') )
    lost_players  
    
    ##        playerID yearID stint teamID.x lgID.x   G G_batting  AB   R   H X2B
    ## 5135  damonjo01   1995     1      KCA     AL  47        47 188  32  53  11
    ## 5136  damonjo01   1996     1      KCA     AL 145       145 517  61 140  22
    ## 5137  damonjo01   1997     1      KCA     AL 146       146 472  70 130  12
    ## 5138  damonjo01   1998     1      KCA     AL 161       161 642 104 178  30
    ## 5139  damonjo01   1999     1      KCA     AL 145       145 583 101 179  39

    ## ....
    ##       X3B HR RBI SB CS  BB  SO IBB HBP SH SF GIDP G_old        BA
    ## 5135    5  3  23  7  0  12  22   0   1  2  3    2    47 0.2819149
    ## 5136    5  6  50 25  5  31  64   3   3 10  5    4   145 0.2707930
    ## 5137    8  8  48 16 10  42  70   2   3  6  1    3   146 0.2754237
    ## 5138   10 18  66 26 12  58  84   4   4  3  3    4   161 0.2772586
    ## 5139    9 14  77 36  6  67  50   5   3  3  4   13   145 0.3070326

    ## ....
    ##             OBP X1B       SLG teamID.y lgID.y   salary
    ## 5135  0.3235294  34 0.4414894      KCA     AL   109000
    ## 5136  0.3129496 107 0.3675048      KCA     AL   180000
    ## 5137  0.3378378 102 0.3855932      KCA     AL   240000
    ## 5138  0.3394625 120 0.4392523      KCA     AL   460000
    ## 5139  0.3789954 117 0.4768439      KCA     AL  2100000
    ## 5
#### Since all these players were lost in after 2001 in the offseason, let's only concern ourselves with the data from 2001.
#### Use subset again to only grab the rows where the yearID was 2001.
    lost_players <- subset(lost_players,yearID == 2001)

#### Reduce the lost_players data frame to the following columns: playerID,H,X2B,X3B,HR,OBP,SLG,BA,AB
    lost_players <- lost_players[,c('playerID','H','X2B','X3B','HR','OBP','SLG','BA','AB')]
     head(lost_players)
    ##        playerID   H X2B X3B HR       OBP       SLG        BA  AB
    ## 5141  damonjo01 165  34   4  9 0.3235294 0.3633540 0.2562112 644
    ## 7878  giambja01 178  47   2 38 0.4769001 0.6596154 0.3423077 520
    ## 20114 saenzol01  67  21   1  9 0.2911765 0.3836066 0.2196721 305
    ## Note: There are lots of correct answers and ways to solve this!
    ## First only grab available players from year 2001
    library(dplyr)
    avail.players <- filter(combo,yearID==2001)
#### Then I made a quick plot to see where I should cut-off for salary in respect to OBP:
library(ggplot2)
ggplot(avail.players,aes(x=OBP,y=salary)) + geom_point()
## Warning: Removed 168 rows containing missing values (geom_point).


## Looks like there is no point in paying above 8 million or so (I'm just eyeballing this number). I'll choose that as a cutt off point. There are also a lot of players with OBP==0. Let's get rid of them too.
avail.players <- filter(avail.players,salary<8000000,OBP>0)
## The total AB of the lost players is 1469. This is about 1500, meaning I should probably cut off my avail.players at 1500/3= 500 AB.

avail.players <- filter(avail.players,AB >= 500)
## Now let's sort by OBP and see what we've got!

possible <- head(arrange(avail.players,desc(OBP)),10)
## Grab columns I'm interested in:
possible <- possible[,c('playerID','OBP','AB','salary')]
possible
     ##     playerID       OBP  AB  salary
     ## 1  giambja01 0.4769001 520 4103333
     ## 2  heltoto01 0.4316547 587 4950000
     ## 3  berkmla01 0.4302326 577  305000
     ## 4  gonzalu01 0.4285714 609 4833333
     ## 5  thomeji01 0.4161491 526 7875000
     ## 6  alomaro01 0.4146707 575 7750000
     ## 7  edmonji01 0.4102142 500 6333333
     ## 8  gilesbr02 0.4035608 576 7333333
     ## 9  pujolal01 0.4029630 590  200000
     ## 10 olerujo01 0.4011799 572 6700000
## Can't choose giambja again, but the other ones look good (2-4). I choose them!
    possible[2:4,]
    ##    playerID       OBP  AB  salary
    ## 2 heltoto01 0.4316547 587 4950000
    ## 3 berkmla01 0.4302326 577  305000
    ## 4 gonzalu01 0.4285714 609 4833333

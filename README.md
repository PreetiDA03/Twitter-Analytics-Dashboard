# Twitter-Analytics-Dashboard
📌 Real-Time Twitter Analytics Dashboard
1. Introduction

This project is about building a Real-Time Twitter Analytics Dashboard using Power BI.
It helps to study how tweets perform based on likes, retweets, replies, impressions, and other engagement metrics.
The main goal is to understand how people interact with tweets and what type of tweets get more engagement.

2. Background

Twitter produces a large amount of data every day.
Analyzing this data helps us understand:

* Trends

* Audience behavior

* Tweet performance

* In this project, visuals appear only during specific time periods and only when tweets meet certain conditions.

3. Learning Objectives

* Learn to use Power BI to analyze real-time Twitter data.

* Learn how to write DAX measures for advanced filtering.

* Understand tweet engagement and performance patterns.

* Build interactive visuals that work only under specific conditions.

4. Activities and Tasks

   
🟦 Task 1 — Scatter Chart
Goal:

* Show the relationship between media engagements and media views for tweets that:

* Have more than 10 replies

* Have odd tweet date

* Have word count above 50

* Visual shows only between 6 PM to 11 PM IST

Source Code

Valid Tweet Condition

Valid_Tweet1 =
IF (
    'SocialMedia'[replies] > 10 &&
    'SocialMedia'[WordCount] > 50 &&
    'SocialMedia'[IsOddDate] = 1,
    1,
    0
)

Time Filter

Time1 =

IF(
    HOUR(UTCNOW() + TIME(5,30,0)) >= 18 &&
    HOUR(UTCNOW() + TIME(5,30,0)) <= 23,
    1,
    0
)

🟦 Task 2 — Clustered Bar Chart
Goal:

* Show URL clicks, profile clicks, and hashtag clicks by tweet category.
  Conditions:

* Tweet has at least one type of click

* Even tweet date

* Word count above 40

* Visual shows only between 3 PM to 5 PM IST

Source Code

Valid Tweet Condition

Valid_Tweet2 =
IF (
    'SocialMedia'[WordCount] > 40 &&
    'SocialMedia'[IsEvenDate] = 1,
    1,
    0
)

Time Filter

Time2 =

IF(
    HOUR(UTCNOW() + TIME(5,30,0)) >= 15 &&
    HOUR(UTCNOW() + TIME(5,30,0)) <= 17,
    1,
    0
)

🟦 Task 3 — Top 10 Tweets Chart
Goal:

* Show the top 10 tweets based on total retweets + likes.
Conditions:

* Even impressions

* Odd tweet date

* Word count below 30

* No weekend tweets

* Visual works only 3 PM to 5 PM IST

Source Code

Valid Tweet Condition

Valid_Tweet3 =

IF (
    'SocialMedia'[WeekDay] >= 5 &&
    MOD ( 'SocialMedia'[Impressions], 2 ) = 0 &&
    'SocialMedia'[IsOddDate] = 1 &&
    'SocialMedia'[WordCount] < 30,
    1,
    0
)

Time Filter

Time3 =

IF(
    HOUR(UTCNOW() + TIME(5,30,0)) >= 15 &&
    HOUR(UTCNOW() + TIME(5,30,0)) <= 17,
    1,
    0
)

🟦 Task 4 — Line Chart
Goal:

* Show monthly trend of average engagement rate for:

* Tweets with media

* Tweets without media

* Conditions:

* Even engagement

* Odd tweet date

* Character count above 20

* No tweet word containing "C"

* Visual shows only 7 AM–11 AM and 3 PM–5 PM IST

Source Code

Valid Tweet Condition

Valid_Tweet4 =

IF (
    MOD ( 'SocialMedia'[engagements], 2 ) = 0 &&
    'SocialMedia'[IsOddDate] = 1 &&
    LEN ( 'SocialMedia'[Tweet] ) > 20 &&
    'SocialMedia'[NoWordWithC] = 1,
    1,
    0
)

Time Filter

Time4 =

IF (
    (
        HOUR ( UTCNOW() + TIME ( 5, 30, 0 ) ) >= 7
        && HOUR ( UTCNOW() + TIME ( 5, 30, 0 ) ) <= 11
    )
    || (
        HOUR ( UTCNOW() + TIME ( 5, 30, 0 ) ) >= 15
        && HOUR ( UTCNOW() + TIME ( 5, 30, 0 ) ) <= 17
    ),
    1,
    0
)

🟦 Task 5 — Replies, Retweets & Likes Comparison
Goal:

* Compare replies, retweets, and likes for tweets where:

* Media engagements > median

* Month between June–August 2020

* Even media views

* Odd tweet date

* Character count > 20

* No word containing "S"

* Visual shows between 7 AM–11 AM and 3 PM–5 PM

Source Code

Valid Tweet Condition

Valid_Tweet5 =

IF (
    'SocialMedia'[IsEvenDate] = 1 &&
    MOD ( 'SocialMedia'[media views], 2 ) = 0 &&
    LEN ( 'SocialMedia'[Tweet] ) > 20 &&
    'SocialMedia'[No_S_Word] = 1 &&
    'SocialMedia'[media engagements] > [Median_Media_Engagement] &&
    'SocialMedia'[Year] = 2020 &&
    'SocialMedia'[Month] >= 6 &&
    'SocialMedia'[Month] <= 8,
1,
0
)

Time Filter

Time5 =

IF (
    (
        HOUR ( UTCNOW() + TIME ( 5, 30, 0 ) ) >= 7 &&
        HOUR ( UTCNOW() + TIME ( 5, 30, 0 ) ) <= 11
    )
    ||
    (
        HOUR ( UTCNOW() + TIME ( 5, 30, 0 ) ) >= 15 &&
        HOUR ( UTCNOW() + TIME ( 5, 30, 0 ) ) <= 17
    ),
    1,
    0
)

🟦 Task 6 — Engagement Rate Comparison (App Opens)
Goal:

* Compare engagement rate for:

* Tweets with app opens

* Tweets without app opens

* Conditions:

* Posted between 9 AM–5 PM, weekdays only

* Even impressions

* Odd tweet date

* No word containing "D"

* Character count > 30

* Visual shows between 7 AM–11 AM and 12 PM–6 PM IST

Source Code

Valid Tweet Condition

Valid_Tweet6 =

IF(
    'SocialMedia'[NoWordWithD] = 1 &&
    'SocialMedia'[WeekDay] > 5 &&
    MOD('SocialMedia'[impressions],2) = 0 &&
    'SocialMedia'[IsOddDate] = 1 &&
    LEN('SocialMedia'[tweet]) > 30 &&
    'SocialMedia'[TweeHour] >= 9 &&
    'SocialMedia'[TweeHour] <= 17,
    1,
    0
)

Time Filter

Time6 =

IF(
    (
        HOUR(UTCNOW() + TIME(5,30,0)) >= 7 &&
        HOUR(UTCNOW() + TIME(5,30,0)) <= 11
    )
    ||
    (
        HOUR(UTCNOW() + TIME(5,30,0)) >= 12 &&
        HOUR(UTCNOW() + TIME(5,30,0)) <= 18
    ),
    1,
    0
)

5. Skills and Competencies

* Creating visuals with advanced filters

* Using DAX to apply strict conditions

* Understanding tweet behavior

* Building real-time dashboards with time-based logic

6. Challenges and Solutions
Challenges

* Many conditions for each visual

* Time-based filtering required careful testing

Solutions

* Broke each requirement into smaller parts

* Tested visuals at multiple times to confirm accuracy

7. Outcomes and Impact

* Dashboard gives deep insight into tweet interactions

* Shows how tweet performance changes based on time and content

* Displays only the most relevant data

* Helps understand engagement trends clearly

8. Conclusion

This project improved skills in Power BI, DAX, data modeling, and time-based filtering.
It shows how real-time Twitter data can be analyzed to understand engagement patterns in a meaningful way.

Dashboard 
* The dashboard look like this.
  ![Dashboard Preview]()

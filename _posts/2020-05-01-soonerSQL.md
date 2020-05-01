---
title: "Sooner Database"
date: 2020-05-01
author_profile: true
tags: [SQL]
header:
  image: "/images/sooner header.jpg"
excerpt: "Sooner SQL Database"
layout: single
---

Since birth, I have been watching the Oklahoma Sooners football team play on Saturdays against many other college football teams. The one aspect that I enjoyed the most about Oklahoma football is their mastery of the offense side. This data base logs every Sooner to either run, catch, or throw a the ball from scrimage in the last ten college football seasons.

The database was created using MySQL and a SQL text editor called PopSQL. The data was pulled from [CollegeFootballReference](https://www.sports-reference.com/cfb/schools/oklahoma/) and I edited the columns within Excel to create .csv files. I used this data to create three main tables within the database, Player, Games, Yards.

## Player

This is the table that holds each Player's **Name** and **Position** as well as a unique **player_id** that will serve as the primary_key for each player.

~~~~mysql
CREATE TABLE Player (
    player_id INT PRIMARY KEY,
    name VARCHAR(40),
    pos VARCHAR(3)
 );
~~~~

This code creates the table and defines each column with its corresponding value type. The **player_id** column is also identified as a primary_key with a unique integer.  

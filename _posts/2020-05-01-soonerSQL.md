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


## Games

In this table, I created another primary_key which is for the **game_id** column. This column will hold a unique decimal number for each individual game played, which starts at 1.01 and ends at 10.14 . The first part of decimal indicates the season, most recent first, while the second part indicates the game in that season in sequential order. The other variables are shown below:

<table>
<colgroup>
<col width="30%" />
<col width="70%" />
<col width="30%"/>
</colgroup>
<thead>
<tr class="header">
<th>Columns</th>
<th>Description</th>
<th>Type</th>
</tr>
</thead>
<tbody>

<tr>
<td markdown="span">**game_id**</td>
<td markdown="span"> Decimal value that indicates each specific game by season then week.</td>
<td>*decimal*</td>
</tr>

<tr>
<td markdown="span">**year**</td>
<td markdown="span">The year in which the season of the game started in.</td>
<td markdown="span">*year*</td>
</tr>

<tr>
<td markdown="span">**game_site**</td>
<td markdown="span">If the location was either home, away, or at a neutral location.</td>
<td markdown="span">*Varchar*</td>
</tr>

</tbody>
</table>

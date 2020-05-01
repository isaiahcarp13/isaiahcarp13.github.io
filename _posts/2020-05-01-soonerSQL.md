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
<col width="30%"/>
<col width="70%"/>
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
<td markdown="span">*decimal*</td>
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

<tr>
<td markdown="span">**opp_rank**</td>
<td markdown="span">Opponent's rank in the AP top 25 poll that week.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**opp**</td>
<td markdown="span">The name of the opposing team that week.</td>
<td markdown="span">*Varchar*</td>
</tr>

<tr>
<td markdown="span">**opp_conf**</td>
<td markdown="span">The athletic conference that the Opponent is a member of at the time of the game.</td>
<td markdown="span">*Varchar*</td>
</tr>

<tr>
<td markdown="span">**result**</td>
<td markdown="span">The result of the game expressed either W for wins or L for losses.</td>
<td markdown="span">*Varchar*</td>
</tr>

<tr>
<td markdown="span">**pts_scored**</td>
<td markdown="span">Total points scored by Oklahoma in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**pass_cmp**</td>
<td markdown="span">Total passes completed by the team in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**pass_att**</td>
<td markdown="span">Total passes attempted by the team in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**pass_pct**</td>
<td markdown="span">Total pass completion rate by the team in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**pass_yds**</td>
<td markdown="span">Total passing yards by the team in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**pass_td**</td>
<td markdown="span">Total passing touchdowns by the team in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**rush_att**</td>
<td markdown="span">Total rush attempts by the team in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**rush_yds**</td>
<td markdown="span">Total rushing yards by the team in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**rush_avg**</td>
<td markdown="span">Average rushing yards per play in each game.</td>
<td markdown="span">*decimal*</td>
</tr>

<tr>
<td markdown="span">**rush_td**</td>
<td markdown="span">Total rushing touchdowns by the team in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**tot_plays**</td>
<td markdown="span">Total plays from scrimage by the offense in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**tot_yds**</td>
<td markdown="span">Total yards from scrimage by the offense in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**avg_play**</td>
<td markdown="span">The Average yards for a play from scrimage by the offense in each game.</td>
<td markdown="span">*decimal*</td>
</tr>

<tr>
<td markdown="span">**1st_downs**</td>
<td markdown="span">Total 1st downs for the offense in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**tot_fum**</td>
<td markdown="span">Total fumbles lost by the offense in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**tot_int**</td>
<td markdown="span">Total interceptions thrown by the offense in each game.</td>
<td markdown="span">*INT*</td>
</tr>

<tr>
<td markdown="span">**tot_turn**</td>
<td markdown="span">Total fumbles, interceptions or unsuccessful 4th down attempts, by the offense in each game.</td>
<td markdown="span">*INT*</td>
</tr>

</tbody>
</table>

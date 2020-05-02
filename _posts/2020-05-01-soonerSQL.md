---
title: "Sooner Database"
date: 2020-05-01
author_profile: true
tags: [SQL]
header:
  image: "/images/sooner header.jpg"
excerpt: "Sooner SQL Database"
layout: single
toc: true
toc_label: "Directory"
toc_icon: "football-ball"
toc_sticky: true
---

Since birth, I have been watching the Oklahoma Sooners football team play on Saturdays against many other college football teams. The one aspect that I enjoyed the most about Oklahoma football is their mastery of the offense side. This data base logs every Sooner to either run, catch, or throw a the ball from scrimage in the last ten college football seasons.

The database was created using MySQL and a SQL text editor called PopSQL. The data was pulled from [CollegeFootballReference](https://www.sports-reference.com/cfb/schools/oklahoma/) and I edited the columns within Excel to create .csv files. I used this data to create three main tables within the database, Player, Games, Yards.

https://isaiahcarp13.github.io/downloads/Sooners.zip

## Tables

### Player

This is the table that holds each Player's **Name** and **Position** as well as a unique **player_id** that will serve as the primary_key for each player.

[Download Zip file](https://isaiahcarp13.github.io/downloads/Sooners.zip)


~~~~mysql
CREATE TABLE Player (
    player_id INT PRIMARY KEY,
    name VARCHAR(40),
    pos VARCHAR(3)
 );
~~~~

This code creates the table and defines each column with its corresponding value type. The **player_id** column is also identified as a primary_key with a unique integer.


### Games

In this table, I created another primary_key which is for the **game_id** column. This column will hold a unique decimal number for each individual game played, which starts at 1.01 and ends at 10.14 . The table also contains team passing, rushing, and other scrimage play stats. Here is the code for creating the Games table:

~~~~mysql
CREATE TABLE Games(
	game_id decimal(4,2) PRIMARY KEY,
	year year,
	game_site Varchar(10),
	opp_rank INT,
	opp Varchar(40),
	opp_conf Varchar(20),
	result Varchar(6),
	pts_scored INT,
	pass_cmp INT,
	pass_att INT,
	pass_pct decimal(4,2),
	pass_yds INT,
	pass_td INT,
	rush_att INT,
	rush_yds INT,
	rush_avg decimal(4,2),
	rush_td INT,
	tot_plays INT,
	tot_yds INT,
	avg_play decimal(4,2),
	1st_downs INT,
	tot_fum INT,
	tot_int INT,
	tot_turn INT);
~~~~

### Yards

This table is where each individual's game stats are stored. **game_id** and **player_id** are both foreign_keys that reference the primary_key in the Game and Player Tables. The combination of these two columns creates the primary_key for this table. The following code is what I used to create the table:

~~~~mysql
Create table Yards(
game_id decimal(4,2),
player_id int,
rush_att INT,
rush_yds INT,
rush_td INT,
rec INT,
rec_yds INT,
rec_td INT,
scrm_plays INT,
scrm_yds INT,
scrm_td INT,
pass_cmp INT,
pass_att INT,
pass_pct INT,
pass_yds INT,
pass_td INT,
pass_int INT,
pass_eff decimal(5,2),
PRIMARY KEY(game_id, player_id),
FOREIGN KEY(game_id) REFERENCES Games(game_id) ON DELETE Cascade,
FOREIGN KEY(player_id) REFERENCES Player(player_id) ON DELETE Cascade
);
~~~~

## Sample outputs

### Player Table
~~~~mysql
Select * From Players
limit 10;
~~~~

Will out put this:

<img src="{{ site.url }}{{ site.baseurl }}/images/sooner/player sample.png" alt="player"/>


### Basic Stat Table

I am able to calculate player stats by joining each of the tables together by their primary_key's

~~~~mysql
select p.pos,p.name, sum(y.rush_yds), sum(y.rec_yds), sum(y.pass_yds), sum(y.scrm_yds)
from Player p
join Yards y
on p.player_id = Y.player_id
group by p.player_id
order by sum(y.scrm_yds) desc
limit 10;
~~~~

Will output a table showing the top 10 Sooners in order of scrimage yards along with their rushing, receiving yards.


<img src="{{ site.url }}{{ site.baseurl }}/images/sooner/join table sample.png" alt="join"/>

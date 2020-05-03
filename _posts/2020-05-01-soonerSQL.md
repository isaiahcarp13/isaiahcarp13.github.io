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

The database was created using MySQL and a SQL text editor called PopSQL. The data was pulled from [CollegeFootballReference](https://www.sports-reference.com/cfb/schools/oklahoma/) and I edited the columns within Excel to create .csv files. I used this data to create three main tables within the database, Player, Games, Yards. I have included all the data in CSV form in the following link.

[Download Sooners.Zip](https://isaiahcarp13.github.io/downloads/Sooners.zip)

## Tables

### Player

This is the table that holds each Player's **Name** and **Position** as well as a unique **player_id** that will serve as the primary_key for each player.

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

### Analysis of Offensive performance against ranked opponents
~~~~mysql
select year,
case
    when opp_rank is Null then 'Not Ranked'
    else 'Ranked'
end as ranked,
ifnull(SUM(case when result like 'W' then 1 end),0) as Wins,
ifnull(SUM(case when result like 'L' then 1 end),0) as Losses,
round(SUM(case when result like 'W' then 1 end)/count(game_site) * 100,2) as 'Win %',
round(avg(pts_scored),2) as 'Avg points',
round(avg(pass_td + rush_td),2) as 'Avg TDs',
round(avg(tot_yds),2) as 'Avg Yards'
from Games
group by ranked,year;
~~~~
Will produce:

<img src="{{ site.url }}{{ site.baseurl }}/images/sooner/ranked.png" alt="ranked"/>

As we can see by the table above, Offensive performance does decrease. This is expected as ranked teams usually have better defenses than teams who are not in the AP top 25.

### Stat Leaders by Year

Here is some code that creates a query for the rushing leader for each year. If one wanted to see other top athletes in other stats all you have to do is replace **rush_yds** with another stat in the Yards Table.

~~~~MySQL
with stat_leader as (

    select g.year,p.name,p.pos, sum(y.rush_yds) as 'total rush yards',
    Rank() Over (
        partition by g.year
        order by sum(y.rush_yds) desc
    ) stat_rank

    from yards y
    join player p
    on p.player_id = y.player_id
    join games g
    on g.game_id = y.game_id
    group by g.year,p.name,p.pos
)
select * from stat_leader
where stat_rank <=1;
~~~~

<img src="{{ site.url }}{{ site.baseurl }}/images/sooner/stat leader.png" alt="join"/>

## Summary

Overall I enjoyed creating this database and throughout the process I learned a lot about the teams history and reminisced on how the team made adjustments during each season to tailor to the strengths of the play makers. This project also taught me how to search for data and led to me creating a unique data set. I may update this set in the future however I am looking forward to more database projects to further my skills in the field. 

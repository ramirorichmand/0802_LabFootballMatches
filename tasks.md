# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

DROP TABLE football;
CREATE TABLE football;

1) Find all the matches from 2017.

```
<!-- SELECT * FROM matches WHERE season = 2017; -->
--Selects from entire matches during the 2017 season

```

2) Find all the matches featuring Barcelona.

```sql
<!-- SELECT * FROM matches WHERE awayteam = 'Barcelona' OR hometeam = 'Barcelona'; -->


```

3) What are the names of the Scottish divisions included?

```sql
<!-- --SELECT * FROM divisions WHERE country = 'Scotland'; -->


```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

```sql
<!-- SELECT COUNT(*) FROM matches WHERE division_code = (SELECT code FROM divisions WHERE name = 'Bundesliga') AND (awayteam='Freiburg' OR hometeam='Freiburg'); -->


```

5) Find the teams which include the word "City" in their name. 

```sql
<!-- SELECT hometeam FROM matches WHERE hometeam LIKE '%City%' UNION SELECT awayteam FROM matches WHERE awayteam ILIKE '%City%'; -->


```

6) How many different teams have played in matches recorded in a French division?

```sql
<!-- SELECT COUNT(*) FROM (SELECT hometeam FROM matches WHERE division_code IN (SELECT code FROM divisions WHERE country = 'France') UNION SELECT awayteam FROM matches WHERE division_code IN (SELECT code FROM divisions WHERE country = 'France')) AS french_teams;
 -->


```

7) Have Huddersfield played Swansea in any of the recorded matches?

```sql
<!-- SELECT COUNT(*) FROM matches WHERE hometeam = 'Huddersfield' AND awayteam = 'Swansea' OR hometeam = 'Swansea' AND awayteam = 'Huddersfield'; -->


```

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

```sql
<!-- SELECT COUNT(*) FROM matches WHERE ftr = 'D' AND division_code = 'N1' AND season >= 2010 AND season <= 2015; -->


```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. When two matches have the same total the match with more home goals should come first.

```sql
<!-- SELECT * FROM matches WHERE division_code = 'E0' ORDER BY (fthg + ftag) DESC, fthg DESC; -->


```

10) In which division and which season were the most goals scored?

```sql
<!-- SELECT division_code, season, SUM(ftag + fthg) AS sum_scores FROM matches GROUP BY division_code, season ORDER BY sum_scores DESC FETCH FIRST 1 ROW ONLY; -->


```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)

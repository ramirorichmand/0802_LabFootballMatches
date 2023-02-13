# 08/02 Lab Football Matches SQL

# Criteria 

In this task you will practice writing SQL queries to extract information from a database. In this example we have provided an SQL file which will add details of some football matches played in various countries over the past few years, plus the divisions they were played in. There are two tables:

- **Divisions** lists the reference code for each division, its name and the country it is played in.
- **Matches** lists the division code, home and away team names, home and away goals, result (**H**ome or **A**way win, or **D**raw) and the season in which the match was played.

The database contains only league matches. In league football every team plays every other team both home and away, meaning there will be at least two entries per season for each combination of teams in the league. For example, The matches between Arsenal and Tottenham in 2021 are listed as:

| id   | division_code | hometeam  | awayteam  | fthg | ftag | ftr | season |
|------|---------------|-----------|-----------|------|------|-----|--------|
| 1023 | E0            | Tottenham | Arsenal   | 2    | 0    | H   | 2021   |
| 1202 | E0            | Arsenal   | Tottenham | 2    | 1    | H   | 2021   |

In order to determine if a team has played in a given division in a given season it is only necessary to query **either** `hometeam` or `awayteam`. Similarly, to check if two teams have played each other it is only necessary to query for one of the `hometeam`/`awayteam` permutations.
---

# Tasks

1) Find all the matches from 2017

```sql
SELECT * FROM matches WHERE season = 2017;
```

2) Find all the matches featuring Barcelona

```sql
SELECT * FROM matches WHERE hometeam = 'Barcelona';
```

3) What are the names of the Scottish divisions included?

```sql
SELECT name FROM divisions WHERE country = 'Scotland';
```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

```sql
SELECT code FROM divisions WHERE name = 'Bundesliga';

SELECT COUNT(*) FROM matches WHERE division_code = 'D1' AND (hometeam = 'Freiburg' OR awayteam = 'Freiburg');
```

5) Find the teams which include the word "City" in their name. HINT: Not every team has been entered into the database with their full name, eg. `Norwich City` are listed as `Norwich`. If your query is correct it should return four teams.

```sql
SELECT DISTINCT hometeam FROM matches WHERE hometeam LIKE '%City%';
```

6) How many different teams have played in matches recorded in a French division?

```sql
SELECT code FROM divisions WHERE country = 'France';

SELECT COUNT(DISTINCT hometeam) FROM matches WHERE division IN ('F1', 'F2');
```

7) Have Huddersfield played Swansea in any of the recorded matches?

```sql
SELECT * FROM matches WHERE (hometeam = 'Huddersfield' AND awayteam = 'Swansea');
```

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

```sql
SELECT code FROM divisions WHERE name = 'Eredivisie';

SELECT COUNT(*) FROM matches WHERE division_code = 'N1' AND ftr = 'D' AND season BETWEEN 2010 AND 2015;
```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. When two matches have the same total the match with more home goals should come first.

```sql
SELECT code FROM divisions WHERE name = 'Premier League';

SELECT * FROM matches WHERE division_code = 'E0' ORDER BY (fthg + ftag) DESC, fthg DESC;
```

10) In which division and which season were the most goals scored?

```sql
SELECT division_code, season, SUM (fthg + ftag) FROM matches GROUP BY division_code, season ORDER BY sum DESC LIMIT 1;

SELECT name FROM divisions WHERE code = 'EC';
```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)

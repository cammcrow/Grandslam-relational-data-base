# Grand Slam Prize Money Analysis (2000–2025)

A self-initiated SQL project analysing gender pay gap trends across all four Grand Slam tennis tournaments over a 25-year period.

## Project Overview

This project explores how and when the four Grand Slam tournaments — Wimbledon, the US Open, the French Open, and the Australian Open — achieved equal prize money between male and female singles champions, and how total prize money has grown over time.

The database was designed and built from scratch using SQLite, with data sourced manually from Wikipedia and verified against official tournament records.

## Key Findings

- The **US Open** was the first Grand Slam to offer equal prize money, achieving parity as far back as 1973
- The **Australian Open** reinstated equal pay in 2001 after a period of disparity in the late 1990s
- The **French Open** equalised in 2006, partly driven by Venus Williams' public campaign the previous year
- **Wimbledon** was the last to follow, achieving equal pay in 2007
- Since 2007 all four slams have offered equal prize money, with total winner prizes growing significantly — the US Open now pays $3.6 million per singles champion compared to $800,000 in 2000

## Tools Used

- **SQLite / DB Browser for SQLite** — database design, population, and querying
- **SQL** — data insertion, filtering, aggregation, and analysis

## Database Structure

Single table: `Grand_slam_prize_money`

| Column | Type | Description |
|--------|------|-------------|
| year | INTEGER | Year of tournament |
| grand_slam | TEXT | Tournament name |
| atp_prize_usd | INTEGER | Men's singles winner prize (USD) |
| wta_prize_usd | INTEGER | Women's singles winner prize (USD) |
| equal_pay | TEXT | Whether prize money was equal (Yes/No) |

## Example Queries

**Find all years where pay was not equal:**
```sql
SELECT year, grand_slam, atp_prize_usd, wta_prize_usd,
       atp_prize_usd - wta_prize_usd AS pay_gap
FROM Grand_slam_prize_money
WHERE equal_pay = 'No'
ORDER BY year, grand_slam;
```

**Compare average winner prize by tournament:**
```sql
SELECT grand_slam, ROUND(AVG(atp_prize_usd), 0) AS avg_prize
FROM Grand_slam_prize_money
WHERE atp_prize_usd IS NOT NULL
GROUP BY grand_slam
ORDER BY avg_prize DESC;
```

**Track prize money growth over time at Wimbledon:**
```sql
SELECT year, atp_prize_usd, wta_prize_usd
FROM Grand_slam_prize_money
WHERE grand_slam = 'Wimbledon'
ORDER BY year;
```

## Why This Project

Built independently to develop practical SQL skills through a dataset that was personal to me. The gender pay gap in professional sports is a well-documented issue and tennis is a useful case study; It was one of the first sports to address it, but the timeline varied significantly across tournaments. Mapping that through data felt like a more meaningful way to learn than completing an online course.

## Files

- `grand_slam_prize_money.sql` — full database schema and data insertion script
- `README.md` — this file

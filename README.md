# Esports Prize Money: Market Concentration, 1998–2024

An exploratory data analysis of how esports prize money is distributed across games and genres, and how that distribution changed over time, including the effect of the 2020 pandemic.

**Author:** Daria Semenova
**Tools:** Python (pandas, matplotlib), Google Colab

## Research questions

1. How concentrated is esports prize money among a small number of games?
2. How did this concentration change between 1998 and 2024?
3. What happened to the market in 2020, and did it return to its previous structure afterwards?
4. Which genres capture most of the prize money?

## Data

- Source: Kaggle dataset [`rankirsh/esports-earnings`](https://www.kaggle.com/datasets/rankirsh/esports-earnings) (see the dataset page for the original source and licence).
- `GeneralEsportData.csv`: one row per game (669 games). Columns: `Game`, `ReleaseDate`, `Genre`, `TotalEarnings`, `OfflineEarnings`, `PercentOffline`, `TotalPlayers`, `TotalTournaments`.
- `HistoricalEsportData.csv`: monthly records per game (10,239 rows, January 1998 – October 2024). Columns: `Date`, `Game`, `Earnings`, `Players`, `Tournaments`.
- The data files are not included in this repository. Download them from Kaggle and place them next to the notebook.

## Methods

- **Top-N share:** the share of yearly prize money earned by the 5 largest games.
- **Herfindahl–Hirschman Index (HHI):** the sum of squared market shares of all games in a year. Values closer to 1 mean higher concentration.
- **Genre shares:** yearly prize money by genre, after joining the monthly data with the genre labels.
- **Prize per player:** `TotalEarnings / TotalPlayers` per game, summarised by genre (median).

## Key findings

1. **Cumulative prize money is highly concentrated.** The 10 largest games out of 669 (about 1.5%) account for 64% of all prize money in the dataset. Dota 2 alone accounts for roughly one-fifth.
2. **Concentration fell over time.** The top-5 games took 99–100% of prize money in 1998–2000, about 62–67% in 2018–2019, and about 41–51% from 2020 onwards. HHI fell from 0.148 (2019) to 0.053 (2020) and stayed around 0.055–0.07 in 2021–2024.
3. **2019 looks like an outlier.** Fortnite took 31% of prize money that year (Battle Royale as a genre took 39%), which is consistent with a single mega-event, but this explanation needs an external source.
4. **2020 hit the largest tournaments.** Total prize money fell from about 258M USD (2019) to about 153M USD (2020), and Dota 2's share fell from 0.18 to 0.07. It recovered in 2021 (about 262M USD), but concentration did not return to its pre-2020 level.
5. **After 2020 no single title dominates.** The top game holds 13–18% of prize money, and mobile titles (e.g. Arena of Valor, PUBG Mobile) appear in the yearly top 3.
6. **Dispersed across games, but not across genres.** MOBA, first-person shooters and Battle Royale together hold about 78–80% of prize money in 2022–2024. Sports titles grew from about 4% (2017) to 10% (2024), while collectible card games almost disappeared.

7. **Genres differ in how prize money is spread across games and players.** Over the whole period, MOBA (29 games), first-person shooters (138) and Battle Royale (17) hold about 80% of all prize money, from 184 of 669 games. Battle Royale has the highest median prize per player (about 10,300 USD), followed by Sports (about 6,500 USD), MOBA (about 3,700 USD) and first-person shooters (about 3,100 USD). Fighting games, with 189 titles, have a median of only about 250 USD per player.

| Genre | Games | Total prize money (USD) | Median prize per player (USD) |
|---|---|---|---|
| Multiplayer Online Battle Arena | 29 | 643.8M | 3,663 |
| First-Person Shooter | 138 | 483.6M | 3,125 |
| Battle Royale | 17 | 390.4M | 10,317 |
| Strategy | 68 | 135.8M | 2,047 |
| Sports | 98 | 106.4M | 6,537 |
| Collectible Card Game | 17 | 51.5M | 2,248 |
| Fighting Game | 189 | 39.7M | 247 |
| Racing | 66 | 18.5M | 2,655 |

*Prize per player is `TotalEarnings / TotalPlayers` for each game; the table shows the median of this value across games in a genre. It is a rough measure: it includes players with very small payouts and does not adjust for inflation or time period.*

## Figures

![Prize money by year](fig1_prize_by_year.png)

![Top-5 share by year](fig2_top5_share.png)

## Limitations

- The data are at the level of games, not players, so there is no information about countries, teams or gender.
- 2024 covers only January–October and may be incomplete; recent records may also be added later. The apparent decline in 2023–2024 should not be interpreted as a trend.
- Prize money is in nominal USD, without inflation adjustment.
- Prize money is not industry revenue: it excludes sponsorship, advertising, streaming and player salaries.
- The analysis is descriptive. Explanations for the changes (pandemic, mega-events, rise of mobile games) are hypotheses and are not tested statistically.

## How to reproduce

1. Download the two CSV files from the Kaggle page above.
2. Open `esports_prize_money_analysis.ipynb` in Google Colab or Jupyter.
3. Upload the CSV files and update the file paths in the first cell.
4. Run all cells.

## Possible next steps

- Look at the distribution of prize money per player inside the largest games (needs player-level data).
- Test the effect of the 2020 break with a regression on yearly data.
- Adjust prize money for inflation.

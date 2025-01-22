# FOOTBALL-TRANSFER-ANALYSIS
## Introduction to Football Player Transfers Dataset
Football player transfers are an integral part of the global football industry, reflecting the dynamic and competitive nature of the sport. The dataset analyzed in this report comprises information about 54 football players and their transfer details, offering insights into the movement of players between clubs and countries. Key attributes of the dataset include the origin of each transfer, the player's name, the country and club they transferred from, the destination country and club, their playing position, and the associated transfer fees. Additionally, the dataset captures the year of each transfer and the birth year of the players, providing opportunities to explore trends over time and correlations with player demographics.
This dataset serves as a valuable resource for understanding patterns in player transfers, such as the most active countries in exporting and importing players, trends in transfer fees over time, and the positional distribution of high-value transfers. With the rich information contained within the dataset, this analysis aims to uncover meaningful insights about the economics and strategy behind football player transfers, offering a deeper understanding of how clubs invest in talent to strengthen their teams.
# Exploratory Data Analysis (EDA)
- Origin: The player's country of origin.
- Player: The name of the player.
- From (Country): The country the player transferred from.
- From (Club): The club the player transferred from.
- To (Country): The country the player transferred to.
- To (Club): The club the player transferred to.
- Position: The position the player plays on the field.
- Fee (€ mln): The amount paid by the country the player was transferred to.
- Fee (£ mln): The amount paid by the club the player was transferred to.
- Year: The year the transfer occurred.
# Tools:-
## Excel, Power BI and SQL.

# Project Objectivs:- 
## Write SQL Query to solve the following problems and interpret the result
1.	Most expensive transfers by year, position, and club.
2.	Trends in transfer fees over the years. (This analysis Identifying years with unusually high or low transfer activity and fees, possibly due to market dynamics, global events, or regulations.)
3.	Countries with the highest player transferred with total fees.
4.	Identify top transfer deals by player positions (e.g., Goalkeeper, Defender, Midfielder, Forward).
5.	Analyze which clubs spend the most on player transfers.
6.	Investigate whether a player’s age influences their transfer fee.
7.	Create a flow diagram or a heatmap showing player transfers between countries.
8.	Highlight countries with the highest exports of players with the transfer fees.
9.	Extract top transfers by year.
10.	Compare the average and median fees by position across years.

# Solution
1. Most expensive transfers by year, position, and club

```SQL
WITH TopTransfers AS (
    SELECT DISTINCT ON (year, position, "to(club)")
        year,
        position,
        "to(club)",
        player,
        paid_club
    FROM football
    ORDER BY year, position, "to(club)", paid_club DESC
)
SELECT *
FROM TopTransfers
ORDER BY paid_club DESC
LIMIT 10;


"year"	"position"	"to(club)"	"player"	"paid_club"
2017	"Forward"	"Paris Saint-Germain"	"Neymar"	198
2018	"Forward"	"Paris Saint-Germain"	"Kylian Mbappé"	163
2019	"Forward"	"Barcelona"	"Antoine Griezmann"	107
2018	"Midfielder"	"Barcelona"	"Philippe Coutinho"	105
2019	"Forward"	"Atlético Madrid"	"João Félix"	104.1
2021	"Midfielder"	"Manchester City"	"Jack Grealish"	100
2017	"Forward"	"Barcelona"	"Ousmane Dembélé"	97
2019	"Forward"	"Real Madrid"	"Eden Hazard"	89
2016	"Midfielder"	"Manchester United"	"Paul Pogba"	89
2018	"Forward"	"Juventus"	"Cristiano Ronaldo"	88
```
# Interpretation:-
This table showcases how clubs prioritize key positions and players to enhance their squads,
with transfer fees often reflecting the players’ talent, age, and potential marketability.
It also highlights the financial disparity between elite clubs and others in the footballing world.

# Overall Patterns
* Paris Saint-Germain: Dominates with two of the highest fees (Neymar and Mbappé), reflecting their
  aggressive investment strategy.
* Barcelona: Frequently appears in the list, indicating their heavy spending to rebuild and remain
  competitive in European football.
* Forward Dominance: The forward position sees the highest transfer fees, illustrating the premium
  placed on goal-scoring players.
* Rising Transfer Fees: The increasing values over the years highlight the inflation in the football
  transfer market.

2.	Trends in transfer fees over the years. 
This analysis Identifying years with unusually high or low transfer activity and fees, possibly due to market dynamics, global events, or regulations.
```
SELECT 
    year,
    COUNT(*) AS total_transfers,
    SUM(paid_club) AS total_fees,
    AVG(paid_club) AS avg_fee,
    MIN(paid_club) AS min_fee,
    MAX(paid_club) AS max_fee
FROM football
GROUP BY year
ORDER BY year DESC;

"year"	"total_transfers"	"total_fees"	"avg_fee"	"min_fee"	"max_fee"
2021	3	224.3	74.76666666666667	51.3	100
2020	5	317.44	63.488	54.8	70
2019	14	1013.8	72.41428571428571	52.4	107
2018	11	847.45	77.0409090909091	52.75	163
2017	5	480	96	52	198
2016	2	164.3	82.15	75.3	89
2015	3	143	47.666666666666664	44	55
2014	3	187.7	62.56666666666666	59.7	65
2013	3	192	64	51	86
2009	3	192	64	56	80
2001	1	46.6	46.6	46.6	46.6
2000	1	37	37	37	37
```
# Columns and Interpretation:
1.	year: The year the transfers occurred.
2.	total_transfers: The total number of player transfers that occurred in that year.
3.	total_fees: The total amount spent on all transfers in that year.
4.	avg_fee: The average transfer fee per player for that year.
5.	min_fee: The smallest transfer fee for a player in that year.
6.	max_fee: The highest transfer fee for a player in that year.

# Interpretation of Trends in Transfer Fees Over the Years
## Key Observations:
1. Increase in Total Fees Over Time:
- There is a noticeable increase in total transfer fees over the years, especially after 2015.
For example:
•	In 2000, the total fees were £37 million for one transfer.
•	In 2021, the total fees soared to £224.3 million for only 3 transfers.
This shows a significant increase in spending on transfers, likely due to the growing commercial value of football, increased sponsorship deals, and improved financial capabilities of top clubs.

2.	Number of Transfers:
- 2019 saw the highest number of transfers (14), while the earlier years like 2000 and 2001 saw only one transfer.
- The 2019 data shows that despite the higher number of transfers, the total fees are much higher compared to years with       fewer transfers.
  - This could indicate more globalized activity in the transfer market in recent years, with more clubs able to afford         expensive players.
    
3.	Fluctuating Average Transfer Fee:
- The average fee has fluctuated over time:
•	The highest average was in 2017 (£96 million), driven by high-profile transfers such as Neymar's move to PSG.
•	The lowest average was in 2000 and 2001 (£37 million), reflecting a very different financial landscape.
•	The general trend shows that as the total transfer fees have risen, the average fee per player has also increased,           indicating higher-valued players being transferred.

4.	Maximum and Minimum Fees:
- Maximum fees have dramatically increased:
•	In 2000, the maximum transfer fee was £37 million.
•	By 2021, the maximum reached £100 million for high-profile players like Jack Grealish.
•	The minimum fee shows how much clubs are still willing to pay for players, though the minimum has steadily increased as     clubs are now willing to invest in younger and more marketable talent.

5.	Outliers and High-Profile Years:
- 2018 and 2019 had significant spikes in total fees, largely due to expensive transfers like Kylian Mbappé and Philippe       Coutinho. These years indicate a period of aggressive spending by top clubs (e.g., PSG, Barcelona).
- 2021 also shows significant spending on fewer transfers (3), which might indicate the signing of high-value, marquee         players such as Jack Grealish.

## Summary of the Trend:
•	Early Years (2000-2013): Football transfer fees were much lower and less frequent. The average fee per player was under     £100 million, and only a few major transfers occurred each year. The market was smaller, with fewer players commanding     large fees.
•	2014-2017: We see a rise in both the number of transfers and the total fees, with a dramatic increase in the most            expensive transfers. Clubs began investing more heavily in star players, and the market saw record-breaking moves (e.g.,    Neymar, Paul Pogba).
•	2018-2021: Transfer fees hit new heights, with 2021 being a significant year of spending. The total transfer spending in     these years rose sharply, reflecting the growing commercial nature of football and the financial influence of clubs like     PSG, Manchester City, and Barcelona. These years were marked by fewer, but more expensive, transfers.

## Conclusion:
The trends in transfer fees show how the football transfer market has evolved from modest investments in the early 2000s to becoming a multi-billion-pound industry today. Factors such as broadcasting deals, commercial interests, and financial strategies of top clubs have played a role in pushing these numbers higher over time.


3.	Countries with the highest player transferred with total fees.
```
SELECT 
    country,
    SUM(total_transfers) AS total_transfers,
    SUM(total_fees) AS total_fees
FROM (
    SELECT 
        "from(country)" AS country,
        COUNT(*) AS total_transfers,
        SUM(paid_country) AS total_fees
    FROM football
    GROUP BY "from(country)"
    
    UNION ALL
    
    SELECT 
        "to(country)" AS country,
        COUNT(*) AS total_transfers,
        SUM(paid_country) AS total_fees
    FROM football
    GROUP BY "to(country)"
) subquery
GROUP BY country
ORDER BY total_fees DESC;

"country"	"total_transfers"	"total_fees"
"England"	37	2955.3999999999996
"Spain"	29	2559.1000000000004
"Italy"	     	16	1206.5
"France"	12	1185.5
"Germany"	9	669.7
"Portugal"	2	194
"Netherlands"	2	150
"China"	1	61
```
## General Insights:
- England and Spain Lead:
•	These countries dominate in both total transfers and fees, driven by globally recognized leagues and financially powerful clubs.
- Concentration of Spending:
•	Fewer transfers in France and Italy suggest concentrated spending by a few top clubs (e.g., PSG, Juventus).
- Smaller Leagues:
•	Countries like Portugal, the Netherlands, and China have fewer transfers, but their high fees for a small number of deals suggest selective but expensive acquisitions.

4. Identify top transfer deals by player positions (e.g., Goalkeeper, Defender, Midfielder, Forward).
```
SELECT position, SUM(paid_club) AS "Total_fees"
FROM football
GROUP BY position
ORDER BY  "Total_fees" DESC;

"position"	"Total_fees"
"Forward"	1311.1
"Midfielder"	1268.65
"Striker"	617.8
"Defender"	520.4399999999999
"Goalkeeper"	127.6
```
## General Insights:
1.	Attackers Are Most Expensive:
•	Positions contributing directly to goal-scoring (forwards and strikers) collectively dominate transfer spending, reflecting their pivotal role in winning matches and attracting fans.
2.	Midfielders' Importance:
•	High spending on midfielders emphasizes their crucial role in balancing defense and attack, as well as dictating the tempo of games.
3.	Defenders and Goalkeepers Are Undervalued:
•	Defenders and goalkeepers, while essential, command significantly lower fees. This may be due to their lower visibility and lesser direct impact on scoring goals.

## Conclusion:
This data illustrates how clubs prioritize spending based on positions. Attacking players dominate transfer markets due to their impact on scoring and entertainment value. In contrast, defensive players and goalkeepers, while critical for team success, tend to have lower market values, reflecting their perceived lesser role in driving commercial appeal and fan engagement.

5. Analyze which clubs spend the most on player transfers.
```
SELECT "to(club)", SUM(paid_club) AS "Total_fees"
FROM football
GROUP BY "to(club)"
ORDER BY "Total_fees" DESC;

"to(club)"	"Total_fees"
"Barcelona"	549.8
"Paris Saint-Germain"	511.3
"Real Madrid"	510
"Manchester City"	500.64
"Manchester United"	376.7
"Juventus"	296.8
"Chelsea"	257.6
"Liverpool"	183.75
"Atlético Madrid"	167.1
"Arsenal"	128.1
"Internazionale"	74
"Bayern Munich"	68
"Napoli"	65
"Tottenham Hotspur"	53.8
"Shanghai SIPG"	52
"Monaco"	51
```
- General Insights:
1.	Top Spenders Dominate:
•	Barcelona, PSG, Real Madrid, and Manchester City lead in spending, driven by their ambition to compete at the highest levels and attract global fans.
2.	Strategic Spending:
•	Clubs like Liverpool and Bayern Munich show more measured spending, focusing on value-for-money signings rather than sheer volume or big names.
3.	Smaller Clubs:
•	Clubs like Napoli, Tottenham Hotspur, and Monaco reflect limited financial power or a focus on nurturing young talent rather than acquiring established stars.
Conclusion:
This data illustrates how the financial muscle of clubs influences the transfer market. Wealthier clubs dominate the market, using their resources to acquire marquee players and enhance competitiveness, while smaller clubs adopt more sustainable, long-term strategies.

6. Investigate whether a player’s age influences their transfer fee (Paid_club).
```
SELECT 
    CORR(born, paid_club) AS age_transfer_fee_correlation
FROM football;

"age_transfer_fee_correlation"
0.23309111158290377
```
- A correlation value of 0.233 suggests a weak positive relationship between a player's age and their transfer fee.
This indicating that age has a minor influence on transfer fees.

## The result of this is display for better understanding in power BI dashboard

- A decreasing trendline in the scatter plot suggests that younger players tend to have higher transfer fees compared to older players. This pattern can be explained by several factors often observed in football (or similar sports markets).


8. Highlight countries with the highest exports of players.
```
SELECT 
    oringin AS exporting_country,
    COUNT(*) AS total_exports, SUM(paid_country) AS "Transfer fees"
FROM football
GROUP BY oringin
ORDER BY total_exports DESC
LIMIT 10;
"exporting_country"	"total_exports"	"Transfer fees"
"France"	9	861.2
"Portugal"	6	515
"Brazil"	6	629.5
"Belgium"	4	340
"England"	4	351.5
"Argentina"	3	229.6
"Spain"	3	215.5
"Netherlands"	3	234.5
"Colombia"	2	135
"Uruguay"	2	146.8
```
- Insights and Interpretation
1. Top Exporting Countries:
-	France leads with the highest number of exports (9 players) and the highest total transfer fees (861.2 million). This suggests that France not only exports the most players, but those players are of significant market value.
-	Brazil follows closely with 6 players exported and 629.5 million in transfer fees, indicating strong player development and a healthy market for Brazilian football talent.
-	Portugal has 6 players exported but with a slightly lower total transfer fee (515 million), suggesting that while Portugal is a major exporter, their players might have lower average fees compared to France and Brazil.

2. Export Fees Relative to Number of Exports:
-	Belgium and England have 4 players exported, but Belgium has a higher transfer fee (340 million) compared to England (351.5 million), suggesting that the players exported from England may have higher individual fees.
-	Netherlands and Argentina both export 3 players, with Netherlands having a higher transfer fee (234.5 million) than Argentina (229.6 million), indicating that Dutch players might be valued slightly more in the market.

3. Minor Exporters with Significant Transfer Fees:
-	Uruguay has 2 exports with a transfer fee of 146.8 million, which is notably higher than Colombia’s 135 million despite having the same number of exports.
-	Algeria, Sweden, United States, Gabon, Germany, Serbia, Ivory Coast, Nigeria, Bosnia and Herzegovina, Wales, Morocco, and Guinea all have 1 player exported. Despite having fewer exports, these countries still generate transfer fees, ranging from 60 million (for some) to 100 million (Wales). While the export volume is low, the transfer fees show that there are still notable players being transferred from these countries, particularly for countries like Wales (100 million).

## Insights from Transfer Fees:
- High Fees and Strong Development: Countries like France, Brazil, and Portugal appear to have strong football infrastructures and development systems, with a high volume of players exported and substantial transfer fees.
-	Smaller Exporters with High Value Players: Even smaller exporters like Uruguay, Colombia, and Wales show that some countries can command high transfer fees for their football talent, suggesting they export high-potential players.
-	High Exporters, Lower Transfer Fees: Countries with high export numbers (e.g., Portugal and Belgium) have slightly lower transfer fees compared to countries like France or Brazil, potentially because they export more mid-tier players rather than top-tier stars.

# Conclusion
The analysis of football player transfers has provided valuable insights into the evolving dynamics of the global football market. Over the years, the transfer fees have increased significantly, reflecting the growing financial capabilities of clubs, changing market conditions, and the increasing commercial value of football. The dominance of clubs like Paris Saint-Germain, Barcelona, and Manchester City in spending on player transfers highlights their ambition to compete at the highest levels, while also influencing global football economics. Additionally, the positional trends suggest that forwards and midfielders, due to their goal-scoring and game-controlling abilities, are often the highest-valued players in the transfer market.
The examination of countries with the highest player exports shows that nations such as France, Brazil, and Portugal are not only major exporters of football talent but also generate substantial revenue through transfer fees. On the other hand, countries with fewer exports, like Uruguay and Colombia, still command high fees for their players, underscoring the significance of individual player potential and market demand.
Moreover, the analysis revealed a weak positive correlation between a player's age and transfer fee, suggesting that while age may influence transfer decisions, it is not the primary determinant in the value of a player. The trends also reflect a growing trend of high-profile players being transferred for record-breaking fees in recent years, indicating the increasing commercialization of football.


# Recommendations
- Investment in Youth Development: Countries like France, Brazil, and Portugal have shown that investing in youth development and football academies can lead to a sustainable flow of talented players who can be sold for high transfer fees. Other countries should consider focusing on improving their youth development programs to nurture talent from an early age.
- Strategic Spending by Clubs: While clubs like Paris Saint-Germain and Barcelona dominate the market, clubs with smaller budgets should focus on strategic spending, targeting emerging talent and investing in player development rather than relying solely on marquee signings. This can provide long-term financial sustainability and competitiveness.
- Position-Specific Transfers: Clubs should prioritize investing in attacking players, as the forward and striker positions consistently dominate transfer fees. However, they should also not overlook the importance of strengthening other areas of the team, such as midfield and defense, which are essential for a well-rounded squad.
- Age-Related Transfer Strategies: Given the weak correlation between age and transfer fees, clubs should adopt more data-driven approaches to player recruitment, focusing on factors such as player performance, potential, and marketability rather than age alone.
- Market Expansion: Smaller football markets, such as those in countries like Uruguay and Colombia, should focus on increasing their global visibility to attract attention from top clubs. These nations could benefit from stronger commercial partnerships, sponsorships, and talent scouting to raise their profiles in the international football market.
- Analysis of Transfer Fee Trends: Monitoring transfer fee trends can help clubs anticipate market changes and make informed decisions about when to buy or sell players. Analyzing historical data and market conditions can give clubs an edge in negotiating better deals and optimizing their transfer strategies.
By adopting these recommendations, clubs, players, and countries can navigate the complexities of the global football transfer market while ensuring long-term success and financial growth.

Thanks. 
For any questions, additions, or contributions regarding the work I posted on GitHub, feel free to reach out to me at
Email :- adekunletimothy92@gmail.com
Linkedin :- https://linkedin.com/in/timothyadekunle1992

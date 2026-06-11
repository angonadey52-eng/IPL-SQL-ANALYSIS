📌 Project Overview

Most cricket analytics rely on superficial leaderboard metrics (highest runs, highest wickets). This project takes a deeper, franchise-first scouting approach using MySQL to evaluate player performance across the 2018 and 2019 IPL seasons.

By querying raw player databases, we isolate high-impact athletes who balance raw volume with critical efficiency benchmarks (such as Strike Rate $\ge 130$ and Economy Rate $< 7.0$).

🔍 The Scouting Framework & Analytical Questions

We constructed standard query frameworks to translate sports logic into database questions:

The Multi-Season Anchor: Which batsman consistently delivered elite run volume across consecutive seasons (2018–2019)?

Aggressive Efficiency: Which batsmen scored heavily while maintaining a Strike Rate $\ge 130$ under high pressure?

The Boundary Catalyst: Who maximized run rates by hitting boundaries (Fours + Sixes) rather than relying on risky running between the wickets?

The Defensive Weapon: Which bowlers consistently took wickets while keeping their tournament Economy Rate strictly under $7$ runs per over?

📊 Key Scouting Insights

🏏 The Ultimate Asset: KL Rahul emerged as the most consistent batsman over the two-year span, scoring a combined $1252$ runs.

🔥 The Boundary Master: Rishabh Pant dominated the 2018 season by maximizing boundaries, reducing reliance on singles to drive the scoreboard rate.

🎯 Elite Defensive Shield: Rashid Khan ($21$ Wkts, $6.73$ rpo) and Andrew Tye ($24$ Wkts, $6.85$ rpo) stood out as the premium bowler profiles balancing high-strike wickets with strict run-containment.

📈 Unit Dominance: Kings XI Punjab showcased the strongest collective batting line-up depth in 2019, accumulating a total of $2141$ runs.

🛠️ SQL Engineering & Toolkit

To clean, merge, and extract these performance profiles, the following SQL features were leveraged:

Relational Joins (JOIN): Merged seasonal player tables on unique player keys to track multi-season athlete evolution.

Aggregations & Grouping (SUM(), GROUP BY): Compiled individual player outcomes to evaluate franchise-wide performance.

Calculated Fields: Built on-the-fly mathematical indicators (e.g., adding 4s + 6s to evaluate boundary dominance profiles).

Threshold Constraints (WHERE, HAVING): Cleanly filtered out elite athletic benchmarks like:

WHERE S_R >= 130 -- Strike Rate constraint
WHERE E_R < 7    -- Economy Rate constraint


💻 Sample Query Highlight

Querying Multi-Season Run Leaders (2018-2019)

SELECT 
    b18.Player, 
    (b18.Runs + b19.Runs) AS Total_Runs
FROM `IPL_analysis.2018_Batsmen_new` b18
JOIN `IPL_analysis.2019_Batsmen_new` b19 
  ON b18.Player = b19.Player
ORDER BY Total_Runs DESC
LIMIT 1;


📂 Project Structure

├── datasets/                 # Raw 2018 and 2019 IPL CSV datasets
├── sql_scripts/              # Clean SQL files containing all 9 scouting queries
├── presentations/            # HTML slides showcasing analytical findings
└── README.md                 # Project summary and documentation


🚀 How to Run the Queries

Set up the Schema: Clone this repository and import the raw .csv datasets into your MySQL environment (e.g., under a database named IPL_analysis).

Execute Scripts: Run the .sql files found inside the sql_scripts/ directory in sequence.

Evaluate Results: Modify the performance filters (e.g., changing E_R < 7 to E_R < 8.5) to test alternative coaching scouting strategies!

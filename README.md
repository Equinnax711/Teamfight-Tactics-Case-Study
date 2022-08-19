TFT: A Case Study of Equinnax, Challenger Players, & Predictions

Introduction:

Over the past 2 months of summer break, I’ve been playing a game called Teamfight Tactics, otherwise known as TFT. TFT is an autochess battler where you build the best team you can with select units from the set and try to knock your opponents out of hit points to become the final person left standing. There is a lot of nuance and a high learning curve when trying to get into the game, so I’ll create a brief overview of how the game is supposed to be played and important tidbits that you should know before reading the case study.

The objective of the game is to buy different units from a shop that refreshes every round, place them on your own board to create an unique team composition, and battle other opponents that are doing the same!
There are 7 opponents that you must beat in order to get first place. If you get top 4, it is considered a win!
You can spend two gold to refresh your shop! This can be done infinitely per round as long as you have enough gold to refresh it.
Buying three of the same base unit will combine and upgrade the unit to a single 2-star unit, and having three 2-stars of the same unit will combine and upgrade it to a single 3-star unit!
There are different tiers of units with increasing power levels, with 1-costs costing 1 gold, 2-costs costing 2 gold, 3-costs costing 3 gold, 4-costs costing 4 gold, and legendaries costing 5 gold. Within this set, there is an added mechanic called “dragons”. Some dragons are considered 4-cost but cost 8 gold, while others are considered legendaries but cost 10 gold. Dragons take up 2 spots on the field but are very strong.
Each unit has different traits, when you field a certain amount of units with the same trait, the units that hold that trait get a certain buff. For example, when fielding two “Shapeshifters”, both the shapeshifters will gain extra hit points when they transform! Click here to see all traits and their effects!
When you lose combat against an opponent, hit points will be subtracted from your hit point total. When you win combat against an opponent, hit points will be subtracted from their hit point total. Everyone starts out with 100 hit points.
For the 2nd, 3rd, and 4th stages which consist of 6 rounds each, you will get an augment on each the first round of each stage. Three random augments are given to you to pick from. Each augment will give your team a certain perk or upside! Click here to see all augments and their effects!
Each unit is able to hold three items. Each item is created through either augments or combining two item components.
A leveling system is in play which allows you to go from level 1 to level 9. When you go up one level, you are able to field an additional unit. The higher level you are, the higher the odds of finding higher cost units.

This concludes a brief overview of TFT as a game, but there are many more parts to the game that I haven’t covered such as different playstyles, different team compositions, and different tempo swings. This depth of gameplay makes the game very enjoyable and fun to play!

Within this case study, I’ll first be analyzing my own gameplay data. I’ll be looking at what types of traits and augments I’ve used the most and see which of those gives my own style of gameplay the best results. I’ll also answer a question that I’ve always had throughout the set: “In the case of my gameplay, does dealing more damage to other players correlate to a higher placement?”.

Second, I’ll be analyzing the gameplay data of the rank 1 North American player. This player is the best of the best, giving a much more accurate depiction of what traits and augments are the best to pick and use compared to my own gameplay. 

Personal Account (Equinnax) Analysis:

Data Collection:

To collect the data for my own account, I utilized Riot Games’s API to query the necessary information needed to conduct my analysis. This dataset had a total of 200 games of TFT that I played on my own account during set 7, standard and hyper roll modes included. Here is a sample of the raw dataset that I queried.

*Example of raw dataset*

There are a total of 200 rows and 17 columns in the dataset, making up all the data queried from the Riot API. Several of these columns will not be included in the final cleaned dataset.

*Dataset Column Descriptions*

Data Formatting & Cleaning:

To start formatting and cleaning the dataset, the size of the dataset, the datatypes in each column, and if there were any NULL values in the entire dataset was printed out through the use of the “info” function. After confirming there were no NULL values, consistent data types in each row, and matching lengths in each column, I was able to begin transforming and cleaning the data to make it easier to digest.

First, the “Game Length” and “Time Eliminated” columns were transformed from seconds to minutes for easier digestion. This allowed me to quickly understand the timeframe at which the games were played and how long it took for me to get knocked out or win. 

Second, the “TFT Set Number” column was filtered to show only the games played in Set 7. This is important as previous sets, such as set 6 and 6.5, have different mechanics and different champs. Including those sets in my dataframe would lead to an inconsistency in gameplay and data collection for following columns.

Third, the “Augments” column was filtered out through the use of regular expressions, extracting only the augment names. New columns were created for each augment type (first, second, or third augment) and the extracted values were placed in their respective columns. This increased the readability of the table as the previous augment column had lists in each cell, containing all three augments in a list as well as unnecessary information.

Fourth, the “Traits” column was cleaned out through the use of regular expressions, extracting only the traits used in each unique game. Similar to the “Augments” column, unnecessary information was removed, leaving a list of traits that I had active on my board in each cell.

Fifth, the “Units” column was cleaned in the same pattern as the “Traits” column, extracting the name of the units placed on the board in each game. Information unnecessary to my analysis was removed, leaving a list of unit names in each cell.

Sixth, several units within the “Units” column had placeholder names, such as “DragonGreen” and “DragonPurple”. I replaced all of these placeholder names with the unit’s actual names to ensure that the naming conventions would be made consistent across the “Units” column.

Seventh, I dropped all rows that had “Turbo” as its TFT Game Type. Because Turbo is a much faster and fundamentally different game than standard TFT, using its statistics to analyze my standard TFT gameplay would throw off any analysis results in future steps.

Finally, I dropped all columns that I did not need for my analysis. The columns “Gold Left”, “Last Round”, “Level”, “Companion Skin ID”, “Companion Species”, “PUUID”, and “Companion Content ID” were dropped from the table. This was done to increase clarity and simplify the amount of information on the table.

After completing all of the cleaning and formatting, our dataset has a total of 13 columns and 197 rows.

*Example of cleaned Dataset*

Primary Statistics:

Over set 7, a total of 197 standard TFT games were played. These games were played from gold to diamond elo, with most games hovering around low to high plat ranking. Over my 197 games played, the distribution of placements was slightly skewed right, indicating that more top 4 finishes were acquired than bottom 4 finishes. With the most common placement being 2nd place in 32 games, followed by 4th place in 31 games, 3rd place in 27 games, and 5th place in 25 games, my gradual climb from gold to diamond can be seen within the data. However, when looking at the first and eighth place counts, I received eighth place 23 times while only getting first place 20 times.

*Placement Countplot*

Within those 197 games, a unique combination of traits were used to buff my team composition each game. Below is a countplot of the traits that I’ve used over set 7. Unsurprisingly, the most frequent trait used within my team comp, used in 119 of my games, was Dragon. As the Dragon trait was one of the main focal points and attractions of this set, it made sense that it was used in many of my games. Different traits such as Guild, used in 112 of my games, were easy to fit into my team composition due to its activation requirement of a single “guild” unit. On the other hand, there were several traits that were not often chosen by me due to their limited synergies with other traits. Traits such as Legend, which was only picked 7 times, forced you to place the same three units in your team composition, severely limiting the amount of flexibility that you were able to play with.

*Traits Countplot*

To help with visualizing which traits I’ve used the most, I’ve created a wordcloud of the above data. 

*Traits Wordcloud*

In addition to a unique combination of traits, a unique combination of three augments are chosen per game. For the first augment, I chose Item Grab Bag (Level 1) the most, for the second augment, I chose Thrill of the Hunt (Level 1) the most, and for the third augment, I chose Portable Forge the most. In combination over all augments, Portable Forge was picked the most.

*All augments countplot*

Data Dealt Analysis:

“In the case of my gameplay, does dealing more damage to other players correlate to a higher placement?”

To answer this question, I decided to move forward with a simple linear regression with “damage dealt to other players” as the independent variable and “placement” as the response variable. A scatterplot with a line of best fit was created in order to visualize the data.

*damage dealt scatterplot*

Before using this model, several assumptions had to be checked. To do so, a density histogram showing the distribution of residuals was created. Looking at the density histogram, we can see that the KDE of the residuals closely matches the orange normal KDE curve. This confirms we are able to use a linear regression with our data.

*residual plot*

The line of best fit was calculated to have a slope of -0.034 and an intercept of 7.77. Interpreting the slope tells us that as damage dealt to other players increases by one, the placement value will decrease on average by 0.034. The intercept tells us that assuming we deal 0 damage to other players in a game, we’ll place at an average of 7.77.

Looking at the scatterplot, there is a clear negative trend between placement and damage dealt to other players. This is further corroborated by calculating the correlation value of -0.838. Squaring this value provides us with a R-squared value of 0.702. As 70.2% of the variance in placement can be explained by the linear regression model created, we can confidently say that there is a strong correlation between the two variables. 

Conclusion:
Dealing more damage to other players has a strong negative correlation with placement value, telling me that as damage dealt increases, my placement value will decrease. 

Trait Analysis:

To guide my analysis of the traits that I used in my gameplay, these questions were formulated. Because I used my own data, the results that this analysis provides can only be applied to my own gameplay and cannot be extrapolated to other players.

Which traits should I be using to get a better placement?
Which combination of three traits works the best together?

*Insert Trait Performance bar charts*

The bar charts above show a clear depiction of my performance with different traits. Traits such as Spellthief, Legend, and Cavalier all have above average placements above the typical average placement of 4.5. These traits, as expected, have the lowest placements because of my unfamiliarity with the traits and the smaller amount of games that I used them in. However, several of the traits that I seldomly used such as Scalescorn, Astral, and Warrior had the lowest average placement as well as a higher top 4 and win percentage. All of the team compositions that use these traits are quite strong but harder to obtain at full power, explaining the higher success rate and low play rate. The complete table of trait statistics are shown below.

*Insert trait stats table*

One trait that surprised me was Dragonmancer. With an average placement slightly above the typical average placement of 4.5, a top 4 percentage of 0.48, and win percentage of 0.08, the trait did not perform well. Throughout the set I had perceived Dragonmancers as quite strong, but looking at the data again it seems as though it is on the weaker end.

*insert combo trait stats table*

The table above was created by iterating through all unique combinations of three traits. Unique combinations of traits that I did not play in the 200 games in my dataset were dropped to ensure consistency. Trait combinations that had less than 15 games together were also dropped to guarantee the combination statistics wouldn’t be skewed as much by an outlier game due to the larger sample size.

The top three trait combinations were:
Combination 1: Guild, Astral, Bruiser (Average Placement of 3.0)
Combination 2: Dragon, Jade, Ragewing (Average Placement of 3.25)
Combination 3: Bard, Guild, Bruiser (Average Placement of 3.25)

Combinations 1 and 3 were as expected, as the traits that were in those combinations had low average placements, high top 4 percentages, and high win rates separately. However, the combination of Dragon, Jade, and Ragewing was unexpected. By themselves, they all had an average placement of above 4, a top 4 percentage of 60% and below, and a win rate percentage of 12% and below. Together however, the average placement jumped up to a value of 3.25, a top 4 percentage of 68.75% and a win percentage of 25%. These differences can most likely be attributed to the synergies between the three traits. Looking at this data, I’ll be sure to be playing a combination of Dragon, Jade, and Ragewing more frequently!


Augment Analysis:

To guide my analysis of the augments that I used in my gameplay, these questions were formulated. Because I used my own data, the results that this analysis provides can only be applied to my own gameplay and cannot be extrapolated to other players. Augments that had less than 5 games played were removed from the dataset in order to ensure that each augment had a large enough sample size and would not be skewed by an outlier.

Which augments should I be using to get a better placement?


*Insert Trait Performance bar charts*

The bar charts above show a clear depiction of my performance with different augments. The augments True Twos, Hot Shot, Celestial Blessing 1, and Sunfire Board have the highest average placement out of all the augments, with average placements of around 3. All the aforementioned augments have significant early game impact and can give you an advantage within the first few rounds that leads into future wins. Sunfire Board not only had a high top 4 rate, but also had the highest win rate out of all the augments chosen. It provides value throughout the entire game by debuffing the enemy team by a percentage of their health. Augments that were taken frequently such as Component Grab Bag, Portable Forge, and Item Grab Bag 1 all had a decent average placement of around 3.5. These augments all provide items or item components when taken, also providing my units with an immediate boost in power. This data further enforces the idea that I typically end up with a higher placement when having a stronger early game and should look for these types of augments when playing in the future. The complete table of trait statistics are shown below.

*Insert augment stats table*

One thing I noticed is that True Twos, and Grand Gambler have a 100% top 4 rate while having a 0% win rate. This is most likely due to its strength in the early game, allowing me to keep healthy enough to maintain a top 4 placement. However, once the top four players are left in the late-game, these two augments cannot compete with other opponent’s augments that are much more effective. 

Challenger Comparative Dataset Analysis:

Data Collection:

To collect the data for the challenger player dataset, I utilized Riot Games’s API to query the necessary information needed to conduct my analysis. This dataset had a total of 1000 games of TFT that the rank 1 player played during set 7, standard and hyper roll modes included. Here is a sample of the raw dataset that I queried.

*Example of raw dataset*

There are a total of 1000 rows and 17 columns in the dataset, making up all the data queried from the Riot API. Several of these columns will not be included in the final cleaned dataset.

*Dataset Column Descriptions*

Data Formatting & Cleaning:

The data formatting & cleaning completed for the challenger dataset analysis was the same process completed for the “Equinnax” dataset. Please refer back to the initial data formatting & cleaning section for more detail.

After completing all of the cleaning and formatting, our challenger dataset has a total of 13 columns and 961 rows.

*Example of cleaned Dataset*

Primary Statistics:

As of 8/10/2022, a total of 961 standard set 7 TFT games were played by “k3 c9soju”, the rank 1 player at the time. These games were played from diamond to challenger elo, with a large majority of games consisting of challenger level players and lobbies. Looking at the placement countplot for these 961 games, the distribution is greatly skewed towards the right, indicating that there were much more top four finishes than bottom four finishes. With the most common placement being 1st in 174 games, followed by 3rd in 145 games, 2nd in 142 games, and 4th in 122 games, the consistency in gameplay is clearly shown as the four highest placements are the four most frequent placements. These results were expected of the rank 1 player, as reaching rank 1 by itself requires a large number of top 4 finishes, in addition to the large number of the top 4 finishes needed to maintain the rank 1 status.

* Challenger Placement Countplot*

Within those 961 games, k3 c9soju utilized a combination of traits shown on the countplot below. The top three most utilized traits in his team compositions were guild, followed by dragon and bruiser. 

*Challenger Traits Countplot*

To help with visualizing which traits I’ve used the most, I’ve created a wordcloud of the above data. 

*Challenger traits Wordcloud*

In addition to the combination of traits that was used, three different augments were chosen every game. For the first augment, k3 c9 soju chose Portable Forge the most, for the second augment, he chose Weakspot the most, and for the third augment, he chose Celestial Blessing 2 the most. Across all augments, Second Wind 2 was picked the most. 

*Challenger all augments countplot*

Comparison of Primary Stats:

*Insert Comparison of Trait Usage Distribution Table*

His top three most used traits were also the top three traits used in my own gameplay. These traits are easy to implement on the board or are one of the main attractions of set 7, leading to an increase in usage. However, the next two traits were different. In the k3 c9soju’s games, the traits Tempest and Bard were used and in my own games, the traits Jade and Shapeshifter were used. The Tempest and Bard traits are much more utility and late-game oriented than Jade and Shapeshifter, which leads to a much stronger late-game board. 

The largest difference between the augments chosen is that k3soju frequently picks “combat” augments that can be used throughout the entire game, rather than augments that give your team an immediate burst of strength and aren’t as useful in later stages. Weakspot, Celestial Blessing 2, and Second Wind 2 all buff your team or debuff enemy teams by a percentage rather than a flat amount, making it strong throughout the entire game.

Looking to use traits and augments that scale better into the late game are the largest difference in my games and his games. We’ll keep this info in mind as we take a deeper look into traits and augment statistics.

Challenger Trait Analysis:

*Insert Trait Performance bar charts*

The bar charts above show a clear depiction of k3 c9soju’s performance with different traits. Nearly every trait had an average placement of below the typical average placement of 4.5. The only exception was the Legend trait, with an average placement of 5.20, a top 4 percentage of 0.4, and a win percentage of 0. These results are most likely due to the fact that Legend was played in a mere 5 out of 961 games that he played during set 7, with the 2nd least played trait being played in 75 games. This unfamilarity and inexperience with the trait combined with a small sample size explains the significantly higher placement results.

On the other hand, traits such as Starcaller, SpellThief, and Bard had several of the lowest average placements, highest top 4 percentages, and highest win percentages. All the units attributed with these traits are legendary units with strong skills that can typically be found much later in the game. Once obtained, fielding these units and activating their traits gives your team a large boost in strength.

*Insert challenger trait stats table*

See the above table for the stats for all traits.

*insert challenger combo trait stats table*

The table above was created by iterating through all unique combinations of three traits. Unique combinations of traits that k3 c9soju did not play in the 200 games in my dataset were dropped to ensure consistency. Trait combinations that had less than 25 games together were also dropped to guarantee the combination statistics wouldn’t be skewed as much by an outlier game due to the larger sample size.

The top three trait combinations were:
Combination 1: Bard, Tempest, SpellThief (Average Placement of 1.703)
Combination 2: Tempest, Bruiser, SpellThief (Average Placement of 1.833)
Combination 3: Guild, Tempest, Starcaller (Average Placement of 1.923)

Traits that were activated by legendary units such as Bard, SpellThief, and Starcaller were in each of the top three combinations, with the best combination containing two of those traits.  Combining these legendary activated traits with other decently performing traits such as tempest, guild, and bruiser drastically increased the average placement of the combination. This jump in placement can be most likely attributed to the strength of these legendary traits and synergy with optimal supporting traits.

Comparison of Traits:

*insert comparison of legendary trait stats table*

When looking at the top three trait combinations of k3 c9soju, traits activated by legendary units were in all of the combinations. My combinations only had a single legendary activated trait, “Bard”, in the third combination. The average placements of k3 c9soju’s combinations were all below 2.00, whereas the top three trait combinations of my data had a minimum average placement of 3.00. k3 c9soju’s data clearly shows that the traits activated by legendary units will give a higher placement when used in a team composition, but my data does not. We’ll look deeper into each of these traits (Bard, Starcaller, SpellThief) to find out why.

When comparing the data, traits such as Bard, Starcaller, and SpellThief had a sizable difference in stats. My Bard’s average placement had a 3.74 compared to his 3.21, my Starcaller’s average placement had a 4.00 average placement compared to his 3.05, and my SpellThief’s average placement had a 5.50 compared to his 3.13. k3 c9soju’s win percentage for these traits were high while mine were quite low, but his top 4 percentages for Bard and Starcaller when compared to mine were relatively similar. SpellThief was quite different, but it was an outlier trait when compared to the rest of my traits. This indicates a discrepancy within my gameplay between getting a top four position and winning when using those traits.

This discrepancy can be attributed to a weak late game. Typically, these traits are activated in the mid to late game when there are around four to five players left. Maintaining a stronger late game increases the speed at which you can find one of these legendary units, upgrade them, and activate the trait. If your late game isn’t as strong, it’ll be tougher to find these units and you’ll be quickly knocked out by other opponents that find the units and activate the trait faster than you. 

Looking at the data, it tells me that I need to maintain a stronger late game in order to find, upgrade, and activate the legendary units and traits quicker. I often manage to get to a top 4 position with those legendary traits active, but am unable to transfer that top four position into a win.

Challenger Augment Analysis:

*Insert challenger Augment Performance bar charts*

The bar charts above show a clear depiction of k3soju’s performance with different augments. Augments that had less than 20 games played were removed from the dataset in order to ensure that each augment had a large enough sample size and would not be skewed by an outlier. The augments with the highest average placement were Assasin Emblem, Makeshift Armor 2, Celestial Blessing 3, Gadget Expert, and Titanic Strength. Assassin Emblem and Makeshift Armor 2 are niche augments that fit very well into several team compositions in the right scenario, inflating their average placement, top 4, and win percentages. Celestial Blessing 3 provides percentage healing for the entire team, Gadget Expert increases damage dealt by direct damage items by 40%, and Titanic strength provides units with the Bruiser trait a percentage increase in attack damage based on health. These three augments deal with percentages, ensuring that they provide decent value in the early game while scaling well into the late game. The complete table of trait statistics are shown below.

*Insert challenger augment stats table*

One augment that surprised me was Second Wind 2, which I perceived as quite good, but only ended up with a respective 4.18 average placement. Looking at its standard deviation of 2.30 and its pick rate of 126 out of 961 games, the augment seems quite volatile, doing well in some games and not so great in others. Augments like these may require further analysis into which traits/team compositions they fit the best in.

Comparison of Augments:

The main difference between the choices between k3 c9soju’s augments and mine are scalability. Most of the augments that I like to choose give me a high top 4 percentage, but don’t convert to a win. On the other hand, most of the augments that he chooses and does well with both have a high top 4 percentage and a decent win percentage. Augments that deal with percentages such as Gadget Expert are generally more scalable than augments that give immediate spikes in strength such as True Twos and Item Grab Bag 1. Picking and choosing those types of augments will greatly help in increasing average placement and win percentage.

Conclusion:

There are several main takeaways from this case study that I can use to improve my own gameplay after analyzing my own gameplay and comparing it to the rank 1 player:

Using earlier game traits are okay in the early to mid game, but try your best to change your team composition in the late game to more utility based traits such as tempest and bard unless your team composition is set in stone.
Don’t sack the entire late game in order to get an advantage in the early game, think of the entire match holistically.
Try to transition your mid game team composition into your late game team composition by implementing legendary and supporting units that provide strong and synergistic traits.
Make sure to pick augments that are decent in the early game and scale into the late game in order to not fall behind other players that do the same.

Future Steps:

There are many different things that can be done to further expand on this Case Study in the future, mainly increasing the amount of data in order to get more holistic results and exploring different relationships between aspects of the game. Utilizing the Riot API to extract data was quite successful, albeit quite slow. Finding workarounds to call data faster would allow me to compare my games to the top 300 players in the NA servers instead of just the top player.

Furthermore, expanding on the trait-augment relationship would also be interesting, allowing us to find out which augments are the most optimal for specific team compositions. 

Looking forward, I plan to try and hit the master tier with all the insights that I gleaned from this case study. Analyzing my own gameplay and comparing it to the top player allowed me to really understand what I needed to fix and correct.

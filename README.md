# crypto_clusters

## Preprocessing
Crypto currency data started with a 1252 x 7 dataframe and was prepared for analysis as follows:
  1. currencies that were not being actively traded were removed from the df (df.shape = 1144 x 7)
  2. 'IsTrading' column dropped (df.shape = 1144 x 6)
  3. columns that contained any missing values were dropped (df.shape = 685 x 6)
  4. data were filtered to keep only rows where the 'TotalCoinsMined' > 0 (df.shape = 532 x 6)
  5. 'CoinName' was dropped (df.shape = 532 x 5)
  6. 'Algorithm' & 'ProofType' columns were investigated for unique values & possible synonymous values
  7. 71 unique values appeared in 'Algorithms' all appeared to be different techniques albeit many were clearly related
  8. 25 unique values appeared in 'ProofType' and produced 3 pairs of values that needed to be equated: 'DPOS' V 'DPoS', 'PoS' v "Pos', & 'PoA' v 'Power of Authority'
  9. .str.lower() was used on 'ProofType' which fixed the first 2 identified pairs
  10. .replace({'proof of authority': "poa"}) was used to fix the final pair
  11. 22 unique values remained in 'ProofType'
  12. pd.get_dummies was used to convert the 'ProofType' & 'Algorithm' columns into binary columns (df.shape = 532 x 96)
  13. 'Unnamed: 0' column (which seemed to be an alternate name column for the currency) was dropped prior to scaling (df.shape = 532 x 95)
  14. StandardScaler was used to normalize the data to z-scores ranging from -1 to +1


## Dimensional Reduction
PCA(n_components=.90) was specified so 90% of variance would be accounted for by the model
* this resulted in a new dataframe (df.shape = 532 x 74)

t-SNE was used & the data was reduced to 2 factors (df.shape = 532 x 2)

![t-SNE results](/t_SNE_04Oct21.png)

#### Q: Are there distinct clusters in the t-SNE scatterplot?
* A: There seems to be 3 very distinct clusters [at approx. (-10, 10), (0, -19), and (40, -10)]. There are a number of smaller clusters throughout where multiple currencies are stacked on top of each other (as can be seen in the areas with the darkest colors). One could maybe argue there is a cluster around (8, 8), but really, that seems like several distinct clusters near each other more than actually being a single group.

## Cluster Analysis with k-Means
KMeans analysis was used to test how many clusters could reasonably be expected from the data
![k-Means elbow](/elbow_04Oct21.png)

## Recommendation
I would say the currencies have 4 obvious clusters based on the 2d plot (though there seem to be smaller clusters). Being able to plot in additional dimensions might suggest slightly different results. KMeans elbow plot concurs with the suggestion of 4 distinct clusters in the data. It would be interesting to see if some of the smaller clusters (where a number of values seem to be stacked in very specific locations) have closely related algorithms--if so, that could be an argument to make some of those equivalent groups earlier in the data cleaning process.




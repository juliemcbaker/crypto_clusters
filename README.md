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


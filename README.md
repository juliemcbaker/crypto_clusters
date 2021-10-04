# crypto_clusters

## Preprocessing
Crypto currency data started with a 1252 x 7 dataframe and was prepared for analysis as follows:
  1. currencies that were not being actively traded were removed from the df (df.shape = 1144 x 7)
  2. 'IsTrading' column dropped (df.shape = 1144 x 6)
  3. columns that contained any missing values were dropped (df.shape = 685 x 6)
  4. data were filtered to keep only rows where the 'TotalCoinsMined' > 0 (df.shape = 532 x 6)
  5. 'CoinName' was dropped (df.shape = 532 x 5)
  6. pd.get_dummies was used to convert the 'ProofType' & 'Algorithm' columns into binary columns (df.shape = 532 x 99)
  7.  

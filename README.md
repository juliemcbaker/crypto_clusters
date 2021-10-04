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
  8. 25 unique values appeared in 'ProofType' and produced 3 pairs of values that needed to be equated: 

    
  
  9. pd.get_dummies was used to convert the 'ProofType' & 'Algorithm' columns into binary columns (df.shape = 532 x 99)
  10.  
    | Term 1 | Term 2 | Solution |
    |--------|--------|----------|
    | 'DPOS' | 'DPoS' | .str.lower() |
    | 'PoS' | 'Pos' | .str.lower() |
    | 'PoA' | 'Power of Authority' | .replace({'proof of authority': "poa"}) | 

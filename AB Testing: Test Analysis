import scipy.stats as scs
import pandas as pd

#Returns the minimum sample size to set up a split test
def min_sample_size(bcr, mde, power=0.8, sig_level=0.05):
    standard_norm = scs.norm(0, 1)
    Z_beta = standard_norm.ppf(power)
    Z_alpha = standard_norm.ppf(1-sig_level/2)
    
    pooled_prob = (bcr + (bcr*(1+mde))) / 2
    
    sample_size = (2 * pooled_prob * (1 - pooled_prob) * (Z_beta + Z_alpha)**2
                 / ((bcr*(1+mde))-bcr)**2)

    return int(sample_size)


#First Line is Control: Trials (total number of visits), Success(number of visits whom reached the desired goal)
#Second line is Variations: Trials (total number of visits), Success(number of visits whom reached the desired goal)

results = [ (23884, 2342) ,
            (35467, 5675)  ]
df = pd.DataFrame(results, columns = ['trials' , 'success'], index=['Control', 'Variation'])



## Statistical Testing of experiences loop

import pandas as pd
import numpy as np
from scipy.stats import chisquare
from scipy.stats import chi2_contingency
from scipy.stats import chi2
from scipy.stats import binom

#set conditions beneath
alpha = 0.05
variations=2
avg_visits_per_week= 186000


#Analysis Loop

def analyse(df):
    df["failures"] = df["trials"]-df["success"]
    df["conversion"] = df["success"]/df["trials"]
    df["diff"] = df["conversion"] - df["conversion"].loc["Control"]
    df["real_diff"] = df["diff"] / df["conversion"].loc["Control"]
    df["sample_size"]= min_sample_size((df["success"].iloc[0]/df["trials"].iloc[0]),0.1,power=0.8,sig_level=alpha)
    df["P-Value"]="N/A"
    df["H0_result"]="N/A"
    df["TP/TN"]="N/A"
    df["CI"] = binom.interval(alpha,df["trials"], (df["success"]/df["trials"]))
    SF=df.iloc[:,[1,2]]
    print(SF)
    CS = chi2_contingency(SF)
    print(CS)
    
    Test_Duration = sum(df["sample_size"])/avg_visits_per_week
    print(Test_Duration)
    if sum(df["trials"]) > sum(df["sample_size"]):
        df.loc["Variation","P-Value"]=CS[1]     
    else:
        print('Trials not reached minimum')
    if df.loc["Variation","P-Value"]< alpha:
        df.loc["Variation","H0_result"]="Reject H0"
    else:
        df.loc["Variation","H0_result"]= "Do not Reject H0"
    if df.loc["Variation","H0_result"]== "Reject H0" and df.loc["Variation","real_diff"] > 0:
        df.loc["Variation","TP/TN"]= "TP"
    elif df.loc["Variation","H0_result"]== "Reject H0" and df.loc["Variation","real_diff"] < 0:
        df.loc["Variation","TP/TN"]= "TN"
    else:
        df.loc["Variation","TP/TN"]= "N/A"
    print(df)
    print('\n\n')
    Test_Duration = sum(df["sample_size"])/avg_visits_per_week
    
analyse(df)

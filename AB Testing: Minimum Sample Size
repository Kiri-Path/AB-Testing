# Sample size calculator
# The sample size will determine how long we will leave the test to run for
# The mde is the minimum diffrence between the control and test and will determine whether it is worthwhile invesment

#Enter the average number of visits to the starting point of the test.
#for example if we are testing conversion of checkout journey, we want the average number of visits who start the checkout.
avg_visits_per_week= 34815 

import scipy.stats as scs
import pandas as pd

#bcr=base conversion rate, mde= minimum detectable effect, power = probability of not making type 2 error, sig_level = alpha)
#industry standard for power is 80% and alpha is 5%

def min_sample_size(bcr, mde_list, power=0.8, sig_level=0.05):

    # standard normal distribution to determine z-values
    standard_norm = scs.norm(0, 1)

    # find Z_beta from power
    Z_beta = standard_norm.ppf(power)

    # find Z_alpha as 2 tail 
    Z_alpha = standard_norm.ppf(1-sig_level/2)
    
    sample_size_list = []
    bcr_list = []
    newcr_list = []
    for mde in mde_list:
        # average of probabilities from both groups
        pooled_prob = (bcr + (bcr*(1+mde))) / 2

        # formula to calculate sample size for given mde
        sample_size = (2 * pooled_prob * (1 - pooled_prob) * (Z_beta + Z_alpha)**2
                 / ((bcr*(1+mde))-bcr)**2)
        sample_size_list.append(int(sample_size))
        bcr_list.append(bcr)
        newcr= bcr* (1+mde)
        newcr_list.append(newcr)

    df = pd.DataFrame([bcr_list,newcr_list,mde_list,sample_size_list]).transpose()
    df.columns = ['BCR','New CR','MDE', 'Sample']
    df[['BCR','New CR','MDE']]=(100. * df[['BCR','New CR','MDE']]).round(2).astype(str) + '%'
    df["Test Duration (weeks)"] = df["Sample"]*3/avg_visits_per_week  
    return df

min_sample_size(0.02,[0.01,0.05,0.1,0.2,0.25,0.3,0.5,1],power=0.8,sig_level=0.05)  



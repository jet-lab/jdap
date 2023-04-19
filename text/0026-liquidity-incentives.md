# Incentive Program Overview: 

The following sections detail the specifics and operations of this incentive program.


## Parameters


### Timeline - Liquidity Mining



* The program will run for a total of 4 years. For the purpose of distributing rewards as epochs, the program uses 2,116,800 minutes as max time (adding 9 additional days to the program past 4 years). 
  * t<sub>max </sub>= 2,116,800
* The start date of the program will occur when Jet Fixed-term Lending Markets are deployed on Solana Mainnet
    * t<sub>0</sub> = tbd
    * The program will distribute rewards in epochs that span 30 days (or 43,200 minutes)
        * t<sub>epoch</sub> = 43,800 
        * epoch<sub>max </sub>= 49

### Timeline - Retroactive Governance Rewards

* A one time, retroactive airdrop will be made to users that participated in Asset Onboarding proposals. The airdrop is based on the following dates:
     * Asset Onboarding Proposals prior to 2023-04-30
        * Estimate: 19 proposals

     * Rewards distributed on: 2023-06-01
     * Rewards must be claimed by: 2023-08-30

### Funds 

* 137,700,946 JET tokens from the DAO treasury
     * 67,050,473 JET to providers acting as lenders
     * 67,050,473 JET to providers acting as borrowers
     * 3,600,000 JET to governance participants


## Logic


### Required Action - Liquidity mining 



* A user acts as a lender or borrower in Jet Fixed-term Markets, with their user liquidity score exceeding 0.25% of the total liquidity score for a given epoch.  

### Reward - Liquidity Mining

```
// Score for each open order

let open_order_score = order_size * exp(-abs(order_interest_rate - mid_market_rate) / mid_market_rate)

// Sum all the open order scores for the minute sample

let q_sample = sum(open_order_scores)

// Scale the sampled score for open orders based on the market tenor, biased towards longer tenors

let q_scaled = q_sample * (1 + sqrt(market_tenor_days) / 30)

// Get the final score for a user in the 30-day epoch by summing all the sampled scores during that period

let q_score = sum(q_scaled)
```

* Rewards must be claimed within 90 days of the epoch pay-out, or funds will be returned to the JetDAO treasury.
* In the case that a market only has liquidity on one side, the mid_market_rate will be defined as the best bid (ask) divided (multiplied) by two.

### Required Action - Retroactive Governance Airdrop

* A user historically has voted in Asset Onboarding proposals in JetDAO Governance prior to 2023-04-30, where their voting threshold is above 1000.

### Reward - Retroactive Governance Airdrop

```
// Get the user score by summing the recorded vote weights and adjusting by the amount of proposals

// the user participated in relative to the total number of proposals voted on.

let user_score = sum(casted_vote_weight ^ (1 / 3)) * user_vote_count / total_proposal_count
```


* Rewards distributed on: 
    * 2023-06-01
* Rewards must be claimed by: 
    * 2023-08-30


### Incentive Success

A successful outcome of this incentive program is defined as: 
* Average liquidity of $250K within 300 basis points on each side of every market.

## Implementation 

### Communication



* A forum post will be published announcing the start date of the incentive 3 days in advance of the rewards starting.

### Funding Source

* Funding for this incentive will be provided by the JetDAO Treasury.

## Technology

* On-chain data and tools will be used to determine user rewards.
* All rewards are distributed via the Jet Governance airdrop system.


## Operations 


### Participation Verification 



* Verification will be completed using on-chain data.
* All information is publicly available and can be verified independently using on-chain tools.

### Reporting

* A forum post will be published announcing the distribution of rewards for each epoch of the program, notifying users to claim their rewards within the 90 day window. 

## Technology 

* The Jet Governance system will distribute rewards. 


## Depreciation


### Communication 



* A forum post will be made at the start of the final rewards program epoch signaling the end of the program. 
* A forum post will be made 60 days after the end of the final rewards program epoch informing users that they have 30 days left to claim their final rewards. 

### Funding 

* All funds that were unclaimed during the life of the program will be returned to the JetDAO treasury.

### Technology 

* The incentive program will automatically conclude at the predetermined date. No further actions are required. 

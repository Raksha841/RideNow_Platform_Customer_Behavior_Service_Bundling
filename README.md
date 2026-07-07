# RideNow Platform: Customer Behavior & Service Bundling

Market basket analysis (Apriori algorithm) uncovering how customers combine ride types, add-ons, and subscription services within a session used to design cross-service bundles and improve retention for a multi-service mobility platform.

## Business Context

RideNow is a multi-service mobility platform offering ride options (Economy, Premium, Shared), add-on services (Extra Luggage), adjacent services (Food Delivery, Grocery), and a subscription plan (RidePass). As Product Manager, the goal is to understand how customers combine services within a session in order to improve cross-service usage, design bundles, and increase retention.

## Dataset

Each row represents a single user session; all columns are binary (1 = used, 0 = not used):

| Column | Description |
|---|---|
| EconomyRide, PremiumRide, SharedRide | Ride type used |
| FoodDelivery, Grocery | Adjacent services |
| RidePass | Subscription indicator |
| AirportRide | Airport-related trip |
| LateNight | Usage between ~10pm–5am |
| ExtraLuggage | Add-on service |

## Methodology

1. **Item frequency analysis**: measured how often each service appears across all sessions to identify the most-used services.
2. **Hypothesis formation** : predicted relationships (e.g., RidePass subscribers cross-using adjacent services, LateNight sessions favoring Premium) before generating rules, to avoid pattern-matching bias.
3. **Frequent itemset mining (Apriori)**: generated frequent itemsets at a minimum support of 0.10.
4. **Association rule mining**: derived rules at a minimum confidence of 0.40, then ranked by confidence and lift.
5. **Rule interpretation & business translation**: converted top rules into behavioral narratives and concrete product actions.
6. **Critical evaluation**: identified and rejected a rule with perfect confidence but low incremental value, and compared high-confidence vs. high-lift rules to decide which is more trustworthy for product decisions.

## Key Findings

- **PremiumRide** is the most-used service (~45% of sessions), followed by **FoodDelivery** (~38%) and **ExtraLuggage** (~37%).
- **AirportRide → ExtraLuggage** (confidence 0.71, lift 1.92): airport travelers reliably add extra luggage — a strong candidate for a dynamic add-on prompt.
- **RidePass → FoodDelivery** (lift ~2.04, confidence ~77%): RidePass subscribers are twice as likely to order food delivery — a clear cross-sell opportunity for the subscription tier.
- **AirportRide → PremiumRide** (confidence 1.0, lift 2.23) was **rejected** as a business action despite perfect metrics, since the relationship reflects a saturated/structural constraint (all airport rides are already Premium) rather than an actionable, incremental behavior.
- **LateNight → PremiumRide** (lift ~0.95) shows confidence without incremental value — a reminder that lift, not confidence alone, should drive investment decisions.

## Business Recommendations

| Strategic Pillar | Actionable Initiative | Primary Goal |
|---|---|---|
| High-Value Travel | One-tap "Extra Luggage" prompt for airport-bound Premium rides | Increase Average Order Value |
| Subscription Growth | Bundle Food Delivery perks into the RidePass subscription tier | Increase Customer Lifetime Value |

## Tools & Libraries

- Python (pandas, numpy)
- mlxtend (`apriori`, `association_rules`)
- matplotlib

## Repository Contents

- `RideNow_Platform_Customer_Behavior_Service_Bundling.ipynb`: full analysis notebook (EDA, Apriori, rule mining, interpretation, business recommendations)
- `uber_arm_dataset.csv`: session-level dataset used in the analysis
- `requirements.txt`: Python dependencies

## Author

Raksha Chabhadia, 
MBA Business Analytics

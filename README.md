# Will the Customer Accept the Coupon?

### Problem Statement

This analysis explores what factors influence whether drivers accept location-based coupons delivered to their mobile devices while driving. Using data from a survey conducted on Amazon Mechanical Turk, I investigate patterns in coupon acceptance across different coupon types, with deep-dive analyses into bar coupons and coffee house coupons.

The goal is to identify which customer segments are most likely to accept coupons, under what circumstances they'll accept them, and what contextual factors (time, weather, passengers, etc.) impact acceptance rates. Understanding these patterns can help businesses optimize coupon distribution strategies to maximize acceptance rates and minimize wasted marketing spend.

### Data Cleaning

The dataset contains missing values in several columns: `car` (12,576 missing), `Bar` (107 missing), `CoffeeHouse` (217 missing), `CarryAway` (151 missing), `RestaurantLessThan20` (130 missing), and `Restaurant20To50` (189 missing).

The `car` column has 99% missing data and appears to have been collected inconsistently. Due to the lack of data and consistency issues, I decided to drop the `car` column entirely.

For the other columns with missing data (Bar, CoffeeHouse, CarryAway, RestaurantLessThan20, Restaurant20To50), the missing values represent only a small fraction of the data. Since these columns have 'never' as a possible value and respondents likely skipped questions that didn't apply to them, I dropped rows with missing values in these columns. This resulted in retaining 95.23% of the data (12,079 out of 12,684 rows).

### Analysis

The overall coupon acceptance rate across all coupon types is **56.93%**. However, acceptance rates vary significantly by coupon type:

- Coffee House: 49.63%
- Restaurant(<20): Data shows similar patterns
- Carry out & Take away: Similar patterns
- Bar: 41.19% (significantly below average)
- Restaurant(20-50): Analyzed separately

This analysis focuses on two distinct coupon types with different behavioral patterns: **Bar coupons** and **Coffee House coupons**.

#### Bar Coupon Analysis

Bar coupons show the lowest acceptance rate (41.19%) among all coupon types. I conducted multiple segmentation analyses to understand who accepts bar coupons:

**Key Findings:**

1. **Frequency is the strongest predictor**: Drivers who visit bars more than 3 times per month have a 76.17% acceptance rate versus 37.27% for infrequent visitors (38.90% difference).

2. **Passenger type matters dramatically**: Having children in the car reduces acceptance significantly. Drivers who visit bars >1/month without kids show 70.94% acceptance versus 29.79% for others (41.15% difference).

3. **Age and lifestyle factors**: Drivers over 25 who visit bars >1/month show 68.98% acceptance versus 33.77% for others (35.21% difference).

4. **Combined targeting criteria**: When combining multiple favorable conditions (frequent bar-goers + no kids + not widowed) OR (frequent bar-goers + under 30) OR (frequent cheap restaurant diners + income <$50K), the acceptance rate reaches 58.71% versus 29.99% for others (28.72% difference).

#### Coffee House Coupon Analysis

Coffee house coupons perform better than bar coupons (49.63% vs 41.19%) and show different behavioral patterns:

**Key Findings:**

1. **Time of day is critical**: Morning times (7AM, 10AM) show 53.64% acceptance versus 46.31% for other times. The 10AM time slot peaks at 63.48% acceptance, while 6PM drops to 41.23%.

2. **Expiration time matters**: 1-day expiration shows 58.06% acceptance versus 42.91% for 2-hour expiration (15.15% difference). Coffee drinkers prefer flexibility.

3. **Frequency still matters but less dramatically**: Frequent visitors (>3/month) have 67.26% acceptance versus 44.59% for infrequent visitors (22.67% difference) - smaller than the 38.90% seen with bars.

4. **Social context**: Being with friends (59.74%) or partner (56.70%) increases acceptance versus being alone (43.39%). Unlike bars, having kids (47.15%) doesn't dramatically reduce acceptance.

5. **Income**: Lower income individuals (<$50K) show slightly higher acceptance (52.28% vs 46.60%).

### Results

#### Bar Coupons - Positive Acceptance Drivers:

- **Visit frequency >3 times/month**: 76.17% acceptance (strongest predictor)
- **No children as passengers + frequent visitors**: 70.94% acceptance
- **Over age 25 + frequent visitors**: 68.98% acceptance
- **Multiple favorable conditions combined**: 58.71% acceptance

**Distribution Strategy**: Target frequent bar-goers (though they represent only 10% of recipients). Avoid distributing when kids are passengers. Focus on drivers over 25 in social situations.

#### Coffee House Coupons - Positive Acceptance Drivers:

- **10AM time slot**: 63.48% acceptance (optimal coffee time)
- **Frequent visitors (>3/month)**: 67.26% acceptance
- **With friends**: 59.74% acceptance
- **1-day expiration**: 58.06% acceptance
- **Morning times (7AM, 10AM)**: 53.64% acceptance

**Distribution Strategy**: Prioritize morning hours, especially 10AM. Target social contexts (friends, partners). Use 1-day expiration for flexibility. Coffee has broader appeal than bars.

#### Key Differences Between Bar and Coffee Coupons:

1. **Time sensitivity**: Coffee shows strong morning preference; bars less time-dependent
2. **Passenger impact**: Kids block bar coupons but not coffee coupons
3. **Frequency impact**: Bars show extreme segmentation (38.90% difference); coffee more moderate (22.67%)
4. **Overall acceptance**: Coffee performs 8.44% better than bars (49.63% vs 41.19%)
5. **Target audience size**: Coffee has broader appeal with more frequent visitors (849 vs 193)

#### Factors Negatively Correlated with Acceptance:

**For both coupon types:**

- Infrequent establishment visits
- 2-hour expiration (especially for coffee)
- Being alone (reduces acceptance relative to social contexts)

**Bar-specific negatives:**

- Having children as passengers (dramatic reduction)
- Infrequent bar visits (only 37.27% acceptance)

**Coffee-specific negatives:**

- Evening times (6PM: 41.23%, 10PM: 42.91%)
- 2-hour expiration (42.91% vs 58.06% for 1-day)

### Next Steps

1. **Validate findings with experimental coupon distribution**: Test the identified high-value segments in real-world campaigns to confirm acceptance patterns.

2. **Cost-benefit analysis**: Determine optimal balance between reach and acceptance rate for each coupon type. Bar coupons have narrow but high-yield targets; coffee coupons can cast a wider net.

3. **Expand analysis to other coupon types**: Apply similar segmentation methodology to Restaurant(<20), Restaurant(20-50), and Carry out & Take away coupons.

4. **Geospatial analysis**: Incorporate location data (direction_same, distance indicators) to understand how proximity affects acceptance.

5. **Seasonal patterns**: Explore whether weather (sunny/rainy/snowy) and temperature interact with coupon type differently.

6. **Multi-factor optimization**: Use machine learning to identify optimal combinations of factors that maximize acceptance while maintaining reasonable reach.

---

## Technical Details

### Repository Structure

- `prompt.ipynb` — Main Jupyter notebook containing all analysis code and visualizations
- `data/coupons.csv` — UCI ML dataset (12,684 rows, 26 columns)
- `README.md` — This file

### Prerequisites

- Python 3.9+
- Required packages: `pandas`, `numpy`, `matplotlib`, `seaborn`, `jupyter`

### Running the Analysis

```bash
# Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# Launch Jupyter
jupyter notebook

# Open prompt.ipynb and run cells sequentially
```

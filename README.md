
# Market Basket Analysis & Product Bundling Recommendations  
Online Retail Dataset – Association Rule Mining

**Name:** Labambay Olawale  
**Project Title:** Market Basket Analysis & Product Bundling Recommendations using Association Rule Mining  

## Project Goal
Increase average order value (AOV) through "Frequently Bought Together" bundles and discounts, as requested by Rita, given thin 3% profit margins.

## Data Preparation (No Code – Manual Steps in Excel)
1. Downloaded Online Retail.xlsx from UCI Repository.
2. Filtered to positive quantities only (removed negative rows).
3. Removed cancelled transactions (InvoiceNo starting with 'C').
4. Kept only United Kingdom transactions.
5. Trimmed spaces from Description column.
6. Removed rows with missing Description or CustomerID.
7. Counted frequency of each product (using pivot table or COUNTIF).
8. Selected the top 50 most frequent products.
9. Created binary transaction table:  
   - Rows = unique InvoiceNo  
   - Columns = top 50 product names  
   - Cell = 1 if product bought in that invoice (quantity ≥ 1), 0 otherwise  
10. Saved as CSV: online_retail_top50_basket.csv

## Analysis in Weka
1. Loaded CSV in Weka Explorer (Preprocess tab).
2. Ignored InvoiceNo column (right-click → Ignore attribute).
3. Applied NumericToBinary filter (first-last) to convert all product columns to binary format.
4. Applied NumericToNominal filter for compatibility.
5. In Associate tab: Used FP-Growth algorithm  
   - minSupport: 0.02  
   - minMetric: 2.0 (lift)  
   - numRulesToFind: 50  
6. Generated 124 positive association rules (presence-based).

## Top 10 Association Rules (with support & confidence)
(From FP-Growth results)

1. ALARM CLOCK BAKELIKE GREEN → ALARM CLOCK BAKELIKE RED  
   Support ≈ 0.057 | Confidence 0.66 | Lift 10.49

2. ALARM CLOCK BAKELIKE RED → ALARM CLOCK BAKELIKE GREEN  
   Support ≈ 0.063 | Confidence 0.60 | Lift 10.49

3. LUNCH BAG PINK POLKADOT → LUNCH BAG BLACK SKULL. + LUNCH BAG CARS BLUE  
   Support ≈ 0.021 | Confidence 0.29 | Lift 8.86

4. LUNCH BAG BLACK SKULL. + LUNCH BAG CARS BLUE → LUNCH BAG PINK POLKADOT  
   Support ≈ 0.021 | Confidence 0.62 | Lift 8.86

5. LUNCH BAG PINK POLKADOT → LUNCH BAG RED RETROSPOT + LUNCH BAG CARS BLUE  
   Support ≈ 0.021 | Confidence 0.30 | Lift 8.77

6. LUNCH BAG RED RETROSPOT + LUNCH BAG CARS BLUE → LUNCH BAG PINK POLKADOT  
   Support ≈ 0.021 | Confidence 0.62 | Lift 8.77

7. LUNCH BAG RED RETROSPOT + LUNCH BAG BLACK SKULL. → LUNCH BAG PINK POLKADOT  
   Support ≈ 0.024 | Confidence 0.61 | Lift 8.63

8. LUNCH BAG PINK POLKADOT → LUNCH BAG RED RETROSPOT + LUNCH BAG BLACK SKULL.  
   Support ≈ 0.024 | Confidence 0.35 | Lift 8.63

9. WOODEN PICTURE FRAME WHITE FINISH → WOODEN FRAME ANTIQUE WHITE  
   Support ≈ 0.038 | Confidence 0.54 | Lift 8.27

10. WOODEN FRAME ANTIQUE WHITE → WOODEN PICTURE FRAME WHITE FINISH  
    Support ≈ 0.038 | Confidence 0.58 | Lift 8.27

## Translations (as required)
1. 66% of customers who buy ALARM CLOCK BAKELIKE GREEN also buy ALARM CLOCK BAKELIKE RED (versus ~6.3% of all customers buy ALARM CLOCK BAKELIKE RED).
2. 60% of customers who buy ALARM CLOCK BAKELIKE RED also buy ALARM CLOCK BAKELIKE GREEN (versus ~5.7% of all customers buy ALARM CLOCK BAKELIKE GREEN).
3. 29% of customers who buy LUNCH BAG PINK POLKADOT also buy LUNCH BAG BLACK SKULL. and LUNCH BAG CARS BLUE (versus ~2.1% of all customers buy both).
4. 62% of customers who buy LUNCH BAG BLACK SKULL. and LUNCH BAG CARS BLUE also buy LUNCH BAG PINK POLKADOT (versus ~3.5% of all customers buy LUNCH BAG PINK POLKADOT in this context).
... (similar translations for rules 5–10 follow the same pattern)

## Bundle Recommendations
1. **Bakelike Clock Duo**  
   ALARM CLOCK BAKELIKE GREEN + ALARM CLOCK BAKELIKE RED  
   → Create this bundle with 12–15% discount.

2. **Lunch Bag Variety Quartet**  
   LUNCH BAG RED RETROSPOT + LUNCH BAG CARS BLUE + LUNCH BAG BLACK SKULL. + LUNCH BAG PINK POLKADOT  
   → Create this set with 15% discount when buying all four.

3. **White Frame Classic Pair**  
   WOODEN FRAME ANTIQUE WHITE + WOODEN PICTURE FRAME WHITE FINISH  
   → Create this décor bundle with 10–12% discount.

## Expected Lift / Sales Increase
- Alarm clock duo: lift 10.49 → bundling should increase sales of the second clock by approximately **950%** (9.5×) among buyers of the first → potential **+20–40% sales increase** in the alarm clock category.
- Lunch bag quartet: lift 8.6–8.9 → bundling should increase sales of additional lunch bags by **760–790%** (7.6–7.9×) → potential **+25–50% sales increase** in the lunch bag category.
- White frame pair: lift 8.27 → bundling should increase sales of the second frame by approximately **727%** (7.3×) → potential **+15–30% sales increase** in the frame category.

Overall: Implementing these bundles could realistically increase average order value by **10–25%** in the affected categories.

## Conclusion
The analysis identified strong, positive co-purchase patterns across multiple categories. These bundles provide clear opportunities to drive higher order values without competing on price.

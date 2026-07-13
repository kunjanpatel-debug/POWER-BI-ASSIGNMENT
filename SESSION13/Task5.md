
Task 5: AI-Assisted DAX Formulation Record

1. Context & Objective
The goal was to calculate the average delivery duration (in days) grouped by each specific city using the `session13_flipkart_dax` dataset containing order-level transactional lifecycles (`OrderDate` to `DeliveryDate`).

2. AI Prompt Utilized
text
Write a DAX formula for Power BI to calculate the average delivery time per city from a 'Flipkart Orders' dataset. The dataset contains 'City', 'OrderDate', and 'DeliveryDate' columns.

 3. Generated DAX Measure Configuration
The following optimized DAX measure was formulated using `AVERAGEX` to compute row-by-row temporal differences across the dataset before evaluating city-level contexts:

dax
AvgDeliveryTimePerCity = 
AVERAGEX(
    'session13_flipkart_dax',
    DATEDIFF('session13_flipkart_dax'[OrderDate], 'session13_flipkart_dax'[DeliveryDate], DAY)
)

4. Verification Check
Context Awareness: The measure dynamically adapts when dropped against a `City` column visual axis/matrix grid.
Granularity:Row-level difference calculation is correctly computed using `DATEDIFF` inside an iterator function (`AVERAGEX`).

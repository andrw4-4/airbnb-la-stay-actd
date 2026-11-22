# LA LA Stay — Files for Dashboard Team

## Current dataset
All files here were generated using `listings_clean (2).xlsx` (sheet: Clean data).
Do NOT mix them with `airbnb_la_*` files from the old cleaning notebook.

## Regression: LA_LA_Stay_Ridge_Model.pkl
Load with joblib.load(). Accepts exactly the columns listed under `features`
in LA_LA_Stay_Model_Info.json. The `.pkl` contains a preprocessing pipeline.
Use LA_LA_Stay_Regression_Input_Reference.csv for valid category values
and realistic median baseline scores for remaining amenity inputs.
The predictions are USD per night and may be negative for unusual inputs:
validate the user inputs and flag implausible predictions.

## Classification: LA_LA_Stay_Classification_Model.pkl
The trained tree accepts a ONE-column DataFrame: `price_ratio`.
Calculate `market_median` from LA_LA_Stay_Market_Reference.csv using:
neighbourhood_model, property_type_model, bedrooms, accommodates.
If the exact group contains fewer than 5 listings, use the neighbourhood
median; if unavailable use the overall training median.
price_ratio = current_price / market_median.
Thresholds: <0.9 => Opportunity to Charge More; >1.1 => Too High;
otherwise Competitive. For production alerts use the exact rule.

The high classifier accuracy only measures how well the tree copies the
threshold rule, NOT real pricing accuracy or expected occupancy.

## Evaluation
LA_LA_Stay_Metrics.csv: MAE, RMSE and R2 for regression (20% holdout).
LA_LA_Stay_Classification_Metrics.csv and LA_LA_Stay_Confusion_Matrix.csv:
accuracy, precision, recall, F1 and confusion matrix (20% holdout).
The regression metrics apply only to hosts 1-2, positive prices, flagged
outliers removed, and long stays removed. No booking or revenue guarantees.

## 5 Examples
LA_LA_Stay_5_Examples.csv includes five test cases.

## Notebook
Share the notebook `.ipynb` as a separate WhatsApp document.
It's the reproducible source and visualization walkthrough.

## Compatibility
Install the versions in requirements.txt before loading `.pkl` files.

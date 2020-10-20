# public-foretell

This repository contains supporting code for CSET Foretell. It currently contains only the Excel spreadsheet used to generate the values in Table 2 of “Future Indices: How Crowd Forecasting Can Inform the Big Picture.” Additional code and queries are forthcoming, including the queries used to generate the historical data used in Table 2.

## Table 2 Model
The primary purpose of the Table 2 Model is to explain how we generated the numbers in Table 2 of the Future Indices brief.

### Q&A Tab
This is a report exported from Foretell on October 11, 2020. The "question id" field is the same as the "Id" field elsewhere in this document. The only fields that matter are AI (bin ranges) and AL (aggregate crowd probabilities).

### Numbered Tabs
These tabs' names correspond to the "Id" field. There are two parts. Part II uses the forecast data to calculate a point estimate, and Part I combines the historical and forecast data to calculate a trend departure value.

#### Part II 
The point of Part II is to generate a point estimate as an input for Part I. The inputs for Part II are columns A (bins) and B (probabilities), both from the Q&A tab. From those, we create a fake data set with 100 entries (columns D & E). The fake data set simply has entries for every bin, in proportion to that bin's probability. The value of each entry is a randomly generated number within the bin range. The only figure here that matters for the rest of this analysis is the mean.

#### Part I
The point of Part I is to generate the trend departure value. Column C is the historical data, generated from the SQL queries on CSET's Foretell Github page (currently private). Column D contains the mean crowd forecast estimate from Part II. 

Table 2 uses the AAA ETS exponential smoothing algorithm (Excel's default) to generate a projection based on historical data. Columns F and G provide the upper and lower bounds of the 95% confidence interval for that forecast. 

To standardize the absolute difference (Column I) between the historical projection (Column F) and crowd forecast (Column D) across metrics with different levels of historical variation, we divide the Column I value by the 95% confidence interval of the AAA ETS algorithm (column H). 

Column J provides the standardized trend departure valued used in the "Summary" tab (and in Table 2). 

### Summary Tab
The "raw" section here simply summarizes the Column J trend departure values from the numbered tabs. The sign of the trend departure value here reflects the relationship between the metric and the predictor. If the metric and predictor are positively correlated, the sign is positive; if they're negatively correlated (e.g., row 4), the sign is negative.

The "Table 2" section provides the figures in Table 2. For the "metric" component, the numbers are primarily taken directly from the "raw" section. The only exception is the conditional O visas questions (row 23), which averages the trend departures from rows 16 and 17. The "predictor" component of this section simply averages the trend departure values of all metrics that inform that predictor.

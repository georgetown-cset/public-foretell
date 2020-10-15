# public-foretell

This repository contains supporting code for CSET Foretell. It currently contains only the Excel spreadsheet used to generate the values in Table 2 of “Future Indices: How Crowd Forecasting Can Inform the Big Picture.” Additional code and queries are forthcoming.

## Table 2 Model
The primary purpose of the Table 2 Model is to explain how we generated the numbers in Table 2 of the Future Indices brief. The spreadsheet contains some entries not directly relevant to Table 2, however. Those entries are identified here.

### Q&A Tab
This is a report exported from Foretell on October 11, 2020. The "question id" field is the same as the "Foretell ID" field elsewhere in this document. The only fields that matter are AI (bin ranges) and AL (aggregate crowd probabilities).

### Numbered Tabs
These tabs' names correspond to the "Foretell IDs” (or "question id" in the Q&A tab). There are two parts: The bottom (PDFs) part and the top part.

#### Bottom 
The point of this part is to derive PDFs from the forecast data. The inputs are columns A (bins) and B (probabilities), both from the Q&A tab. From those, we create a fake data set with 100 entries (columns D & E). The fake data set simply has entries for every bin, in proportion to that bin's probability. The value of each entry is a randomly generated number within the bin range. The only figure here that matters for the rest of this analysis is the mean: H34.

#### Top
The point of this part is to generate the trend departure estimate (column N). Column C is the historical data, generated from the SQL queries on CSET's Foretell Github page (currently private). Column D contains the mean forecast estimate from the bottom part of the tab (H34). Column E is currently extraneous but will eventually allow for comparisons between the crowd forecast and the subject-matter expert forecast.

Table 2 uses the AAA ETS exponential smoothing algorithm (Excel's default) to generate a projection based on historical data. Columns H and I provide the upper and lower bounds of the 95% confidence interval for that forecast. Column F provides a forecast based on linear regression, in case anyone prefers that method; it's not currently used in the analysis.

The data variance estimate is used to standardize the trend departure estimate across metrics with different levels of variation. Table 2 uses the 95% confidence interval of the AAA ETS algorithm (column J). Column k provides the standard deviation of the historical data, in case anyone prefers that method.

Column N provides the standardized trend departure figure used in the "Summary" tab (and Table 2). It's simply the difference between the historical projection and crowd forecast, divided by the 95% confidence interval of the historical projection. Columns O and P are alternative methods of estimating trend departure, not currently used in this analysis.

### Summary Tab
The "raw" section here simply summarizes the column N trend departure estimates from the numbered tabs (column F). Columns G and H provide alternative methods for estimating trend departure, not currently used in this analysis. The sign of columns F through H corresponds to the relationship between the metric and the predictor. If the metric and predictor are positively correlated, the sign is positive; if they're negatively correlated (e.g., row 4), the sign is negative.

The "Table 2" section provides the figures in Table 2. For the "metric" component, the numbers are primarily taken directly from the "raw" section. The only exception is the conditional O visas questions (row 25), which averages the trend departures from rows 17 and 18. The "predictor" component of this section simply averages the trend departure values of all metrics that inform that predictor.

# Customer segmentation with K-means (R)

A 2023 study: grouping retail customers by purchase behavior with K-means clustering in R.

> **Em português:** estudo de 2023 de segmentação de clientes de varejo com K-means em R, a partir de uma base pública de transações do Kaggle.

## Data

[Retail Sales Dataset](https://www.kaggle.com/datasets/mohammadtalib786/retail-sales-dataset) (Kaggle): 1,000 transactions with date, gender, age, product category (Beauty, Clothing, Electronics), quantity, price per unit and total amount.

The CSV is not in this repository. Download `retail_sales_dataset.csv` from Kaggle and put it next to the script.

## What the script does

`script_clients_segmentation.R`:

1. Turns gender and product category into numbers, removes the customer ID, and splits the date into year, month and day.
2. Scales every column, so no variable dominates the distances.
3. Runs K-means with 1 to 10 clusters and plots the within-cluster sum of squares (elbow method).
4. Runs K-means with 8 clusters and adds the cluster label to each transaction.
5. Prints the mean and standard deviation of each variable per cluster.
6. Plots age by cluster and gender by cluster.

## How to run

- R with the `tidyverse` and `cluster` packages.
- Put the CSV next to the script and run it in RStudio.

**Known issue:** line 6 (`df_scaled <- scale(df)`) runs before the text columns are converted, so the script stops there with `'x' must be numeric`. Delete that line: the data is scaled again, correctly, at line 36.

## What I would do differently today

- **Remove `Transaction.ID`.** It is a row number, not behavior, but it still goes into the clustering.
- **Remove `Total.Amount`.** It is quantity times price per unit, so it counts the same information twice.
- **Treat gender and category as categories.** K-means on codes like 1, 2 and 3 assumes an order and a distance that do not exist. One-hot encoding, or k-prototypes, fits these columns better.
- **Call `set.seed()` before K-means,** so every run gives the same clusters.
- **Check the number of clusters with the silhouette score,** not only the elbow plot.

## Author

Allan Felipe Silva, 2023.

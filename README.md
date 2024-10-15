<div align="center">
    <h1>Price Changes in Cryptocurrencies</h1>
</div>

<div align="center">
    <h4>By: Tai Reagan</h4>
</div>

<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/download.jpg" alt="crypto_currency" width="800"/>
</div>

---
<a name="top"></a>
# Table of Contents

<details>
  <summary>Click to expand</summary>


- [Overview](#overview)
- [Resources](#resources)
- [Analysis Process](#analysis-process)
  - [Data Preparation](#data-preparation)
  - [Finding Best Value for k Using the Scaled DataFrame](#finding-best-value-for-k-using-the-scaled-dataframe)
  - [Cluster Cryptocurrencies with K-means Using the Scaled DataFrame](#cluster-cryptocurrencies-with-k-means-using-the-scaled-dataframe)
  - [Optimize Clusters with Principal Component Analysis](#optimize-clusters-with-principal-component-analysis)
  - [Finding Best Value for k Using the PCA DataFrame](#finding-best-value-for-k-using-the-pca-dataframe)
  - [Cluster Cryptocurrencies with K-means Using the PCA DataFrame](#cluster-cryptocurrencies-with-k-means-using-the-pca-dataframe)
- [Comparing Results](#comparing-results)


</details>



## Overview 
Bitcoin (BTC), created in 2009, was the first cryptocurrency and remains the most valuable and well-known. Cryptocurrencies, in general, are recognized for their volatility, making them one of the riskiest assets to own. This analysis aims to explore whether cryptocurrencies are significantly impacted by 24-hour or 7-day price fluctuations. Using Python and unsupervised learning techniques, specifically K-means clustering, we group cryptocurrencies based on these price movements.

Additionally, Principal Component Analysis (PCA), a dimensionality reduction technique, is applied to simplify the data. PCA transforms a large set of variables into a smaller set while retaining most of the original information, making it easier to visualize and analyze complex data. This method allows us to reduce the complexity of the dataset without losing critical insights. This analysis provides valuable information for understanding price trends and clustering patterns in the cryptocurrency market.

## Resources 
The data used for the analysis was provided by [Crypto Market Data](https://github.com/Taireagan/Crypto-Clustering/blob/main/Resources/crypto_market_data.csv)

[Back to Top](#top)
<a href="#top" style="display: inline-block; background-color: black; color: white; padding: 5px 10px; text-decoration: none; border-radius: 5px;">Back to Top</a>


## Analysis Process 

### Data Preparation
- To prepare the data for analysis, the Crypto Market Data was first imported into a DataFrame using Jupyter Notebook.
![read_in_csv](https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/read_in_csv.png)

- Next, the data was normalized using the StandardScaler module from scikit-learn, ensuring that all features were scaled appropriately for further analysis. A new DataFrame was then created with the scaled data, using the **coin_id** from the original dataset as the index. This transformation facilitated a structured and normalized view of the first five rows of data, as shown below.
![standard_scaler](https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/standard_scaler.png)

[Back to Top](#top)
<a href="#top" style="display: inline-block; background-color: black; color: white; padding: 5px 10px; text-decoration: none; border-radius: 5px;">Back to Top</a>


### Finding Best Value for k Using the Scaled DataFrame 
- The elbow method was applied to determine the optimal value for **k** using the following steps:

 1. Created a list with the number of **k** values from 1 to 11. Then, created an empty list to store the inertia values.
<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/list_for_scaled.png" alt="list_for_sclaed" width="600"/>
</div>

> [!NOTE]
> The **k-value** in K-means clustering represents the number of groups (clusters) you want to divide your data into. **Inertia** measures how tightly the data points are grouped around the center of their cluster; lower inertia means the points are closer together, indicating better grouping.

   2. Created a for loop to compute the inertia with each possible value of **k**.
<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/for_loop_sclaed.png" alt="for_loop_scaled" width="600"/>
</div>

   3. Created a dictionary with the data to plot the elbow curve/ Then, ploted a line chart with all the inertia values computed with the different values of **k** to visually identify the optimal value for **k**.
<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/first_elbow_curve.png" alt="first_elbow_curve" width="600"/>
</div>

> [!NOTE]
> The elbow method helps find the best number of clusters by showing where adding more groups stops making a big difference in how well the data is grouped.

<p align="center"> 
    On the x-axis, you plot the <strong>k</strong> values, and on the y-axis, you plot the inertia. 
    The goal is to find the "elbow" or bend in the graph, which indicates the optimal 
    <strong>k</strong> value where adding more clusters doesn't significantly improve the model. 
    Here the graph indicated that the optimal value for <strong>k</strong> is 4.
</p>

[Back to Top](#top)
<a href="#top" style="display: inline-block; background-color: black; color: white; padding: 5px 10px; text-decoration: none; border-radius: 5px;">Back to Top</a>


### Cluster Cryptocurrencies with K-means Using the Scaled DataFrame 
- The following steps were used to cluster the cryptocurrencies for the best value for **k** on the scaled DataFrame:

1. Initialize the K-means model with the optimal **k** value, then fit the model and predict the clusters to group the cryptocurrencies using the scaled DataFrame. Next, create a copy of the scaled DataFrame and add a new column to store the predicted cluster assignments.

<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/clustering_scaled.png" alt="clustering_scaled" width="600"/>
</div>

2. Create a scatter plot using **hvPlot** setting the x-axis as **price_change_percentage_24h** and the y-axis as **price_change_percentage_7d**. Color the graph points with the labels found using K-means and add the **coin_id** column in the **hover_cols** parameter to identify the cryptocurrency represented by each data point.

<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/scatter_plot_scaled.png" alt="scatter_plot__scaled" width="600"/>
</div>


> [!TIP]
> hover_cols are the columns or data fields that display additional information when you hover over a specific point, providing more context about that data point.

[Back to Top](#top)
<a href="#top" style="display: inline-block; background-color: black; color: white; padding: 5px 10px; text-decoration: none; border-radius: 5px;">Back to Top</a>


### Optimize Clusters with Principal Component Analysis 
1. Perform a PCA on the original scaled DataFrame to reduce the features to three principal components.
2. Retrieve the explained variance to assess how much information each principal component captures, and calculate the total explained variance of the three components.

<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/explained_ratios.png" alt="explained_ratios" width="600"/>
</div>

<p align="center"> 
    The First component accounts for <strong>37%</strong> of the data. 
    The Second component accounts for <strong>35%</strong> of the data. 
    The Third component accounts for <strong>18%</strong> of the data. 
    The total explained variance of the three principal components is 
    <strong>0.8950 (89.50%)</strong>, which means that these three components 
    explain about <strong>90%</strong> of the total variance in the dataset.
</p>
   
3. Next, create a new DataFrame with the scaled PCA data, using the **coin_id** from the original DataFrame as the index. The first five rows of the scaled PCA DataFrame should appear as follows:

<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/pca_standard_scaler.png" alt="pca_standard_scaler" width="600"/>
</div>

[Back to Top](#top)
<a href="#top" style="display: inline-block; background-color: black; color: white; padding: 5px 10px; text-decoration: none; border-radius: 5px;">Back to Top</a>


### Finding Best Value for k Using the PCA DataFrame
Here we will use the Principal Component Analysis (PCA) as a technique used to simplify complex datasets by reducing the number of variables while still retaining most of the important information. It works by transforming the original data into a set of new variables called "principal components." These components are ordered so that the first few capture the most significant patterns or variance in the data. Essentially, PCA helps make data easier to analyze and visualize, especially when dealing with large sets of variables, by focusing on the key underlying trends.

- Use the elbow method on the scaled PCA DataFrame to find the best value for **k** using the following steps:

1. Created a list with the number of **k** values from 1 to 11. Then, created an empty list to store the inertia values.
<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/list_for_scaled.png" alt="list_for_sclaed" width="600"/>
</div>

> [!NOTE]
> The **k-value** in K-means clustering represents the number of groups (clusters) you want to divide your data into. **Inertia** measures how tightly the data points are grouped around the center of their cluster; lower inertia means the points are closer together, indicating better grouping.

2. Created a for loop to compute the inertia with each possible value of **k**.
<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/pca_for_loop.png" alt="pca_for_loop" width="600"/>
</div>

3. Create a dictionary with the data to plot the Elbow curve.Then, plot a line chart with all the inertia values computed with the different values of **k** to visually identify the optimal value for **k**.

 <div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/pca_elbow_plot.png" alt="pca_elbow_curve" width="600"/>
</div>

> [!NOTE]
> The elbow method helps find the best number of clusters by showing where adding more groups stops making a big difference in how well the data is grouped.

<p align="center"> 
    Using the PCA-scaled data, the optimal value for <strong>k</strong> remains 4, which is consistent with the value derived from the original scaled data. 
    In both cases, the elbow method indicates that 4 is the ideal number of clusters, showing no difference between the two datasets in determining the best <strong>k</strong>.
</p>



[Back to Top](#top)
<a href="#top" style="display: inline-block; background-color: black; color: white; padding: 5px 10px; text-decoration: none; border-radius: 5px;">Back to Top</a>


### Cluster Cryptocurrencies with K-means Using the PCA DataFrame
- The following steps were used to cluster the cryptocurrencies for the best value for **k** on the PCA DataFrame:

  1. Initialize the K-means model with the best value for **k**, then fit the K-means model and predict the clusters to group the cryptocurrencies using the scaled PCA DataFrame. Next, create a copy of the scaled PCA DataFrame and add a new column to store the predicted clusters.

<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/pca_predictions.png" alt="pca_predictions" width="600"/>
</div>

2. Create a scatter plot using **hvPlot setting the x-axis as **PC1** and the y-axis as **PC2**. Color the graph points with the labels found using K-means and add the **coin_id** column in the **hover_cols** parameter to identify the cryptocurrency represented by each data point.

<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/pca_scatter.png" alt="pca_scatter" width="600"/>
</div>

<p align="center">This scatter plot represents the PCA-scaled data, where the features have been reduced to two principal components (PC1 and PC2). The different colors represent distinct clusters that were predicted using K-means clustering. The clusters show relatively clear separation, with most data points concentrated near the origin. A few outliers are evident, with one in cluster 3 (green) and another in cluster 1 (red), suggesting these data points have unique characteristics compared to the others. The PCA scaling helps to simplify the multi-dimensional data while maintaining significant variance for cluster analysis.</p>


[Back to Top](#top)
<a href="#top" style="display: inline-block; background-color: black; color: white; padding: 5px 10px; text-decoration: none; border-radius: 5px;">Back to Top</a>


### Comparing Results

<div align="center">
    <h4>Elbow Curve Comparison</h4>
</div>
<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/comparing_elbow_curve.png" alt="elbow_comparison" width="600"/>
</div>

<p align="center"> When comparing the elbow curves of the original scaled data and the PCA-scaled data, both graphs consistently indicate that the optimal <strong>k</strong> value is 4.</p>

<div align="center">
    <h4>Cluster Scatter Plot Comparison</h4>
</div>
<div align="center">
    <img src="https://github.com/Taireagan/Crypto-Clustering/blob/main/Images/comparing_scatter_plot.png" alt="scaterr_comparison" width="600"/>
</div>

<p align="center"> The top scatter plot, based on the original scaled data, shows more spread along the axes and a clearer separation between some clusters, particularly in terms of the 24-hour and 7-day price changes. In contrast, the PCA-scaled scatter plot below shows the data reduced to two principal components, which condenses the variability while still maintaining distinguishable clusters. While both visualizations highlight similar cluster groupings, the PCA plot simplifies the complexity of the data, revealing clusters in a more compact form. .</p>

What is the impact of using fewer features to cluster the data using K-Means?
- When we use fewer features in K-Means clustering by applying PCA (Principal Component Analysis), it helps make the groups (or clusters) of data points easier to see. This is because PCA simplifies the data, reducing the overlap between clusters and making the boundaries between them clearer. This is especially helpful when we have a lot of features or dimensions in our data, as it lets us focus on the most important information without losing the overall structure of the clusters. However, some of the clusters might still overlap a little, depending on the data and the number of groups we're trying to create.


[Back to Top](#top)
<a href="#top" style="display: inline-block; background-color: black; color: white; padding: 5px 10px; text-decoration: none; border-radius: 5px;">Back to Top</a>



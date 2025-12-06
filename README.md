# Customer-Segmentation
Background¶

Nowadays, businesses generate large volumes of data capturing customer behavior. This data provides an important opportunity to understand customers at scale and support personalized services. One of the most widely used applications derived from such data is recommendation systems, which rely on meaningful customer insights to deliver relevant product suggestions.
Before any recommendation can be performed effectively, businesses must first understand who their customers are and how they behave. This foundational step is customer segmentation, and it plays a critical role in personalized recommendations.

For this project, let's use the Online Retail II dataset, which consists of real world e-commerce transactions. The dataset includes invoice, stock code, description, quantity, invoive data, price, customer ID, and country information.

Main problem

The main problem addressed in this project is the development of unsupervised customer segments that group similar customers together based on their purchasing behavior.
Motivation for Choosing This Topic
Recommendation is one of the most widely used machine learning applications. Recommendation systems power major platforms such as Amazon, Netflix, Spotify, and TikTok. Segmentation is the foundation of recommendations.

Project Flow

This project is structured through Data Loading & Cleaning, Exploratory Data Analysis (EDA), Model Selection and Comparison, Recommendation Exploration, and Results/ Analysis.
Silhouette score is used at the beginning to evaluate the performance, but it cannot work very well, we will go through in detail.

Dataset

https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci/data

Model Architecture and Result
The primary goal in this project is using unsupervised machine learning model to do customer segmentation. I tried 4 different model architectures.

Model 1: Product distribution + K-Means + PCA
Since we have a sense of the product that customers like to buy. We can cluster based on the Total quantity per product, the Proportion of each product purchased, the average price per product purchased.
First model we use is K-Means Clustering. K-Means is an unsupervised machine learning algorithm used to group data points into k distinct clusters based on similarity (Assign each data point to the nearest center point). It is one of the most widely used clustering methods in retail analytics, marketing, and customer segmentation because it is simple, fast, and interpretable.

Model 2: RFM + K-Means
The second model in this project combines RFM with K-Means clustering to create meaningful customer segments based on purchasing behavior. RFM stands for Recency, Frequency, and Monetary value—three key dimensions that capture how recently a customer made a purchase, how often they purchase, and how much they spend overall. These features summarize each customer’s relationship with the retailer instead of looking at individual products.

Model 3: RFM + GMM
For model 3, I want to try RFM + Gaussian Mixture Model (GMM). Compared with K-Means, GMM allows soft clustering, so customers can belong to multiple segments with different probabilities. It may often be more realistic than K-Means for customer segmentation.

Model 4: Jaccard based customer segmentation
Collaborative segmentation treats customers as “similar” if they purchase similar products, instead of relying on pre-defined features like RFM. We compute the Jaccard similarity between each pair of customers.Then applying agglomerative hierarchical clustering to group customers with similar purchase patterns into clusters.

Recommandation Result and Analysis

Recommendation using Model 2: RFM + K-Means¶
Recommendation Strategy: For each cluster, the most popular products purchased by other customers in the same cluster were recommended.

Recommendation using Model 3: RFM + GMM
The soft clustering of GMM allows more personalized recommendations by considering nuanced customer behaviors, producing slightly different top products for each individual, even within the same cluster.

Conclusion¶
To simulate the experience of how modern e-commerce companies build their recommendation pipelines, I began this project by focusing on customer segmentation using unsupervised machine learning techniques.

The analysis was performed using four different segmentation models—each designed to capture different aspects of customer behavior:

Product Distribution + PCA + K-Means (Model 1)

RFM Features + K-Means (Model 2)

RFM Features + Gaussian Mixture Model (GMM) (Model 3)

Jaccard + Hierarchical Clustering (Model 4)

Evaluation - Problems I Meet
Initially, silhouette score was used to determine cluster quality. However, it consistently favored 2 clusters for all models. Although mathematically valid, this produced very unbalanced clusters, where almost all customers fell into one cluster, and only a small number formed the second cluster.

Therefore, I evaluated models using more actionable criteria, including distribution balance across clusters, business interpretability. This approach resulted in much more valuable segmentation outcomes.

Among the 4 models. Model 2 is best for segmentation and model 3 is best for personalization.

Their clustering results have some similar parts. By analysis, the main difference is that Model 3 has a wider range for the second-level high-value and loyal customers. From a cluster balance and personalization perspective, Model 3 has a better result. However, Model 2 may be easier to interpret. It will be better to compare model output with user research questionnaire to get better ideas.

Future Work
In the future, I may continue looking for better model evaluation methods. And try more clustering methods, including sequential modeling to find users' behaviour change.

Reference
RFM: https://www.investopedia.com/terms/r/rfm-recency-frequency-monetary-value.asp

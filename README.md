# Bank Customer Segmentation using K-Means
Customer segmentation using K-Means clustering to identify distinct customer profiles and support targeted banking strategies.

## 1.- Business problem 
The goal of this project is to segment bank customers into distinct groups based on their demographic, financial, and engagement characteristics. The resulting customer segments can help the bank better understand its customer base and develop more targeted marketing, engagement, and retention strategies.

## 2.- Dataset 
### 2.1.- Dataset understanding 
The dataset is publicly available on Kaggle and contains information about bank customers, including demographic, financial, and banking activity information, as well as whether the customer left the bank.

*Dataset source:* [Dataset in Kagge](https://www.kaggle.com/datasets/radheshyamkollipara/bank-customer-churn)

The dataset contains 10,000 customers and 18 variables initially.

| Variable | Description |
|---|---|
| `RowNumber` | Record number. Each row represents a customer. |
| `CustomerId` | Unique customer identifier. |
| `Surname` | Customer's surname. |
| `CreditScore` | Customer's credit score. |
| `Geography` | Customer's country. |
| `Gender` | Customer's gender. |
| `Age` | Customer's age. |
| `Tenure` | Number of years the customer has been with the bank. |
| `Balance` | Customer's account balance. |
| `NumOfProducts` | Number of bank products used by the customer. |
| `HasCrCard` | Whether the customer has a credit card. |
| `IsActiveMember` | Whether the customer is an active bank member. |
| `EstimatedSalary` | Customer's estimated salary. |
| `Exited` | Whether the customer left the bank.|
| `Complain` | Whether the customer has made a complaint. |
| `Satisfaction Score` | Customer satisfaction score regarding complaint resolution. |
| `Card Type` | Type of credit card held by the customer. |
| `Point Earned` | Points earned through credit card usage. |

## 3.- Data cleaning 
The structure of the dataset was first examined. The dataset contains 10,000 entries representing customers and 18 columns initially.

During this phase duplicates, missing and inconsistent values were searched, but no repeated or missing rows/ values were found.

## 4.- Feature selection 
The features were selected based on their potential to describe meaningful differences between bank customers.

The segmentation uses demographic, financial, and customer engagement variables, including CreditScore, Geography, Age, Tenure, Balance, NumOfProducts, HasCrCard, IsActiveMember, EstimatedSalary, and Card Type.

Identifier variables such as RowNumber, CustomerId, and Surname were excluded because they do not provide meaningful information for customer segmentation. The target variable Exited was also excluded from the clustering process, as the objective is to create customer segments independently of churn. Complain, Satisfaction Score, and Point Earned were excluded to keep the segmentation focused on broader customer characteristics and avoid potentially redundant or overly specific information.

After feature selection, categorical variables were encoded and the numerical features were scaled before applying the clustering algorithm.

## 5.- Exploratory Data Analysis 

The selected features were divided into numerical and categorical variables to analyse their distributions and relationships separately.

### Numerical Features

Summary statistics and histograms were used to understand the distribution of the numerical variables.

![Summary statistics](images/numerical%20summary%20statistics.png) 
![Distributions](images/numerical%20distributions.png)  
No concerning outliers or unusual patterns were identified in the distributions. However, the variables have different numerical scales, which highlights the need for feature scaling before applying K-Means.

One notable observation is that a considerable number of customers have a balance of zero. This was kept as part of the original data, as it may represent a meaningful characteristic of certain customer segments.

### Categorical Features

Bar plots were used to examine the distribution of the categorical variables.

![Barplot](images/CardType%20barplot.png) 
![Barplot](images/Geography%20barplot.png)
![Barplot](images/HarCrCard%20barplot.png)
![Barplot](images/IsActiveMember%20barplot.png)
![Barplot](images/NumOfProducts%20barplot.png)

The largest customer group is located in France, and most customers have one product, a credit card, and active membership. Overall, the categorical variables show reasonable distributions without any obvious data quality issues.

### Correlation Analysis

A correlation matrix was used to examine the relationships between the numerical variables.

No strong correlations were identified between the selected numerical features, suggesting that there are no major multicollinearity issues that would require removing variables before applying the clustering algorithm.

![Correlation matrix](images/correlation%20matrix.png)

## 6.- Data processing 
The categorical features were transformed using One-Hot Encoding, converting each category into a numerical binary variable.

The numerical features were standardized using StandardScaler so that all variables are on a comparable scale. This is important for K-Means because the algorithm is sensitive to the scale of the features.

## 7.- Choosing K 

The Elbow Method was used to determine the appropriate number of clusters. Different values of k were tested and their inertia was compared. Based on the point where the reduction in inertia started to decrease, 4 clusters were selected as a suitable balance between model simplicity and cluster separation.

![Elbow method](images/elbow%20method.png)

## 8.- Clusters analysis 
The resulting clusters were analyzed based on their average numerical features and customer size. The main characteristics of each segment are shown below.

![Clusters](images/CardType%20vs%20Clusters.png)
![Clusters](images/Geography%20vs%20clusters.png)
![Clusters](images/HasCrCard%20vs%20clusters.png)
![Clusters](images/IsActiveMember%20vs%20clusters.png)
![Clusters](images/NumOfProducts%20vs%20clusters.png)
![Clusters](images/cluster%20vs%20numerical%20features.png)

### Cluster 0: Established Customers

Cluster 0 contains 2,710 customers. These customers have an average age of 36 years and a relatively high average balance of approximately 122,186. They have been with the bank for the longest period, with an average tenure of 7.6 years. They use an average of 1.38 products and have a moderate level of activity, with 46% classified as active members. Overall, this segment can be characterized as relatively established customers with high account balances and long relationships with the bank.

### Cluster 1: Low-Balance Customers

Cluster 1 is the largest segment, with 3,298 customers. These customers have an average age of 36 years and a very low average balance of approximately 1,119. They have an average tenure of 5.1 years and use the highest average number of products among the four segments, at 1.79 products per customer. Approximately 49% are active members. This segment is therefore characterized by younger customers with very low account balances and relatively higher product usage.

### Cluster 2: Older Active Customers

Cluster 2 is the smallest segment, with 1,271 customers. It is clearly distinguished by its higher average age of approximately 59 years. Customers in this segment have an average balance of around 79,660 and an average tenure of 4.9 years. They also have the highest level of engagement, with approximately 68% classified as active members. This segment can be characterized as an older and relatively highly engaged customer group.

### Cluster 3: Shorter-Tenure High-Balance Customers

Cluster 3 contains 2,721 customers. These customers have an average age of approximately 36 years, and have a high average balance of around 120,837. However, they have the shortest relationship with the bank, with an average tenure of only 2.4 years. They use an average of 1.39 products and around 52% are active members. This segment can therefore be characterized by customers with relatively high balances but shorter relationships with the bank.



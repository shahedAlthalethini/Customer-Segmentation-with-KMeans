# Customer-Segmentation-with-KMeans

![Uploading image.png…]()

---

## 📋 Table of Contents

*   [Project Overview](#-project-overview)
*   [Introduction — What is Customer Segmentation?](#-introduction--what-is-customer-segmentation)
*   [Business Scenario](#-business-scenario)
*   [Explore the Dataset](#-explore-the-dataset)
*   [Data Preprocessing](#-data-preprocessing)
*   [K-Means for Segmentation](#-k-means-for-segmentation)
*   [PCA with K-Means for Better Visualization](#-pca-with-k-means-for-better-visualization)
*   [Conclusion](#-conclusion)
*   [How to Use](#-how-to-use)

## Project Overview

This project demonstrates the application of unsupervised machine learning to solve a common business problem: customer segmentation. By analyzing customer data, we can uncover hidden patterns and group customers into meaningful segments.

### Goal
The primary goal is to segment customers of an FMCG company into distinct groups based on their demographic and behavioral data. This will enable the marketing department to develop targeted and effective campaigns, ultimately increasing ROI and customer satisfaction.

### Role
As a Data Scientist, my role is to process and analyze the customer dataset, apply appropriate clustering algorithms, interpret the resulting segments, and provide actionable insights to the marketing team.

### Challenges
*   **Determining Optimal Clusters:** Identifying the correct number of customer segments (`k`) is a critical and often subjective task.
*   **Interpreting Segments:** Once clusters are formed, the challenge is to analyze their characteristics to create meaningful and actionable "personas" for each group.
*   **High-Dimensional Data:** With multiple features, visualizing the clusters is difficult. We need a way to reduce dimensions without losing significant information.
*   **Feature Scaling:** Algorithms like K-Means are sensitive to the scale of the data. Features like `Income` can disproportionately influence the result if not handled correctly.

## Introduction — What is Customer Segmentation?

Let’s say you decided to buy a t-shirt from a brand online. Have you ever thought about who else bought the same t-shirt?

People who are similar to you, right? Same age, same hobbies, same gender, etc.

In marketing, companies basically try to find your t-shirt on other people!

But wait, how? Of course, with data! Customer segmentation is that simple.

We actually try to find and group customers based on common characteristics such as age, gender, living area, spending behavior, etc., so that we can market to them effectively.

Let’s dive into our segmentation project!

## Business Scenario

Suppose we are working as a data scientist for an FMCG company and want to segment our customers to help the marketing department launch new products and sales based on the segmentation. Therefore, we will save our time and money by marketing a specific group of customers with selected products.

**How did we collect the data, by the way?**

All data has been collected through the loyalty cards customers use at checkout. :)

We will utilize K-Means and PCA algorithms for this project and see how we define new grouped customers!

## Explore the Dataset

Understanding the data is important! Before starting any project, we need to understand the business problem and the dataset first. Let’s see the variables (features) in the dataset.

| Variable | Description |
| :--- | :--- |
| **ID** | Shows a unique identification of a customer. |
| **Sex** | Gender of a customer. `0: male`, `1: female`. |
| **Marital status** | Marital status of a customer. `0: single`, `1: non-single`. |
| **Age** | Age of the customer in years (Min: 18, Max: 76). |
| **Education** | Level of education. `0: other/unknown`, `1: high school`, `2: university`, `3: graduate school`. |
| **Income** | Self-reported annual income in US dollars (Min: 35832, Max: 309364). |
| **Occupation** | Category of occupation. `0: unemployed/unskilled`, `1: skilled`, `2: management/highly qualified`. |
| **Settlement size** | The size of the city the customer lives in. `0: small`, `1: mid-sized`, `2: big city`. |

## Data Preprocessing

To prepare the data for our K-Means model, we performed the following preprocessing steps:

1.  **Dropping Unnecessary Columns:** The `ID` column was removed as it is a unique identifier and provides no value for clustering.
2.  **Feature Scaling:** Since K-Means is a distance-based algorithm, it's crucial to scale our features. We used `StandardScaler` from scikit-learn to standardize the data, ensuring that features with large ranges (like `Income`) do not dominate the clustering process. Each feature was transformed to have a mean of 0 and a standard deviation of 1.

## K-Means for Segmentation

K-Means is an iterative algorithm that partitions a dataset into a pre-determined number of non-overlapping subgroups (clusters), where each data point belongs to only one group.

1.  **Finding the Optimal 'k' (The Elbow Method):** To find the optimal number of clusters, we used the Elbow Method. We calculated the Within-Cluster Sum of Squares (WCSS) for a range of `k` values (from 1 to 10). The plot showed a distinct "elbow" at **k=4**, indicating that four clusters would be a good balance between capturing variance and avoiding overfitting.

2.  **Model Training and Interpretation:** We trained the K-Means model with `k=4` on the scaled data. After assigning each customer to a cluster, we analyzed the characteristics of each group by examining the original, unscaled feature values. This allowed us to create distinct personas:

    *   **Cluster 0: "Standard"** - Average income, mixed demographics. Represents the general customer base.
    *   **Cluster 1: "Career-Focused"** - High income, older, well-educated, and in high-level occupations.
    *   **Cluster 2: "Young & Ambitious"** - Younger, single, educated but with lower-to-mid-range incomes. High potential for future growth.
    *   **Cluster 3: "Well-Off"** - The highest income and education group, often married, and living in larger cities.

## PCA with K-Means for Better Visualization

Our dataset has 7 dimensions, making it impossible to visualize directly. To solve this, we used **Principal Component Analysis (PCA)**.

PCA is a dimensionality reduction technique that transforms the data into a new coordinate system of "principal components." We reduced the 7 scaled features into just 2 principal components, which together capture the maximum possible variance from the original data.

By plotting these two components on a scatter plot and coloring each point according to its assigned cluster, we can visually confirm the effectiveness of our segmentation. The plot clearly shows four distinct, well-separated groups.



## Conclusion

This project successfully segmented customers into four distinct, actionable groups using K-Means clustering. By leveraging these insights, the FMCG company can now move away from a "one-size-fits-all" marketing approach.

**Actionable Insights:**
*   **Standard Group:** Target with general promotions and brand awareness campaigns.
*   **Career-Focused Group:** Market premium products and loyalty programs.
*   **Young & Ambitious Group:** Engage with social media campaigns, trendy products, and entry-level offers.
*   **Well-Off Group:** Target with exclusive, high-end products and personalized service offerings.

This data-driven approach allows for more efficient allocation of marketing resources, leading to higher campaign effectiveness and stronger customer relationships.

## How to Use

To replicate this analysis, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/Customer-Segmentation-Analysis.git
    cd Customer-Segmentation-Analysis
    ```

2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Run the analysis:**
    Open and run the `Customer_Segmentation.ipynb` Jupyter Notebook to see the step-by-step process.

# Behavioral User Segmentation for a Movie Review Platform

## Overview

This project focuses on identifying distinct user behavior patterns on a movie review platform using unsupervised machine learning. The goal was to segment users based on their interaction behavior and lifecycle characteristics, and to evaluate whether these segments meaningfully capture differences in engagement and future activity. The resulting segmentation provides insights that can support targeted engagement strategies, user retention efforts, and product personalization.

The analysis uses historical movie rating data containing user identifiers, movie identifiers, ratings, and timestamps. Behavioral features were engineered to summarize how users interact with the platform, and clustering techniques were applied to group users into meaningful cohorts. The project follows a rigorous segmentation workflow including stability analysis, predictive validation, statistical testing, and algorithm robustness checks.



## Dataset

The dataset contains movie ratings from users over a long time horizon. Each record includes:

- `userId`: unique identifier for a user  
- `movieId`: unique identifier for a movie  
- `rating`: rating given by the user  
- `timestamp`: time at which the rating was submitted  

For segmentation, user behavior was analyzed primarily using interactions between **2013 and 2014**, which served as the observation window. Activity from **2015** was used as a future validation period to test whether the identified segments could predict subsequent user engagement.



## Feature Engineering

User-level behavioral features were engineered to represent different aspects of engagement and lifecycle dynamics:

- **num_interactions** – total number of ratings submitted by the user  
- **active_days** – number of distinct days on which the user was active  
- **recency_days** – number of days since the user's last interaction  
- **span_days** – time difference between the first and last recorded interaction  

Together, these features capture engagement intensity, activity frequency, recency of interaction, and overall engagement lifespan.

Before clustering, the features were standardized to ensure that differences in scale did not bias the clustering algorithm.



## Clustering Methodology

User segmentation was performed using **K-Means clustering**. The optimal number of clusters was determined using inertia and silhouette analysis, which indicated that **four clusters** provided a meaningful separation of user behavior.

To ensure the segmentation was reliable, clustering stability was tested by running the algorithm multiple times with different initialization seeds and measuring agreement using the **Adjusted Rand Index (ARI)**. The clustering demonstrated extremely high stability, confirming that the identified segments were not artifacts of random initialization.



## Segment Profiles

Analysis of cluster centroids revealed four distinct user personas based on engagement behavior:

- **Core Loyal Users**  
  Users with high interaction counts, long engagement spans, and recent activity. These users contribute consistently to the platform and demonstrate the highest future retention.

- **Burst Reviewers**  
  Users who generate many interactions in a short time span but show limited long-term engagement. Their behavior often reflects short bursts of activity followed by inactivity.

- **Fading Users**  
  Users who were previously active but have gradually disengaged from the platform. Their activity spans are longer than burst users but their recency indicates declining engagement.

- **Churned Users**  
  Users who have not interacted with the platform for a long time and show almost no future activity.

These segments form a clear lifecycle gradient from highly engaged users to fully inactive ones.



## Predictive Validation

To evaluate whether the clusters capture meaningful behavioral differences, segmentation was performed using only **2013–2014 data**, while user activity in **2015** was used as a validation window.

Results showed strong differences in future engagement between clusters. Core loyal users exhibited significantly higher interaction counts and retention rates, while churned users showed almost no return activity. Intermediate clusters displayed moderate levels of future engagement.

This temporal validation demonstrates that the segmentation is not merely descriptive but also **predictive of future user behavior**.



## Statistical Testing

To formally verify that the observed differences between clusters were statistically significant, a **Kruskal–Wallis test** was performed on future interaction counts across clusters.

The test confirmed highly significant differences with a large effect size, indicating that cluster membership explains a substantial portion of the variation in future engagement. This provides strong statistical evidence that the segments represent distinct behavioral populations.



## Segment Drivers

A supervised classifier was trained to predict cluster membership using the engineered behavioral features. The model achieved approximately **98% accuracy**, indicating that the segments are highly separable in feature space.

Feature importance analysis revealed that the most influential drivers of segment membership were:

1. Recency of activity  
2. Number of interactions  
3. Engagement span  
4. Number of active days  

This indicates that user segmentation on the platform is primarily driven by a combination of **engagement intensity and lifecycle recency**.



## Algorithm Robustness

To ensure the segmentation was not dependent on the assumptions of K-Means clustering, a **Gaussian Mixture Model (GMM)** was also applied. Although cluster assignments differed slightly due to differences in boundary placement, the same underlying behavioral personas emerged.

Both algorithms consistently identified loyal, regular, fading, and churned user groups, demonstrating that the segmentation reflects intrinsic structure in the data rather than algorithm-specific artifacts.



## Business Implications

The resulting segmentation provides a practical framework for user engagement strategies:

- **Core Loyal Users** can be targeted with loyalty programs, recognition mechanisms, and community-driven features.  
- **Burst Reviewers** may benefit from post-session engagement prompts and personalized follow-up recommendations.  
- **Fading Users** are candidates for reactivation campaigns highlighting new content or platform features.  
- **Churned Users** represent low-engagement cohorts where reactivation efforts should be limited or experimental.

By tailoring strategies to these segments, platforms can improve retention, increase user engagement, and better allocate marketing resources.



## Conclusion

This project demonstrates a comprehensive behavioral segmentation pipeline, moving beyond simple clustering to include stability analysis, predictive validation, statistical significance testing, and algorithm robustness checks. The resulting user segments reveal a clear lifecycle structure and provide actionable insights for improving user engagement and retention.

The workflow implemented in this project represents a rigorous and production-oriented approach to user segmentation in real-world platforms.

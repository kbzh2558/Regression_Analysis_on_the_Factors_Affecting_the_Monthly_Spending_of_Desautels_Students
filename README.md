# 📝💰 Regression Analysis on the Factors Affecting the Monthly Spending of Desautels Students
![Excel](https://img.shields.io/badge/Microsoft-Excel?logo=microsoft-excel&logoColor=green)

⚡ Optimization in Balance between Demand Capturing and Cost Deployment ⚡

> [!NOTE]
> This project was carried out by students (Mingshu Liu, Xiasheng Quan, Faye Wu, and Kaibo Zhang) of Desautels Faculty of Management at McGill University, under the supervision of Professor [Rim Hariss](https://www.mcgill.ca/desautels/rim-hariss). It was built upon previous research done by scholars at HKUST. Click [here](https://doi.org/10.1145/2820783.2820837.).

## Overview

Bike-sharing systems have emerged as a popular and sustainable mode of transportation in urban environments, offering an efficient means of travel for commuters and tourists alike. Understanding the dynamics of bike-sharing demand is crucial for optimizing resource allocation to ensure efficient service delivery and customer satisfaction. Leveraging the dataset and preprocessing techniques established by prior researchers, our study aims to develop a simplified yet robust model capable of capturing the nuances of demand variations and customer patterns. Furthermore, this study goes beyond mere prediction by integrating an optimization model to determine the optimal number of bikes to deploy. Focusing on the week of August 16th to August 22nd, we aim to devise a strategy for resource allocation that maximizes efficiency and minimizes operational costs. In essence, this project bridges academic research and practical
applications, offering a comprehensive framework for understanding and managing the transitional demands of bike-sharing stations in New York City. By leveraging insights from previous research and employing advanced analytical techniques, we aspire to contribute to the ongoing efforts to enhance the sustainability and accessibility of urban transportation systems.

![image](https://github.com/kbzh2558/Bike-sharing_System_in_New_York_City/assets/161892255/375a9212-296e-4e12-a64b-ab73e70ee3a6)


### Step-by-step Breakdown

1. <details>
    <summary>Network Analysis.</summary>

    - we used the `networkx` package as the primary tool for network analysis. **NOTE:** We aggregated trip records on an hourly basis and created an adjacency matrix.
    - this helped us to capture the inherited relationship between individual stations and include them in the clustering algorithm.
   </details>

2. <details>
    <summary>K-NN.</summary>

    - we used the `sktlearn` package to perform unsupervised learning on the dataset to group stations together. Detailed rationales can be found in the paper. 
   </details>

3. <details>
    <summary>Exponential Smoothing ETS.</summary>

    we had to predict the transition probability, in other words, the tendency for a bike to travel from one cluster to the other at different times between clusters:

      - The `ETS` model: was chosen for its capability to capture human behavioral probabilities, past dependencies, and seasonalities, aligning with the nature of bike-sharing systems.

   </details>

4. <details>
    <summary>Multiple Regression.</summary>

      - considered the hour of the day and day of the week for temporal patterns and incorporates meteorological features: weather type, temperature, and wind speed.

      - autocorrelation found from the Watson test (Durbin-Watson statistic of 0.781) to assess autocorrelation:
        - a. Persistent seasonality observed in residuals (ACF & PACF), despite attempts to decompose, AND
        - b. non-stationary residuals
   </details>

5. <details>
    <summary>ARIMA.</summary>

    - we used auto `ARIMA` to explore the remaining time dependency correlations in the residuals. **NOTE:** `ARIMA` struggles to capture high peaks in time series accurately.

    </details>

6. <details>
   <summary>Gurobi Optimization.</summary>

    - we used `gurobi` to implement our optimization model.
    - the detailed documentation and methods for `gurobi` usage can be found [here](https://www.gurobi.com/).
    - the optimization formulation was in essence a linear programming model:

        - a. with decision variables keeping track of the transitional flow of bikes between clusters to find the optimal number of initial bike deployments.
        - b. the parameters were calculated from the abovementioned prediction models.
        - c. the `objective function` was imitating the techniques of `LASSO Regression` by introducing a regularization term `lamda (λ)` into the formula, seeking to minimize the mismatch between the estimated demand and the number of bikes              checked out at each cluster while penalizing attempts to overly increase the number of initial bikes needed, thereby aligning supply with anticipated demand.
        - d. The optimal `λ` = 6 was selected through trials and errors and sensitivity analysis on the magnitude of changes in demand mismatch.
   </details>

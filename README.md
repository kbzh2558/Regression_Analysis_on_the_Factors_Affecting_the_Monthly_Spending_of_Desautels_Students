# 📝💰 Regression Analysis on the Factors Affecting the Monthly Spending of Desautels Students
![Excel](https://img.shields.io/badge/Microsoft-Excel?logo=microsoft-excel&logoColor=green)

⚡ Exploratory Data Analysis, Hypothesis Testing, and Multiple Regression Engineering ⚡

> [!NOTE]
> This project was carried out by Kaibo Zhang, a student of Desautels Faculty of Management at McGill University, under the supervision of Professor [Gabriel Frieden](https://www.mcgill.ca/desautels/gabriel-frieden). This study relied on first-hand data collection through a self-administered questionnaire developed on the Qualtrics platform. 

## Overview

University presents an opportune platform for students to develop their financial literacy skills. At Desautels, the Faculty of Commerce, students begin their education by learning about the economy, accounting, and global business backgrounds, which are on broader scopes than trifles like monthly spending. Despite most of their outstanding academic performance, many encounter challenges in controlling their expenditures due to an inadequate understanding of the underlying factors affecting their spending behavior. Thus, this research investigates the effects of multiple factors on the monthly spending of students enrolled at Desautels. By performing statistical analyses of the data collected, this paper aims to interpret the relationship between our targeting variables and monthly spending to provide valuable insights into practical recommendations for controlling students’ monthly spending. These recommendations will assist students in understanding their spending behaviors and managing their budgets to attain their respective financial goals.


### Step-by-step Breakdown

1. <details>
    <summary>Data Collection.</summary>

    - data collection was completed through a delicately designed questionnaire built on `Qualtrics` platform. The link can be found [here](https://qfreeaccountssjc1.az1.qualtrics.com/jfe/form/SV_bsIn07U5qcK27IO). The questionnaire comprised seven questions, six requiring numerical inputs, while the remaining required a text input.
    - Based on conventional wisdom, the following independent variables were selected:
        - a. the distance of residence from McGill in kilometers (quantitative),
        - b. frequency of dining out per month in numbers of times (quantitative),
        - c. living arrangement(categorical),
        - d. number of monthly subscriptions (quantitative),
        - e. frequency of going to the groceries in numbers of times (quantitative), and
        - f. the number of shopping (quantitative).
    
    **NOTE:** Below are some screenshots of the questionnaire.
   
    - Cover page of the questionnaire:
    ![image](https://github.com/user-attachments/assets/23d13083-0590-4a8c-8296-597b7d64b1ff)

    - First half of the questionnaire:
    ![image](https://github.com/user-attachments/assets/66350378-43b0-44e3-9263-4fa09aa34403)

    - Second half of the questionnaire:
    ![image](https://github.com/user-attachments/assets/f91c1c60-c4cd-4225-9779-253696008f8c)

   </details>

3. <details>
    <summary>K-NN.</summary>

    - we used the `sktlearn` package to perform unsupervised learning on the dataset to group stations together. Detailed rationales can be found in the paper. 
   </details>

4. <details>
    <summary>Exponential Smoothing ETS.</summary>

    we had to predict the transition probability, in other words, the tendency for a bike to travel from one cluster to the other at different times between clusters:

      - The `ETS` model: was chosen for its capability to capture human behavioral probabilities, past dependencies, and seasonalities, aligning with the nature of bike-sharing systems.

   </details>

5. <details>
    <summary>Multiple Regression.</summary>

      - considered the hour of the day and day of the week for temporal patterns and incorporates meteorological features: weather type, temperature, and wind speed.

      - autocorrelation found from the Watson test (Durbin-Watson statistic of 0.781) to assess autocorrelation:
        - a. Persistent seasonality observed in residuals (ACF & PACF), despite attempts to decompose, AND
        - b. non-stationary residuals
   </details>

6. <details>
    <summary>ARIMA.</summary>

    - we used auto `ARIMA` to explore the remaining time dependency correlations in the residuals. **NOTE:** `ARIMA` struggles to capture high peaks in time series accurately.

    </details>

7. <details>
   <summary>Gurobi Optimization.</summary>

    - we used `gurobi` to implement our optimization model.
    - the detailed documentation and methods for `gurobi` usage can be found [here](https://www.gurobi.com/).
    - the optimization formulation was in essence a linear programming model:

        - a. with decision variables keeping track of the transitional flow of bikes between clusters to find the optimal number of initial bike deployments.
        - b. the parameters were calculated from the abovementioned prediction models.
        - c. the `objective function` was imitating the techniques of `LASSO Regression` by introducing a regularization term `lamda (λ)` into the formula, seeking to minimize the mismatch between the estimated demand and the number of bikes              checked out at each cluster while penalizing attempts to overly increase the number of initial bikes needed, thereby aligning supply with anticipated demand.
        - d. The optimal `λ` = 6 was selected through trials and errors and sensitivity analysis on the magnitude of changes in demand mismatch.
   </details>

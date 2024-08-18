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
    - based on conventional wisdom, the following independent variables were selected:
        - a. the distance of residence from McGill in kilometers (quantitative),
        - b. frequency of dining out per month in numbers of times (quantitative),
        - c. living arrangement(categorical),
        - d. number of monthly subscriptions (quantitative),
        - e. frequency of going to the groceries in numbers of times (quantitative), and
        - f. frequency of shopping (quantitative).
    
    **NOTE:** Below are some screenshots of the questionnaire.
   
    - Cover page of the questionnaire:
    ![image](https://github.com/user-attachments/assets/23d13083-0590-4a8c-8296-597b7d64b1ff)

    - First half of the questionnaire:
    ![image](https://github.com/user-attachments/assets/66350378-43b0-44e3-9263-4fa09aa34403)

    - Second half of the questionnaire:
    ![image](https://github.com/user-attachments/assets/f91c1c60-c4cd-4225-9779-253696008f8c)

    The data was exported into an `xlsx` file for further analysis. 

   </details>

2. <details>
    <summary>Exploratory Data Analysis.</summary>

    - exploratory data analysis was conducted to comprehensively understand the data at hand. The study included the following portions:
        - a. `SOCS` analysis for variable distributions,
        - b. `Confidence Interval` inference for population means, and
        - c. `Correlation` analysis between the variables.
    
    Detailed rationales and explanations can be found in the paper. 
   </details>

3. <details>
    <summary>Hypothesis Testing.</summary>

    - several hypothesis tests were conducted to gain more directional insights before building the actual regression model:

      - a. two-sample t-test for difference in population means
      - b. one-sample t-test for the true slope beta1
      - c. global f-test for all variables

    The detailed explanations can be found in the paper. 

   </details>

4. <details>
    <summary>Multiple Regression.</summary>

      - to obtain the optimal multiple regression model, this study mimicked the `best subset` method and tested all possible combinations of variables.
      - then, further examinations were conducted to remove insignificant variables from the model.

      the final equation obtained is as follows:
        - Monthly Spending = 916.4253 + 16.7489 (Dine-out) + 85.4177 (Groceries) + 29.4629 (Subscriptions) + e
   </details>


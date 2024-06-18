# Media Mix Modeling (MMM)

**Aim of the project:** Optimization of media budget allocation using Lightweight MMM.


What are MMMs?
- MMMs are statistical models used to measure the effectiveness of marketing spending.

Media Mix Models use :
  - historical sales data to predict sales
  - based on advertising variables and some control variables like weather, seasonality and market competition.

At the base of it, MMMs are machine learning models which are used to answer causal questions like **What was the ROAS of Google Ads?** where the cause is the amount spent on google ads and the ROAS is the effect.


**Dataset used:** https://github.com/ajitjadhav10/Mix_Marketing_Modeling/blob/d9759c6d8cc35d8dc112cc462eff02f63b38b7df/data.csv

Snapshot of the data ![](https://github.com/ajitjadhav10/Mix_Marketing_Modeling/blob/d9759c6d8cc35d8dc112cc462eff02f63b38b7df/Images/Screenshot%202024-06-17%20at%203.41.25%20PM.png)

The above dataset has 3 important parts
- Media data columns: It contains the budget allocated to different marketing channels.
- Extra feature columns: It contains data of seasonality and control variables.
- Target data column: It is the sales column (or the revenue generated column).



**Data preparation:** I've used the Custom Scaler provided by Lightweight MMM for scaling the dataset.

- Data in each column is scaled so that each one of it contributes equally to model, this ensures that one feature does not have a dominating influence on the model because of its scale. For eg. if 10x money is spent on social media in comparison to sms marketing, then it'll make the model think that the social media is more important than sms marketing without even comparing its effectiveness.

- So scaling is done to ensure that the model is not biased and the data is more comparable.


**Model Training:**
The effect of a media channel on sales could likely have a lagged effect which tapers off slowly over time. The Lightweight MMM model captures this effect and offers three different approaches. The approach that works the best will typically be the one which has the best out-of-sample fit (which is one of the generated outputs).

The 3 approaches are:

- Adstock: Applies an infinite lag that decreases its weight as time passes.

- Hill-Adstock: Applies a sigmoid like function for diminishing returns to the output of the adstock function.

- Carryover: Applies a causal convolution giving more weight to the near values than distant ones.

For this project I've used the Hill-Adstock approach after testing all three approaches as the Hill-Adstock approach offered the best out of sample fit.


Posterior distribution of media effects:

![](https://github.com/ajitjadhav10/Mix_Marketing_Modeling/blob/c19fb9294b71c943cf3c79f2fde996efa7822524/Images/Screenshot%202024-06-17%20at%204.12.09%20PM.png)



**Model Predictions:**


- True KPI vs Predicted KPI (not scaled):
![](https://github.com/ajitjadhav10/Mix_Marketing_Modeling/blob/415168dde22541b32438577d6f686dbc38bf5c94/Images/Screenshot%202024-06-17%20at%203.56.35%20PM.png)

- True KPI vs Predicted KPI (scaled):
![](https://github.com/ajitjadhav10/Mix_Marketing_Modeling/blob/415168dde22541b32438577d6f686dbc38bf5c94/Images/Screenshot%202024-06-17%20at%203.56.43%20PM.png)


**Media Insights:**

 - Baseline sales vs Effect of media.
   - About 70% of sales are baseline sales (blue region).
   - The other colors show media contribution to the remaining sales.

   ![](https://github.com/ajitjadhav10/Mix_Marketing_Modeling/blob/8d9c9322cff2d37a78c9071d3e4eb9121ff075a6/Images/download.png)


- Estimated ROI of each media channel
  -  Online Display is the most efficient channel.
  ![](https://github.com/ajitjadhav10/Mix_Marketing_Modeling/blob/b79209d2adca5290a3a212b8fd62cab856de3a2c/Images/Screenshot%202024-06-17%20at%203.57.37%20PM.png)


- Effect on KPI as marketing spending increases.
![](https://github.com/ajitjadhav10/Mix_Marketing_Modeling/blob/f0b0447dfeb7dc75349914d08fca9f0a6c9c40fe/Images/Screenshot%202024-06-17%20at%204.03.45%20PM.png)



**Budget Optimization:**
- Budget allocation before and after optimization.

![](https://github.com/ajitjadhav10/Mix_Marketing_Modeling/blob/f0b0447dfeb7dc75349914d08fca9f0a6c9c40fe/Images/Screenshot%202024-06-17%20at%204.04.02%20PM.png)


![](https://github.com/ajitjadhav10/Mix_Marketing_Modeling/blob/f0b0447dfeb7dc75349914d08fca9f0a6c9c40fe/Images/Screenshot%202024-06-17%20at%204.04.52%20PM.png)




























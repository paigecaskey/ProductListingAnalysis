# Product Listing Analysis
This project aims to develop predictive models to assist clothing resellers in accurately pricing their items, considering factors such as trendiness, brand, quality, and seasonality. By leveraging data-driven techniques, sellers, particularly those new to the platform, can optimize pricing strategies to enhance competitiveness and increase sales. With guidance on pricing, sellers can save time and effort, especially when dealing with a diverse range of items, ultimately empowering them to succeed in the resale market.
## Table of Contents
[Intro](https://github.com/paigecaskey/ProductListingAnalysis/#Intro)

[Data Gathering](https://github.com/paigecaskey/ProductListingAnalysis/#Data-Gathering)

[Exploratory Analysis](https://github.com/paigecaskey/ProductListingAnalysis/#Exploratory-Analysis)

[Predictive Model](https://github.com/paigecaskey/ProductListingAnalysis/#Predictive-Model)
## Intro
Pricing dynamics for resell items is extremely important for resellers in terms of managing stock and buying strategies. Using exploratory analysis and predictive modeling, sellers are able to strategize pricing to maximize profit. 
Data for this project was gathered using a [web scraper](https://github.com/paigecaskey/WebScraperSelenium) and cleaned in RStudio. 
The goal of this project is to empower resellers with actionable insights for pricing decisions, helping them navigate the online resale landscape. 
## Data Gathering
Data for this project was gathered using a [web scraper](https://github.com/paigecaskey/WebScraperSelenium) and cleaned in RStudio. 
### Data Key and Transforming Techniques
➔ Datetime (Continuous): Date and time the product was posted

➔ Link (Textual): Unique link to the product

  ◆ used as a unique identifier to remove duplicates
  
➔ Price (Continuous Numeric): Current,full price the item is listed for

  ◆ Removed ‘$’ symbol, making the variable fully numeric, removed outliers using z scores
  
➔ Description (Textual): Description of the product provided by seller on listing

➔ Brand: Brand of the product

  ◆ If brand was “NULL”,replaced with “None” 
  
➔ Condition (Categorical): Condition of which the product is in

  ◆ Removed values where condition was “NULL” 
  
➔ Title (Textual): Title of the product as listed by seller

  ◆ Extracted last word and made it a new categorical column called “Type”
  
➔ Size (Categorical): Size of the item

  ◆ If sizes were listed as “MultipleSizes”,it meant the seller was most likely dropshipping (buying multiple products new   from a cheaper website and reselling them for more), so binary column was created called “Dropshipping”
  
➔ Amt.Sold (Continuous Numeric): Amount of items the seller has sold in total to date

  ◆ Removed rows that did not contain the word“ Sold” (formatted wrong),then extracted the amount sold and made the value numeric
  
➔ Activity (Categorical): When the seller was most recently active on the app

➔ Recent.Review1 (Textual): The seller’s most recent customer review

➔ Time.Listed (Continuous Numeric): How long ago the product was listed

  ◆ Formatted to numeric
  
➔ Sold.and.Reviews (Textual): How many shop reviews the seller has and what their total average rating is out of 5 stars

  ◆ Converted to a numeric column, which provides the seller’s rating out of 5 stars
  
➔ Discount (Categorical): If the product offers a discount, what % off it is

  ◆ Extracted the numeric discount, equal to 0 if discount was “NULL” making the column numeric
  
➔ In.Bags (Textual): How many people’s bags the item is in currently

  ◆ Extracted the number of how many bags the item was currently in, making the variable numeric
  
➔ Like (Continuous Numeric): How many likes the item has currently (up to 99)

  ◆ If Like was “NULL” change it to 0, making it fully numeric
  
➔ Free.Shipping (Textual): If the item has free domestic shipping or not

  ◆ Changed to binary, 1 for free shipping, 0 for no free shipping
  
➔ Color (Categorical):Color of the item

➔ Material (Categorical): Material of the item/Style

➔ Style (Categorical):Style of the item

  ◆ All three style variables (Color, Material, and Style) were changed to binary and made into separate columns for each unique value they contained.
  
## Exploratory Analysis
Seller's utilization of "free shipping" as an incentive for buyers not only enhances the perceived value of the product but also contributes to increased profitability. This strategy encourages sales and also serves to maintain overall costs by adjusting the base price to offset shipping expenses. Our analysis reveals a notable trend wherein items offering free shipping command significantly higher average prices compared to those without such incentives, shown in the graph below. This underscores the effectiveness of free shipping as a marketing tool in driving consumer purchasing decisions.

<img width="620" alt="Screenshot 2024-02-20 at 11 08 43 AM" src="https://github.com/paigecaskey/ProductListingAnalysis/assets/120995805/e9776b2c-bdd8-4c84-a940-5e3e0e1991d8">

Similarly, the implementation of discounts underscores leveraging pricing dynamics to the seller's advantage is important. By initially pricing items higher and subsequently offering discounts, sellers create the illusion of a bargain for customers while effectively maintaining profit margins. This dynamic pricing strategy not only enhances customer satisfaction but also provides sellers with a competitive edge in the marketplace. This is shown in the graph below.
<img width="729" alt="Screenshot 2024-02-20 at 11 10 37 AM" src="https://github.com/paigecaskey/ProductListingAnalysis/assets/120995805/4f8bbace-4a4b-4aaa-8bbe-9809d431bd0f">

Understanding the impact of these pricing strategies is important for sellers seeking to optimize their pricing decisions, as well as remain competitve in comparision to others. By aligning pricing strategies with consumer behavior and market trends, sellers can effectively enhance their sales potential and profitability. Furthermore, insights garnered from exploratory analysis enable informed decision-making, enabling sellers to adapt their pricing strategies in response to the evolving market.

## Predictive Model
In order to construct and choose a model best fit for prediction, multiple were used to determine lowest error rate. Ridge Regression and Random forest were found to be the top two contenders, and were used interchangably in an attempt to lower error rate. Random Forest, a powerful ensemble learning technique, excels in capturing complex relationships within the data by constructing multiple decision trees. Through aggregation of predictions from these trees, the model delivers robust and accurate price predictions. Conversely, Ridge Regression, a linear regression technique, mitigates the risk of overfitting by imposing a penalty on the size of the regression coefficients, thereby enhancing generalization performance.
<img width="1177" alt="Screenshot 2023-12-17 at 2 25 41 PM" src="https://github.com/paigecaskey/ProductListingAnalysis/assets/120995805/48080fbd-c72f-4a93-8d28-810e977806ab">
Upon analysis, the Random Forest model emerges as the most accurate predictor, yielding a root mean squared error of approximately $33. Although this figure may fall short of the overall average price of $34, the majority of prediction errors stem from high-priced items, highlighting the models' limitations in capturing extreme values.

Furthermore, the Random Forest model demonstrates greater accuracy in predicting lower price values, reflecting the skewed distribution of prices within the dataset. Notably, the disparity between actual and predicted prices is more pronounced for high-priced items, indicating the need for additional data to improve model performance and address anomalies in pricing patterns.

In practical terms, minor discrepancies in predicted pricing, ranging from one to four dollars, are unlikely to significantly impact the ability to sell. Therefore, these models are best suited for non-luxury items and those priced below fifty dollars, where precise pricing accuracy may be less critical.

In summary, predictive modeling offers sellers a powerful tool for optimizing pricing strategies and enhancing competitiveness in the online resale market. By leveraging insights from Random Forest and Ridge Regression models, sellers can make informed decisions to maximize profitability and drive success in their entrepreneurial endeavors.



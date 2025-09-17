## ⛄🌀⭐ Groceries-Sales-Performance ⭐🌀⛄

Leeon is a fictional grocery detail business that operates in multiple locations, offering a diverse range of grocery products to customers. The company aims to optimize sales strategies, enhance customer experience, and increase revenue by leveraging data-driven decision-making.



## ⛄🌀⭐ Dataset Schema ⭐🌀⛄

<img width="557" height="269" alt="image" src="https://github.com/user-attachments/assets/c2d1136b-75ed-4ecb-b957-ee39479637e0" />



## ⛄🌀⭐  Dataset Overview ⭐🌀⛄

<img width="371" height="271" alt="image" src="https://github.com/user-attachments/assets/dfcb1892-8c8f-4181-af64-c91df9f18126" />



## ⛄🌀⭐ Project Goals ⭐🌀⛄ 
1. Identification of High-Performing Product Categories
The initial phase involves identifying the product categories that are generating the most significant revenue. This requires a detailed examination of sales data to pinpoint which segments are excelling and contributing most substantially to the overall financial performance of the business. Understanding these top performers is crucial for strategic planning, as it allows for the allocation of resources to areas with proven success.

2. Analysis of Key Revenue Drivers
Following the identification of top categories, it is essential to analyze the underlying factors that are driving revenue. This analysis goes beyond simple sales figures to explore the causal relationships between various business activities and financial outcomes. Such factors may include marketing campaigns, promotional events, seasonal trends, and customer demographics. A thorough understanding of these drivers provides valuable insights for optimizing future sales strategies.

3. Evaluation of Pricing Strategies and Their Sales Impact
This step involves a critical evaluation of existing pricing strategies. It's important to assess how different price points, discounts, and promotional offers affect sales volume and revenue. This evaluation should consider the elasticity of demand for various products and the competitive landscape. By understanding the direct impact of pricing on sales, we can refine our strategies to maximize profitability and market share.

4. Synthesis of Overall Insights on Sales Performance
The final step is to synthesize all the data and findings into a coherent summary. This summary should provide a holistic view of the company's sales performance, incorporating insights from the analyses of product categories, revenue drivers, and pricing strategies. The goal is to articulate actionable recommendations and strategic conclusions that can guide future business decisions and drive sustained growth. This comprehensive overview serves as a foundational document for stakeholders, informing them of the key trends and opportunities within the sales domain.



## ⛄🌀⭐ Methodology ⭐🌀⛄ 

<img width="556" height="188" alt="image" src="https://github.com/user-attachments/assets/35c4f546-9985-4f27-80d1-16499b9c6547" />



## ⛄🌀⭐ Identify the product category that generates the highest revenue ⭐🌀⛄  
Query :
```
SELECT
    categoryname,
    SUM(s.Quantity * p.Price) AS total_price_before_discount,
    SUM(s.Quantity * p.Price * s.Discount) AS total_discount,
    SUM(s.Quantity * p.Price - (s.Quantity * p.Price * s.Discount)) AS total_revenue
FROM `fsda-sql-01.grocery_dataset.sales` s
JOIN `fsda-sql-01.grocery_dataset.products` p
    ON s.ProductID = p.ProductID
JOIN `fsda-sql-01.grocery_dataset.categories` c
    ON p.CategoryID = c.CategoryID
GROUP BY categoryname
```


<img width="275" height="156" alt="image" src="https://github.com/user-attachments/assets/a06ae8de-0ff2-4d4a-bc67-0e11e037c5c9" />


Summary :
The Confections category (sweets/snacks) generates the highest revenue at 565.9 million, surpassing essential categories like Meat and Poultry. This highlights the strong consumer appeal of sweet products — even more than daily staples. 



## ⛄🌀⭐ Assess the correlation between revenue and total units sold for each product category ⭐🌀⛄  
Query :
```
SELECT
    c.categoryname,
    SUM(s.Quantity * p.Price * (1 - s.Discount)) AS total_revenue,
    SUM(s.Quantity) AS total_units_sold      
FROM `fsda-sql-01.grocery_dataset.sales` s
JOIN `fsda-sql-01.grocery_dataset.products` p
    ON s.ProductID = p.ProductID
JOIN `fsda-sql-01.grocery_dataset.categories` c
    ON p.CategoryID = c.CategoryID
GROUP BY c.CategoryID, c.categoryname
ORDER BY total_units_sold DESC
```

<img width="271" height="191" alt="image" src="https://github.com/user-attachments/assets/5c7ad9c1-bdce-4c51-82ea-6b04ef72796b" />

Summary :
There’s a strong positive correlation between total revenue and units sold — categories like Confections and Meat top both metrics. However, Poultry stands out with fewer units sold than Meat but still ranks 3rd in revenue — suggesting a higher price per unit. 



## ⛄🌀⭐ The correlation between revenue and the number of unique customers for each product category  ⭐🌀⛄  
Query :
```
SELECT
    c.CategoryName,
    SUM(s.Quantity * p.Price * (1 - s.Discount)) AS total_revenue,
    COUNT(DISTINCT s.CustomerID) AS number_of_customers
FROM `fsda-sql-01.grocery_dataset.sales` s
JOIN `fsda-sql-01.grocery_dataset.products` p
    ON s.ProductID = p.ProductID
JOIN `fsda-sql-01.grocery_dataset.categories` c
    ON p.CategoryID = c.CategoryID
GROUP BY c.CategoryName
ORDER BY number_of_customers DESC

```


Summary :
Confections and Meat not only generate the highest revenue but also attract the most unique customers — proving their wide consumer appeal. Interestingly, Shell Fish and Seafood have a similar number of customers, yet Shell Fish brings in much higher revenue — indicating high-value purchases from loyal buyers. 



## ⛄🌀⭐ Calculate the average price per unit for each product category ⭐🌀⛄  
Query :
```
SELECT
    c.CategoryName,
    AVG(p.price) AS avg_price_per_unit
FROM `fsda-sql-01.grocery_dataset.products` p
JOIN `fsda-sql-01.grocery_dataset.categories` c
    ON p.CategoryID = c.CategoryID
GROUP BY c.CategoryName
ORDER BY avg_price_per_unit DESC
```


<img width="270" height="244" alt="image" src="https://github.com/user-attachments/assets/53eec875-c43d-4f54-a178-2deee8b840f3" />


Summary :
The product category with the highest average price per unit is Grain — surprising for a staple often seen as inexpensive. Meanwhile, Shell Fish, typically considered a luxury item, has the lowest average price per unit. 


## ⛄🌀⭐ License ⭐🌀⛄ 
- Copyright by Diantya Pitaloka

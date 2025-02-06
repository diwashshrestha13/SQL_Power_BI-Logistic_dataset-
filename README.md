# Logistic-Dashboard


## Problem Statement

The dashboard presented helps the company to understand three key business operations, Delivery Performance, Customer Management, and Logistic Insights. The company has data from 1971 to 2019 which includes deliveries, customer information, and revenue.

The customer has failed to deliver 50% of it's deliveries, which has decreased it's earning potential, with the company only making more money than due from it's customer in 2017. Besides, it also has a poor membership retention rate of 10.5%. The dashboard aims to provide insights in the areas the company can make improvements from it's type of service, delivery status, and shipping domain and reduce it's service to most profitable. 


### Steps followed 

- Data Collection
Gathered 7 Excel files containing raw business data.

- Data Import to SQL

Loaded the Excel files into SQL database tables.

Standardized data formats and optimized structure for querying.
- Data Analysis in SQL

Wrote SQL queries to derive insights, understand the data, and answer business questions.
Applied aggregations, joins, and filters to extract key metrics.
- Data Load to Power BI

Established a connection between SQL and Power BI by importing and structuring the data for visualization.
- Data Modeling
- Using 3 dimensions table, 4 facts table (including a created date table), and a bridge table joining employee and shipment. 

![Image](https://github.com/user-attachments/assets/bf068c83-f2d8-411e-aee6-4f965e0b27d2)

Created relationships between tables.
- Built a Calendar Table for time-based analysis (date filtering, YTD, MTD calculations).

- Dashboard & Metrics

Designed a Power BI dashboard with key insights and visuals separted into 3 dashboard.
- Created DAX measures for KPIs like average KPI's, cumilative earnings, ratios, filters.
           
- Cumulative earnings received were calculated using DAX and visualized in a line chart over the years to visualize the year company's earning against the due sum from customers. 
- A bar chart comparing orders delivered and orders pending to understand the year the company performance trend. 
- A stacked column chart to understand the category, in which the company made the highest revenue but also which industry the company failed to receive payment from. 

Some examples of the DAX measure used usage. 

for creating cumulative paid received measures following DAX expression was written;
       
       cumulativepaid = CALCULATE(
                      SUM(payment_details[Paid_Column]), 
               'CALENDAR'[Date] <= MAX('CALENDAR'[Date])) 
               
line graph: 

![Image](https://github.com/user-attachments/assets/e23fa154-3183-4d12-80a0-3dd232f49c11)

        


- Following DAX expression was to ensure that the Active Member Count is affected only by the year selection on the right side of the slider (and not the left)
        
        CumulativeMembers = 
            VAR MaxDate = MAX('CALENDAR'[Date])
        RETURN 
            CALCULATE(
            COUNT('membership'[MembershipStatus]), 
        FILTER(
            ALL('CALENDAR'),
            'CALENDAR'[Date] <= MaxDate
                )
            )
        
A card visual was used to represent the count of active members.

![Image](https://github.com/user-attachments/assets/cefaee4e-eee7-4824-b4cc-f11806fa6fb3)

        

 
- Following Dax was used to find the average time it took to complete a delivery.
 
         AverageDeliveryMonth = 
            VAR CompletedDelivery = 
                COUNTROWS(FILTER
                (
                'status', 'status'[Current_Status] = "Delivered")
                )
            RETURN
        SUM('status'[Date_Difference])/ [Delivery Completed]
 
 A card visual was used to represent this average.

![Image](https://github.com/user-attachments/assets/278346d8-7104-485c-90e6-c7bb643babd8)


 
A new measure was created to calculate the average price per weight and shipment charge. 

 
         AvgShipmentCharge = 
                VAR totalcharge = SUM(shipment_details[SH_CHARGES])
                VAR totalshipment = COUNTROWS(shipment_details)
            RETURN
        DIVIDE(totalcharge, totalshipment,0) 

A card visual was used to represent these KPI.
 
 
![Image](https://github.com/user-attachments/assets/3eebb89b-3af7-43ed-9365-f99403d9c369)



 # Bookmark was used for buttons to easily navigate within the dashboard.

 
![Image](https://github.com/user-attachments/assets/a6b9bd90-6d79-4e4b-aa21-cc1552aa2bdc)
 # The report was then published to Power BI Service.
 # Report Snapshot (Power BI DESKTOP)

![Image](https://github.com/user-attachments/assets/c1c01bfe-d21d-4738-b5e5-3f994b0dced0)

![Image](https://github.com/user-attachments/assets/4c1b9c22-3272-400f-88d9-2814e8a9a1c7)

![Image](https://github.com/user-attachments/assets/0e19264e-ebf3-4ed3-8000-8459e4428211)

# Insights

Following inferences can be drawn from the dashboard;

### [1] Total Number of orders = 200
    most penidngs are between 1975-1985 and 2005-2015.
   Number of orders fulfilled = 100 (50 %)

   Number of orders pending = 100 (50 %)

           
### [2] Earnings

    Cumulative earning in 2017 = $4,651,927
    Present Payment Due = $4,645,041
   
The company's earnings received only reached higher than pending earnings due to failed delivery in 2017

  
  ### [3] Revenue per Category  
  
      a) Construction - $1.19 million
      b) Healthcare- $0.7 million (Highest earned)
      c) Construction- $0.6 (Highest Due)
The value will change based on the filter selected. 

 ### [4] Some other insights based on filters 
 
 ### Shipping Domain
 1.1) $2.57 Million Earned from International of 91 shipments.
 
 1.2) $2.28 Million Earned from Domestic of 109 shipments.
 
 1.3) $102 Express Shipment / 98 Express Shipment 

 1.4) The company has the highest revenue from International        Express Shipment $1.30 million and the least  from domestic express, an earning of $988k
 
         thus, the company must look more into international express shipment. 
 
 ### Customer Insights
 
 2.1)  12.77 % retention rate, 12 Active members, and 87 customers among whom 45 paid prefer card payment.
 
 2.2)  8.49 % retention rate, 9 Active members, 98 customers among whom 55 paid for cash on delivery.
 
 2.3)  Most of the paid customers came between 1994-2019 - 65 (second half of business life) than first half - 37 (first half of business)
 
 2.4)  The highest earnings came from wholesale customers preferring cash on delivery who also had a higher retention rate of 14.81% with equal preference for card payment and cash on delivery.
         Although the membership retention rate is good for customers who prefer card payment, most of the revenue comes from cash on delivery, so the company could focus more on cash on delivery who are wholesale members if the goal is to increase revenue.
         

### Some Business Questions Solved through SQL Query
How are customers divided based on the payment mode?

![Image](https://github.com/user-attachments/assets/b5689c41-2c88-47c4-95e6-767c0f340cc5)


What is the number of employees for each designation?

![Image](https://github.com/user-attachments/assets/ffeffae9-f20e-426a-9025-f5e7ddc63894)


What is the delivered percentage for each employee designation?

![Image](https://github.com/user-attachments/assets/7b4a9e69-4ff0-4813-a0d7-cd5095433e29)


Which Customer ID / Member ID has been the member for the longest?

![Image](https://github.com/user-attachments/assets/d5b6120c-a777-4c2a-8e1e-feab7b56f87e)


Cumulative column of Undelivered status over the years

![Image](https://github.com/user-attachments/assets/5bf60aaa-bc24-412c-8e29-567fdfa1361e)

Which customer paid the highest shipment charge?

![Image](https://github.com/user-attachments/assets/bd7f40fb-cf73-4dd1-b52a-13350218f983)



Name of the customer with highest payment due in California?
![Image](https://github.com/user-attachments/assets/ac1053a1-4022-48b4-9ce7-dee0bacfe879)

Dateset Used: https://www.kaggle.com/datasets/aashokaacharya/logistics-company-dataset-for-sql

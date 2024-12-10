
# I. Cleaning

## 1. Olist customers_dataset
- Check column quality

![image](https://github.com/user-attachments/assets/91c79fe2-4fa1-4b61-b5ed-3eb0ab5d165b)

- Rename Column

  ![image](https://github.com/user-attachments/assets/789b000d-fc96-42ae-938f-2cc63cf9d6a8)

- Capitalize Each Letter in the City Column

![image](https://github.com/user-attachments/assets/88337008-314e-4b33-9a85-c4c8740d172b)

## 2. Olist geolocation_dataset
- Check column quality

  ![image](https://github.com/user-attachments/assets/f76e2819-15e6-4459-92c0-7d19c54512ad)
- Remove unesscary columns

![image](https://github.com/user-attachments/assets/f774c6c0-2c31-4420-939f-1badd352f2cc)

- Remove duplicate
- Rename columns
- 
![image](https://github.com/user-attachments/assets/437121f0-60b6-4324-a1e7-4054cab2c01b)

## 3. Olist_orders_dataset
- Check column quality
![image](https://github.com/user-attachments/assets/81008a64-927d-4dc7-9497-509ca8227bd8)![image](https://github.com/user-attachments/assets/13dbc9b8-90c8-4736-905c-d06c447cdff9)

- Add Day of Week column of order_purchase_timestamp column

![image](https://github.com/user-attachments/assets/070b34d8-8618-44c8-979e-c3946a10039d)

- Add custom column Weekend/ Weekday

 ![image](https://github.com/user-attachments/assets/0576d6a1-83ee-4477-8c30-b679ae08b5b1)

## 4. Olist_order_items_dataset
- Check column quality
![image](https://github.com/user-attachments/assets/2a9b528d-617b-4d96-a712-f46cc8b0542d)![image](https://github.com/user-attachments/assets/73dd29cb-13c2-4a1e-bb9e-b6d524ba2dd0)


## 5. Olist_order_payment dataset
- Check column quality
![image](https://github.com/user-attachments/assets/1a574fae-1a48-4902-aa7a-cc59c77ce8de)

## 6. Olist_order_review_dataset
- Check column quality
  
![image](https://github.com/user-attachments/assets/0cf8ee39-1982-49b7-a67a-cce5da3e3a50)


## 7. Olist_sellers_dataset
- Check column quality

  ![image](https://github.com/user-attachments/assets/b058b10f-4337-4cf6-a745-6ac608de53fa)

- Rename columns

  ![image](https://github.com/user-attachments/assets/433102c3-ebd2-4f4e-93df-fb9cceabc610)

- Filter wrong values

![image](https://github.com/user-attachments/assets/0b0670ae-ff8e-49a2-b00d-e1a03602833f)

## 8. Olist_products_dataset
- Check column quality

  ![image](https://github.com/user-attachments/assets/30d05006-bf59-428d-9eeb-0408a0f482e8)![image](https://github.com/user-attachments/assets/c14731de-da5c-4ad8-9e0e-013c73ad8951)
- Left join with Category table to get english name of Product

  ![image](https://github.com/user-attachments/assets/1822a752-0b1d-4d22-98d7-0a9486ab22b1)

## 9. Olist_product_category_name_translation
- Check column quality
  
![image](https://github.com/user-attachments/assets/84cf928f-ca33-4c2c-9c83-b1c3a264a56f)

- Use first row as header
  
![image](https://github.com/user-attachments/assets/ab9e762b-7231-4826-af1c-b9d761b9da1e)
# III. Dax and measure
---

### Add a new column "Review score" to the `olist_order_items_dataset` table:
```DAX
Review score = 
CALCULATE(
    AVERAGE(olist_order_reviews_dataset[review_score]),
    FILTER(
        olist_order_reviews_dataset,
        olist_order_reviews_dataset[order_id] = olist_order_items_dataset[order_id]
    )
)
```

---

### Add a column "Comment" to the `olist_order_reviews_dataset` table (indicates whether the order has a comment):
```DAX
Comment = if(olist_order_reviews_dataset[review_comment_message] = "", "No Comment", "Comment")
```

---

### Extract "Month" and "Year" from the `order_delivered_customer_date` column in the `olist_orders_dataset` table:
```DAX
Month delivered customer date = MONTH(olist_orders_dataset[order_delivered_customer_date])
Year delivered customer date = YEAR(olist_orders_dataset[order_delivered_customer_date])
```

---

### Extract "Hour" from the `order_purchase_timestamp` column in the `olist_orders_dataset` table:
```DAX
Hour purchase timestamp = HOUR(olist_orders_dataset[order_purchase_timestamp])
```

---

### Add a column to calculate the total time each order took to reach the customer:
```DAX
Total received time = DATEDIFF(olist_orders_dataset[order_purchase_timestamp], olist_orders_dataset[order_delivered_customer_date], DAY)
```

---

### Number of orders:
```DAX
Orders = COUNT(olist_orders_dataset[order_id])
```

---

### Number of products:
```DAX
Products = COUNT(olist_order_items_dataset[product_id])
```

---

### Number of orders with review comments:
```DAX
Comment orders = CALCULATE(COUNT(olist_order_reviews_dataset[order_id]), olist_order_reviews_dataset[Comment] = "Comment")
```

---

### Average review score:
```DAX
Avg of review score = DIVIDE(SUM(olist_order_items_dataset[Review score]), COUNT(olist_order_items_dataset[Review score]))
```

---

### Number of orders in the previous month:
```DAX
Orders_previous_month = 
CALCULATE(
    [Orders],
    FILTER(
        ALLSELECTED(olist_orders_dataset),
        (
            MAX(olist_orders_dataset[Month delivered customer date]) = 1 &&
            olist_orders_dataset[Year delivered customer date] = MAX(olist_orders_dataset[Year delivered customer date]) - 1 &&
            olist_orders_dataset[Month delivered customer date] = 12
        ) ||
        (
            MAX(olist_orders_dataset[Month delivered customer date]) > 1 &&
            olist_orders_dataset[Year delivered customer date] = MAX(olist_orders_dataset[Year delivered customer date]) &&
            olist_orders_dataset[Month delivered customer date] = MAX(olist_orders_dataset[Month delivered customer date]) - 1
        )
    )
)
```

---

### Growth percentage of orders compared to the previous month:
```DAX
Growth percentage of order = DIVIDE([Orders] - [Orders_previous_month], [Orders_previous_month])
```

---

### Conditional formatting for growth percentage:
```DAX
Cond growth percentage of order = IF([Growth percentage of order] < 0, 1, IF(ISBLANK([Growth percentage of order]), 0, 2))
```

---

### Rank product categories by the number of sold items:
```DAX
Category Rank = 
RANKX(
    ALL(olist_products_dataset[product_category_name_english]), -- Ignore filter context
    [Orders], -- Calculate total sold items for each category
    , -- No secondary sorting criteria, defaults to ascending order
    DESC, -- Sort in descending order
    DENSE -- Dense ranking style (1, 2, 3,…)
)
```

---

### Total revenue:
```DAX
Total Revenue = SUM(olist_order_items_dataset[price])
```

---

### Number of customers:
```DAX
Customers = DISTINCTCOUNT(olist_customers_dataset[customer_id])
```

---

### Add a column to indicate whether the delivery was on time or late in the `olist_orders_dataset` table:
```DAX
On time/ Late = IF(olist_orders_dataset[order_delivered_customer_date] > olist_orders_dataset[order_estimated_delivery_date], "Late", "On time")
```
# II. Data Schema
The data is divided in multiple datasets for better understanding and organization.

![image](https://github.com/user-attachments/assets/06db6c00-2623-4c25-bc58-2531baeb610b)

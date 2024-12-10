# Brazilian-E-Commerce-Dashboard

<div align="center">
  <img src="https://github.com/user-attachments/assets/fdbffd46-4f92-47c7-8f00-d9bfb3d29fcf" alt="mô tả" width="1000">
</div>

# I. Dataset Introduction

The **Brazilian E-Commerce Public Dataset by Olist** is a real-world dataset containing information on nearly 100,000 orders placed on the Olist Store, a fashion-focused e-commerce platform, between 2016 and 2018 across various markets in Brazil.

The Olist Store has garnered over 10 million registrations since its launch in Europe in 2009, subsequently expanding globally. The platform includes features such as order status tracking, price viewing, payment processing, shipping performance analysis for customer locations, product attributes, and customer-written reviews.

The dataset includes comprehensive information such as:  
- User information  
- Buyer distribution by country  
- Seller comparison metrics by gender and country  
- Top sales by country  

You can learn more about and download the dataset here: [https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

# II. Goal
The goal of the Power BI exercise is to analyze the business performance of the Olist Store e-commerce site.

- Analyze the overall business situation.
- Analyze revenue and business products.
- Analyze orders.
- Analyze transactions.
- Analyze order shipping performance.
- Analyze customer feedback.
# III. Cleaning
Dataset has information of nearly 100.000 orders placed on Olist website and contains 9 tables: 
- Olist customers_dataset: This dataset has information about the customer and its location. Use it to identify unique customers in the orders dataset and to find the orders delivery location.
- Olist geolocation_dataset: This dataset has information Brazilian zip codes and its lat/lng coordinates.
- Olist_orders_dataset: This is the core dataset of the project.
- Olist_order_items_dataset: This dataset includes data about the items purchased within each order.
- Olist_order_payment dataset: This dataset includes data about the orders payment options.
- Olist_order_review_dataset: This dataset includes data about the reviews made by the customers.
- Olist_sellers_dataset: This dataset includes data about the sellers that fulfilled orders made at Olist.
- Olist_products_dataset: This dataset includes data about the products sold by Olist.
- Olist_product_category_name_translation: This dataset translates the product_category_name to english.
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

# IV. Data Schema
The data is divided in multiple datasets for better understanding and organization.

![image](https://github.com/user-attachments/assets/06db6c00-2623-4c25-bc58-2531baeb610b)

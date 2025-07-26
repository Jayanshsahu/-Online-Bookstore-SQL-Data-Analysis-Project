                                                  📚 -Online-Bookstore-SQL-Data-Analysis-Project




📌 Project Overview

                This project simulates an online bookstore's database system, focusing on 
                managing books,customer information, and order history. The project involves
                creating and populating SQL tables,performing data queries, and conducting comprehensive
                analysis to extract key business insights using PostgreSQL #SQL #DataAnalysis #Bookstore



🎯 Objective

                The aim of this project is to:

                Design and create a relational database for an online bookstore.

                Import real-world structured data into tables.

                Use SQL queries to derive useful insights for business decisions like revenue tracking, 
                customer behavior, inventory management, and sales performance.



🗂️ Database Schema
                The project includes the following 3 primary tables:


           📘 Books                                               👤 Customers                                   🛒 Orders
    | Column          | Description              |    | Column       | Description          |     | Column        | Description                  | 
    | --------------- | ------------------------ |    | ------------ | -------------------- |     | ------------- | ---------------------------- |
    | Book\_ID        | Primary Key              |    | Customer\_ID | Primary Key          |     | Order\_ID     | Primary Key                  |
    | Title           | Name of the book         |    | Name         | Customer name        |     | Customer\_ID  | Foreign key (Customers)      |
    | Author          | Book author              |    | Email        | Email address        |     | Book\_ID      | Foreign key (Books)          |
    | Genre           | Fiction, Fantasy, etc.   |    | Phone        | Phone number         |     | Order\_Date   | Date of the order            |
    | Published\_Year | Year of publication      |    | City         | City of residence    |     | Quantity      | Units purchased              |
    | Price           | Cost per unit            |    | Country      | Country of residence |     | Total\_Amount | Price × Quantity (per order) |
    | Stock           | Available stock quantity |         


<img width="338" height="239" alt="T  135930" src="https://github.com/user-attachments/assets/e831a33d-b975-42be-814c-c56d1403509e" />
<img width="622" height="251" alt="T 140100" src="https://github.com/user-attachments/assets/2c5e04a8-19cb-41fa-8757-b74b8409aad1" />
<img width="658" height="250" alt="T 140227" src="https://github.com/user-attachments/assets/b83089f5-c805-4d2f-bb44-e420791a8b2c" />


📥 Data Import
       Data was imported using the COPY command from CSV files (Books, Customers, Orders) using this format:
       COPY Books(Book_ID, Title, Author, Genre, Published_Year, Price, Stock)
       FROM 'your_path/Books.csv' CSV HEADER;


📊 Key SQL Queries and Insights


🧠 Advanced Insights

    1 Total books sold per genre
     
                    SELECT Genre, SUM(Quantity) AS Total_Books_Sold
                    FROM Orders o
                    JOIN Books b ON o.Book_ID = b.Book_ID
                    GROUP BY Genre;

              
 <img width="218" height="166" alt="1  133356" src="https://github.com/user-attachments/assets/c54b8705-6092-4848-918b-1ad18290eeb1" />



    2 Average price of Fantasy books

     
                   SELECT AVG(Price) FROM Books WHERE Genre = 'Fantasy';

                  
    3 Customers with at least 2 orders
                  SELECT c.Name, COUNT(*) AS Order_Count
                  FROM Orders o
                  JOIN Customers c ON o.Customer_ID = c.Customer_ID
                  GROUP BY c.Customer_ID, c.Name
                  HAVING COUNT(*) >= 2;

                  
<img width="229" height="200" alt="3  133323" src="https://github.com/user-attachments/assets/1041c795-be00-44ce-ad71-82e233a02861" />



   4  Most frequently ordered book
                  
                    SELECT b.Title, COUNT(*) AS Order_Count
                    FROM Orders o
                    JOIN Books b ON o.Book_ID = b.Book_ID
                    GROUP BY b.Title
                    ORDER BY Order_Count DESC
                    LIMIT 1;


                    



   5  Books sold by each author

                    SELECT Author, SUM(Quantity) AS Total_Sold
                    FROM Orders o
                    JOIN Books b ON o.Book_ID = b.Book_ID
                    GROUP BY Author;

                    
<img width="550" height="112" alt="5  133209" src="https://github.com/user-attachments/assets/87dd033e-59e2-492c-9c38-51b94ecca20b" />


   6  Cities where customers spent over $30
                    SELECT DISTINCT City
                    FROM Orders o
                    JOIN Customers c ON o.Customer_ID = c.Customer_ID
                    WHERE o.Total_Amount > 30;

                    
<img width="208" height="253" alt="7  132432" src="https://github.com/user-attachments/assets/5282f62f-a916-4fc2-9a91-d5dd15eb8208" />



   7  Top spending customer      
     
                    SELECT c.Name, SUM(o.Total_Amount) AS Total_Spent
                    FROM Orders o
                    JOIN Customers c ON o.Customer_ID = c.Customer_ID
                    GROUP BY c.Name
                    ORDER BY Total_Spent DESC
                    LIMIT 1;

                    
<img width="208" height="253" alt="7  132432" src="https://github.com/user-attachments/assets/2b36090b-269e-4bc1-9fc7-680be9e75026" />



     8  Remaining stock after all orders

                    SELECT b.Title, b.Stock - COALESCE(SUM(o.Quantity), 0) AS Remaining_Stock
                    FROM Books b
                    LEFT JOIN Orders o ON b.Book_ID = o.Book_ID
                    GROUP BY b.Book_ID;

                    
<img width="449" height="236" alt="9 132346" src="https://github.com/user-attachments/assets/57c3428b-d79c-4031-ac4a-bee52e5119b3" />




🔎 Basic Queries

  All Fiction books
  
            SELECT * FROM Books WHERE Genre = 'Fiction';

        
Books published after 1950

          SELECT * FROM Books WHERE Published_Year > 1950;
          
          
Customers from Canada

          SELECT * FROM Customers WHERE Country = 'Canada';



📦 Inventory & Sales Insights

         Total books in stock
         
                SELECT SUM(Stock) AS Total_Stock FROM Books;

                
         Revenue generated       

                SELECT SUM(Total_Amount) AS Revenue FROM Orders;


         Top 3 most expensive Fantasy books

                SELECT * FROM Books WHERE Genre = 'Fantasy' ORDER BY Price DESC LIMIT 3;



📌 Key Takeaways
                    Database Design: Learned to structure an efficient relational database using foreign keys.

                    Data Integration: Imported and mapped real-world book, customer, and order data.

                    SQL Skills: Practiced filtering, joining, grouping, and subquery writing.

                    Business Insight Extraction: Simulated e-commerce analytics from sales and inventory data.

                    Decision Support: Provided data-driven insights like revenue, customer behavior, and product trends.
                

💊 Pharmaceutical Inventory Management System (PharmaDB)

PharmaDB is a comprehensive software application designed to streamline the management of suppliers, medicine categories, medicines, sales, and purchase orders within a pharmacy. It features a full-featured dashboard built with Streamlit and backed by a robust MySQL database.

This application not only serves as a practical inventory tool but also as a technical demonstration of advanced database concepts, including triggers, stored procedures, functions, role-based views, and efficient backend connection pooling.


✨ Features

Analytics Dashboard: A visual overview of key metrics (total medicines, suppliers, customers), total sales (₹), and total stock value (₹). Includes interactive charts for "Daily Revenue Trend" and "Revenue by Medicine Category".

Full CRUD Operations: Complete Create, Read, Update, and Delete functionality for:

Medicines

Suppliers

Customers

Order Management: A cart-based system for creating and managing:

Sales Orders: Automatically deducts from Medicine.StockQty upon sale.

Purchase Orders: Automatically adds to Medicine.StockQty upon receiving.

Trigger Sandbox (Live Demo): A dedicated page to demonstrate the database triggers in real-time. Simulate a sale and watch the trg_low_stock_alert and trg_resolve_stock_alert triggers automatically create and resolve entries in the Stock_Alert table.

Stored Procedures Demo: An interactive interface to execute the GetMedicineDetailsByCategory stored procedure directly from the app.

Role-Based Views: A simulator to show how different database views (Available_Medicines_View, Customer_Order_History_View, Supplier_Purchase_History_View) can provide simplified, secure data access for different roles (Pharmacist, Customer, Supplier).

Advanced Database Backend: Utilizes a robust backend.py with a MySQL connection pool (mysql.connector.pooling) for efficient, stable, and scalable database interactions.

🛠️ Technologies Used

Frontend: Streamlit, Plotly, Pandas

Backend: Python

Database: MySQL

Python Libraries: mysql-connector-python, python-dotenv

🗄️ Database Schema & Logic

This project is a DBMS-first application, demonstrating complex database-level logic.

Normalized Tables: A relational schema with tables for Medicine, Category, Supplier, Customer, Purchase_Order, Purchase_Item, Sales_Order, Sales_Item, Stock_Alert, and Prescription.

Triggers:

trg_low_stock_alert: Automatically creates an alert in Stock_Alert when a medicine's StockQty drops to or below its ReorderLevel during a sale.

trg_resolve_stock_alert: Automatically marks a Stock_Alert as Resolved = TRUE when stock is replenished above the ReorderLevel.

trg_pi_* (insert/update/delete): A set of triggers to manage stock levels and update Purchase_Order totals when purchase items are modified.

trg_si_* (insert/update/delete): A set of triggers to manage stock levels (decrementing) and update Sales_Order totals when sales items are modified.

Stored Procedures:

GetMedicineDetailsByCategory(IN category_name): A procedure that efficiently queries and returns all medicines belonging to a specific category name.

Functions:

GetStockValue(): A function that calculates and returns the total monetary value of all medicine currently in stock (SUM(StockQty * Price)).

Views:

Available_Medicines_View: A simplified view for customers, showing only medicine names, prices, and categories.

Customer_Order_History_View: Joins sales data to show a complete order history for customers.

Supplier_Purchase_History_View: Joins purchase data to show a complete purchase order history for suppliers.

🚀 Setup and Installation

Follow these steps to run the project locally:

1. Clone the Repository

git clone [https://github.com/PES1UG23AM069/PharmaDB.git](https://github.com/PES1UG23AM069/PharmaDB.git)
cd your-repo-name


2. Set Up the Database

Ensure you have a MySQL server running (e.g., via XAMPP, WAMP, or a standalone service).

Create a new database. The project report uses PharmaDB.

CREATE DATABASE PharmaDB;


Import the database schema, data, triggers, and procedures using the PharmaDB.sql file. You can use a tool like MySQL Workbench or run the following command:

mysql -u your_mysql_user -p PharmaDB < PharmaDB.sql


3. Set Up Environment Variables

Create a file named .env in the root directory of the project.

Add your database credentials to this file:

DB_HOST=localhost
DB_PORT=3306
DB_USER=your_mysql_user
DB_PASSWORD=your_mysql_password
DB_NAME=PharmaDB


Note: The backend.py file will load these variables.

4. Install Dependencies

It is highly recommended to use a Python virtual environment:

python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`


Install the required packages from requirements.txt:

pip install -r requirements.txt


5. Run the Application

With your virtual environment active, run the Streamlit app:

streamlit run app.py


Open your web browser and navigate to the local URL provided by Streamlit (usually http://localhost:8501).

🧑‍💻 Authors

Ritvik S - (PES1UG23AM085)

ARYAN S - (PES1UG23AM069)

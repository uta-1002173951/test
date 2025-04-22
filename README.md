##### OrganicMarket Product Management
This project is a Flask-based web application for managing products in the OrganicMarket database. It allows users to add, view, and delete products, as well as generate various reports on sales, revenue, and customer loyalty.
Prerequisites

Python 3.x
MySQL (e.g., XAMPP for local development)
Flask (pip install flask)
MySQL Connector for Python (pip install mysql-connector-python)

Installation

Clone or download this repository to your local machine.

Install the required Python packages:
pip install flask mysql-connector-python


Ensure MySQL is running (e.g., via XAMPP).


Database Setup

Start your MySQL server (e.g., through XAMPP).

Create the database and table using the following SQL commands:
CREATE DATABASE OrganicMarket;
USE OrganicMarket;

CREATE TABLE products (
id INT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(100) NOT NULL,
price DECIMAL(10, 2) NOT NULL,
quantity INT NOT NULL
);

CREATE TABLE vendor (
vId INT PRIMARY KEY,
Vname VARCHAR(100),
Address VARCHAR(255)
);

CREATE TABLE item (
iId INT PRIMARY KEY,
Iname VARCHAR(100),
Sprice DECIMAL(10, 2),
Category VARCHAR(50)
);

CREATE TABLE vendor_item (
vId INT,
iId INT,
PRIMARY KEY (vId, iId),
FOREIGN KEY (vId) REFERENCES vendor(vId),
FOREIGN KEY (iId) REFERENCES item(iId)
);

CREATE TABLE store_item (
sId INT,
iId INT,
StockCount INT,
PRIMARY KEY (sId, iId),
FOREIGN KEY (iId) REFERENCES item(iId)
);

-- Additional tables for reports (example structure)
CREATE TABLE ItemSalesSummary (
Iname VARCHAR(100),
TotalRevenue DECIMAL(10, 2),
TotalQuantitySold INT
);

CREATE TABLE TopLoyalCustomers (
Cname VARCHAR(100),
LoyaltyScore DECIMAL(3, 1)
);


Update the db_config in app.py with your MySQL credentials if needed (default uses root with no password).


Running the Application

Navigate to the project directory in your terminal.

Run the Flask app:
python app.py


Open your browser and go to http://127.0.0.1:5000/ to access the application.


Features
1. Add Product
Input fields for product name, price, and quantity.








Currently supports adding "Almond Nuts" (hardcoded for specific requirements: iId=101, vId=201, storeId=1).
Inserts data into vendor, item, vendor_item, and store_item tables.

2. View Products










Displays a list of products with their name, price, and quantity.
Fetches data from the database and renders it on the frontend.

3. Delete Product















Allows deletion of a product by its ID.
Removes related data from store_item, vendor_item, item, and vendor tables (if the vendor has no other items).

4. Reports













Top 3 Revenue-Generating Items: Lists the top 3 items by revenue.
Items Sold More Than 50 Units: Shows items with sales exceeding 50 units.
Top Loyal Customer: Displays the customer with the highest loyalty score.
Loyal Customers (Score 4–5): Lists customers with loyalty scores between 4 and 5.
Total Revenue: Shows the total revenue from all sales.
List All Products: Displays all products in the store.

File Structure

app.py: Main Flask application with routes for adding, viewing, deleting products, and generating reports.
templates/index.html: Frontend HTML file with a form to add products, a product list, and links to reports.
templates/*.html: Additional templates for rendering reports (products.html, top_revenue.html, etc.).

Notes

The application uses Flask for the backend and MySQL for the database.
The frontend uses basic HTML and JavaScript for interacting with the Flask API.
Ensure your MySQL server is running before starting the app.
The database configuration in app.py assumes a local MySQL setup with the default XAMPP credentials (root, no password).

Troubleshooting

If you encounter a database connection error, verify your MySQL credentials in db_config and ensure the server is running.
Ensure the required tables are created in the database before running the app.
If the app fails to load, check the Flask console for error messages.

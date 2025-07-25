Step-by-Step Documentation for Database Setup
Step 1: Creating the Database
Open phpMyAdmin or any database management tool.
Create a new database named ecommerce.
Run the following SQL commands to create the necessary tables:
Cart Table

CREATE TABLE cart (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
Products Table

CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    description TEXT,
    image VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
Users Table

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    role ENUM('user', 'admin') DEFAULT 'user'
);
Step 2: Setting Up db.php
Create a folder named includes in your project directory.
Inside this folder, create a file named db.php.
Add the following code:
db.php

<?php
$host = 'localhost';
$dbname = 'ecommerce';
$user = 'root';
$password = '';

try {
    $conn = new PDO("mysql:host=$host;dbname=$dbname", $user, $password);
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
?>
Explanation:

This script uses the PDO (PHP Data Objects) method for connecting to the database.
If the connection fails, an error message will be displayed.
Step 3: Testing the Database Connection
Create a new file named test_db.php in the root folder.
Add the following code to test the connection:
test_db.php

<?php
include 'includes/db.php';

if ($conn) {
    echo "Database connected successfully!";
} else {
    echo "Failed to connect to the database.";
}
?>
Access http://localhost/ecommerce/test_db.php in your browser.
Ensure the message "Database connected successfully!" is displayed.
Next Steps
Once the database is set up:

Move to the Registration Page (register.php) so users can create accounts.
Build the Login Page (login.php) to authenticate users.
Proceed to dynamic pages like index.php.

Requests 21 
    SELECT * FROM files 
    WHERE user_id = 1;

    DELETE FROM files 
    WHERE id = 1;

    UPDATE files 
    SET file_name = 'new_file_name.txt' 
    WHERE id = 1;

    CREATE USER 'new_user'@'localhost' IDENTIFIED BY 'password';

    DELIMITER $$
    CREATE PROCEDURE add_user(
        IN p_username VARCHAR(50), 
        IN p_email VARCHAR(100), 
        IN p_password VARCHAR(255)
    )
    BEGIN
        INSERT INTO users (username, email, password) 
        VALUES (p_username, p_email, p_password);
    END $$
    DELIMITER ;

    CALL add_user('jane_doe', 'jane@example.com', 'securepassword');

    ALTER TABLE users 
    ADD CONSTRAINT unique_username UNIQUE (username);

    CREATE INDEX idx_email ON users(email);

    SELECT p.name, SUM(o.quantity) AS total_quantity 
    FROM products p 
    JOIN customer_orders o ON p.id = o.product_id 
    GROUP BY p.name;

    SELECT u.username, COUNT(o.id) AS order_count 
    FROM users u 
    LEFT JOIN customer_orders o ON u.id = o.user_id 
    GROUP BY u.username 
    ORDER BY order_count DESC;

    SELECT username FROM users WHERE status = 'active'
    UNION
    SELECT username FROM users WHERE created_at < '2022-01-01';

    SELECT NOW();

    SELECT CURRENT_DATE;

    SELECT DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%s');

    SHOW COLUMNS FROM users LIKE 'email';



Requests 22 
   CREATE DATABASE my_database;

   USE my_database;

   DROP DATABASE my_database;


   CREATE TABLE users (
       id INT AUTO_INCREMENT PRIMARY KEY,
       username VARCHAR(50) NOT NULL UNIQUE,
       email VARCHAR(100) NOT NULL,
       password VARCHAR(255) NOT NULL,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );


   CREATE TABLE orders (
       id INT AUTO_INCREMENT PRIMARY KEY,
       user_id INT,
       product_id INT,
       quantity INT NOT NULL,
       total DECIMAL(10, 2) NOT NULL,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
       FOREIGN KEY (user_id) REFERENCES users(id),
       FOREIGN KEY (product_id) REFERENCES products(id)
   );

   CREATE INDEX idx_users_username ON users(username);

   DROP TABLE IF EXISTS products;

   ALTER TABLE users ADD COLUMN phone VARCHAR(15);


    RENAME TABLE orders TO customer_orders;

    INSERT INTO users (username, email, password) 
    VALUES ('john_doe', 'john@example.com', 'securepassword');

    UPDATE users 
    SET email = 'john.doe@example.com' 
    WHERE username = 'john_doe';


    DELETE FROM users 
    WHERE username = 'john_doe';


    INSERT INTO products (name, price, description) 
    VALUES ('Laptop', 999.99, 'High-performance laptop');


    UPDATE products 
    SET price = 899.99 
    WHERE name = 'Laptop';

    DELETE FROM products 
    WHERE name = 'Laptop';


    SELECT * FROM users;


    SELECT * FROM products 
    WHERE price > 500.00;

    SELECT * FROM users 
    WHERE username = 'john_doe';


    SELECT * FROM customer_orders 
    WHERE user_id = 1;

CREATE TABLE comments (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    product_id INT REFERENCES products(id),
    comment TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

INSERT INTO comments (user_id, product_id, comment) 
VALUES (1, 1, 'Great product!');


UPDATE comments 
SET comment = 'Awesome product!' 
WHERE id = 1;


DELETE FROM comments 
WHERE id = 1;



SELECT * FROM comments 
WHERE product_id = 1;


CREATE INDEX idx_comments_product ON comments(product_id);



SELECT product_id, COUNT(*) AS comment_count 
FROM comments 
GROUP BY product_id;






Requests 23 
CREATE TABLE reviews (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    product_id INT REFERENCES products(id),
    rating INT CHECK (rating >= 1 AND rating <= 5),
    review TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);


INSERT INTO reviews (user_id, product_id, rating, review) 
VALUES (1, 1, 5, 'Excellent!');

UPDATE reviews 
SET rating = 4, review = 'Very good!' 
WHERE id = 1;

DELETE FROM reviews 
WHERE id = 1;


SELECT * FROM reviews 
WHERE product_id = 1;

SELECT product_id, AVG(rating) AS average_rating 
FROM reviews 
GROUP BY product_id;


INSERT INTO suppliers (name, contact_email) 
VALUES ('Supplier One', 'supplier1@example.com');



UPDATE suppliers 
SET contact_email = 'newemail@example.com' 
WHERE id = 1;


DELETE FROM suppliers 
WHERE id = 1;


SELECT * FROM suppliers;


CREATE TABLE supplier_orders (
    id SERIAL PRIMARY KEY,
    supplier_id INT REFERENCES suppliers(id),
    product_id INT REFERENCES products(id),
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    quantity INT NOT NULL
);

INSERT INTO supplier_orders (supplier_id, product_id, quantity) 
VALUES (1, 1, 10);


SELECT * FROM supplier_orders 
WHERE supplier_id = 1;
















# sqlite_practice

How many users are there? - 50 users

What are the 5 most expensive items? 
Small Cotton Gloves|9984
Small Wooden Computer|9859
Awesome Granite Pants|9790
Sleek Wooden Hat|9390
Ergonomic Steel Car|9341
SELECT title, price FROM items ORDER BY price DESC LIMIT 5;

What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
Ergonomic Granite Chair|1496
SELECT title, price FROM items WHERE category = "Books" ORDER BY price ASC LIMIT 1;
SELECT title, price FROM items WHERE category LIKE "%Books%" ORDER BY price ASC LIMIT 1;


Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
SELECT user_id FROM addresses WHERE street = "6439 Zetta Hills"
   ...> ; 
user_id
40

then: 
 SELECT addresses.street, addresses.city, addresses.state FROM addresses JOIN users ON addresses.user_id = users.id WHERE users.id = 40;

Corrine|Little
6439 Zetta Hills|Willmouth|WY
54369 Wolff Forges|Lake Bryon|CA

Correct Virginie Mitchell's address to "New York, NY, 10108".
UPDATE addresses SET city = "New York", state = "NY", zip = "10108" WHERE user_id = (SELECT id FROM users WHERE first_name = "Virginie" AND last_name = "Mitchell");

How much would it cost to buy one of each tool?
46477
SELECT SUM(price) FROM items WHERE category LIKE "%tool%";

How many total items did we sell?
SELECT SUM(quantity) FROM orders
   ...> ;
SUM(quantity)
2125

How much was spent on books?

SELECT SUM(orders.quantity * items.price) FROM items INNER JOIN orders ON items.id = orders.item_id WHERE items.category LIKE "%books%";
1081352

Simulate buying an item by inserting a User for yourself and an Order for that User.
INSERT INTO users (first_name, last_name, email) VALUES("Dave", "McKinney", "davidjmckin@gmail.com");

INSERT INTO orders (user_id, item_id, quantity, created_at) VALUES(51, 97, 1, 2017-02-014);

Adventure Mode

What item was ordered most often? Grossed the most money?


What user spent the most?
SELECT users.first_name, users.last_name, SUM(orders.quantity * items.price) FROM users INNER JOIN orders on users.id = orders.user_id INNER JOIN items #I stopped here. I know this line is halfway complete. 

What were the top 3 highest grossing categories?


Epic Mode

Complete the exercises on sqlteaching.com as well and add a screenshot of the final screen showing all exercises completed to your README.

# SQL_Practice


1)How many users are there?
  `SELECT count(*) FROM users;`
  50
  
2)What are the 5 most expensive items?
  
  `SELECT * FROM items ORDER BY price DESC LIMIT 5;`

3)What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)

  `SELECT * FROM items WHERE category LIKE '%Books' ORDER BY price LIMIT 1;`

4)Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
  `SELECT user_id FROM addresses  WHERE street LIKE '%6439 Zetta Hills';`
  
  PART 2: Yes(2 locations)
  
  `SELECT * FROM addresses WHERE user_id LIKE '%40';`
5)Correct Virginie Mitchell's address to "New York, NY, 10108".
  `SELECT * FROM users WHERE first_name LIKE '%Virginie' and last_name LIKE '%Mitchell';`
  Part 2:
  `SELECT * FROM addresses WHERE user_id=39;`
  Part 3;
  `UPDATE addresses SET city ='New York', state = 'NY', zip = '10108'WHERE user_id='39';`
6)How much would it cost to buy one of each tool?

  `SELECT SUM(price) FROM items WHERE category LIKE '%Tools%';`
  46477

7)How many total items did we sell?
  `SELECT SUM(quantity) FROM orders;`

8)How much was spent on books?

  `SELECT SUM(orders.quantity * items.price) FROM orders INNER JOIN items ON items.id = orders.item_id WHERE items.category    Like '%Books%';`

9)Simulate buying an item by inserting a User for yourself and an Order for that User.
  `INSERT INTO users(first_name, last_name, email) VALUES('Keith','Smith','keilsmit@yahoo.com');`
  Part 2:
  `SELECT * FROM users WHERE first_name LIKE '%Keith%';`
  Part 3:
  `sqlite> INSERT INTO orders(user_id, item_id, quantity, created_at) VALUES('51', '17', '300', date('now'));`
  sqlite> SELECT orders WHERE user_id = '51';
  Error: no such column: orders
  sqlite> SELECT * FROM orders WHERE user_id='51';
  id|user_id|item_id|quantity|created_at
  378|51|17|300|2016-10-24

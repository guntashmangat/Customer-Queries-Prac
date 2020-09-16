# Customer-Queries-Prac

CREATE TABLE salesman (
	salesman_id INT,
	name TEXT,
	city TEXT,
	commission INT);
	
INSERT INTO salesman
VALUES (5001, 'James Hoog', 'New York', 0.15);

INSERT INTO salesman
VALUES (5002, 'Nail Knite', 'Paris', 0.13);

INSERT INTO salesman
VALUES (5005, 'Pit Alex', 'London', 0.11);

INSERT INTO salesman
VALUES (5006, 'Mc Lyon', 'Paris', 0.14);

INSERT INTO salesman
VALUES (5007, 'Paul Adam', 'Rome', 0.13);

INSERT INTO salesman
VALUES (5003, 'Lauson Hen', 'San Jose', 0.12);

CREATE TABLE customer (
	customer_id INT,
	customer_name TEXT,
	city TEXT,
	grade INT,
	salesman_id INT);
	
INSERT INTO customer
VALUES (3002, 'Nick Rimando', 'New York', 100, 5001);

INSERT INTO customer
VALUES (3007, 'Brad Davis', 'New York', 200, 5001);

INSERT INTO customer
VALUES (3005, 'Graham Zusi', 'California', 200, 5002);

INSERT INTO customer
VALUES (3008, 'Julian Green', 'London', 300, 5002);

INSERT INTO customer
VALUES (3004, 'Fabian Johnson', 'Paris', 300, 5006);

INSERT INTO customer
VALUES (3009, 'Geoff Cameron', 'Berlin', 100, 5003);

INSERT INTO customer
VALUES (3003, 'Jozy Altidor', 'Moscow', 200, 5007);

INSERT INTO customer
VALUES (3001, 'Brad Guzan', 'London', 100, 5005);

SELECT * FROM salesman
JOIN customer
ON salesman.salesman_id = customer.salesman_id;

SELECT * FROM salesman
JOIN customer
ON salesman.salesman_id = customer.salesman_id
WHERE salesman.city = customer.city;

CREATE TABLE orders (
	order_no INT,
	purch_amt REAL,
	order_date DATE,
	customer_id INT,
	salesman_id INT);
	
INSERT INTO orders
VALUES (70001, 150.5, '2012-10-05', 3005, 5002);

DELETE FROM orders
WHERE order_date = 1997;

INSERT INTO orders
VALUES (70009, 270.65, '2012-09-10', 3001, 5005);

INSERT INTO orders
VALUES (70002, 65.26, '2012-10-05', 3002, 5001);

INSERT INTO orders
VALUES (70004, 110.5, '2012-08-17', 3009, 5003);

INSERT INTO orders
VALUES (70007, 948.5, '2012-09-10', 3005, 5002);

INSERT INTO orders
VALUES (70005, 2400.6, '2012-07-27', 3007, 5001);

INSERT INTO orders
VALUES (70008, 5760, '2012-09-10', 3002, 5001);

INSERT INTO orders
VALUES (70010, 1983.43, '2012-10-10', 3004, 5006);

INSERT INTO orders
VALUES (70003, 2480.4, '2012-10-10', 3009, 5003);

INSERT INTO orders
VALUES (70012, 250.45, '2012-06-27', 3008, 5002);

INSERT INTO orders
VALUES (70011, 75.29, '2012-08-17', 3003, 5007);

INSERT INTO orders
VALUES (70013, 3045.6, '2012-04-25', 3002, 5001);

SELECT orders.order_no, customer.customer_name
FROM orders, customer
WHERE orders.customer_id = customer.customer_id;

SELECT customer.customer_name as 'customer', customer.city, salesman.name as 'salesman', salesman.commission
FROM customer, salesman
WHERE customer.salesman_id = salesman.salesman_id AND
	salesman.commission <= 0.14 AND
	salesman.commission >= 0.12;
	
SELECT orders.order_no as 'order no', 
	customer.customer_name as 'customer name', 
	salesman.commission as 'commission rate', 
	ROUND((salesman.commission * orders.purch_amt), 2) as 'earned commission'
FROM orders, customer, salesman 
WHERE orders.customer_id = customer.customer_id
	AND customer.salesman_id = salesman.salesman_id
	AND customer.grade >= 200;
	
SELECT * FROM customer, orders
WHERE orders.order_date = '2012-10-05'
AND customer.customer_id = orders.customer_id;

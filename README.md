# GroupBYHavingSubqueries

--1. 
USE Magasine
SELECT p.name, MIN(s.price)
FROM Product p
JOIN Sale s ON s.id_product = p.id
GROUP BY p.name
HAVING MIN(s.price) > 1

--2.
USE Magasine
SELECT p.name
FROM Product p
JOIN Sale s ON s.id_product = p.id
GROUP BY p.name
HAVING AVG(s.price) > 50

--3.
USE Magasine
SELECT c.name, COUNT(*)
FROM Product p
INNER JOIN Category c ON c.id = p.id_category
JOIN Delivery d ON d.id_product = p.id
GROUP BY c.name
HAVING AVG(d.price) > 100

--4. 
USE Magasine
SELECT c.name, p.name, SUM(p.price)
FROM Product p
JOIN Category c ON c.id = p.id_category
WHERE c.name = 'Овощи' OR c.name = 'Техника'
GROUP BY c.name, p.name

--5.
USE Magasine
SELECT s.name, MIN(d.price)
FROM Product p
JOIN Delivery d ON p.id = d.id_product
JOIN Supplier s ON d.id_supplier = s.id
WHERE d.date_of_delivery = '2023-07-01'
GROUP BY s.name
ORDER BY MIN(d.price) DESC

--6.
USE Magasine
SELECT s.name, a.street, c.name, r.name, co.name, COUNT(*)
FROM Supplier s
LEFT JOIN Delivery d ON d.id_supplier = s.id
FULL JOIN Product p ON p.id = d.id_product
INNER JOIN Address a ON s.id_address = a.id
INNER JOIN City c ON a.id_city = c.id
INNER JOIN Region r ON c.id_region = r.id
INNER JOIN Country co ON r.id_country = co.id
GROUP BY s.name, a.street, c.name, r.name, co.name

--7.
USE Magasine 
SELECT TOP 1 c.name
FROM Category c
JOIN Product p ON c.id = p.id_category
GROUP BY c.name
ORDER BY COUNT(*)

--8.
USE Magasine
SELECT c.name, COUNT(*)
FROM Product p  
JOIN Category c ON c.id = p.id_category
JOIN Delivery d ON d.id_product = p.id
JOIN Supplier s ON d.id_supplier = s.id
WHERE c.name = 'Алкоголь' OR c.name = 'Овощи' OR c.name = 'Техника'
GROUP BY c.name
HAVING SUM(d.price) > 400


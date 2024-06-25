# Primeiros comandos sql

SELECT * FROM customers LIMIT 10

SELECT customername,country FROM customers WHERE country = 'UK'
ORDER BY customername DESC

SELECT COUNT(customers.customerid), country FROM customers
WHERE country = 'USA'
GROUP BY country

--desafio 1

--1. Como você seleciona todas as colunas da tabela Customers?
SELECT * FROM customers

--2. Como mostrar apenas o CustomerName e City da tabela Customers?
SELECT customers.customername, customers.city FROM customers

--3. Como encontrar clientes na tabela Customers que estão localizados no país Germany?
SELECT customers.customername, customers.country FROM customers WHERE customers.country = 'Germany'

--4. Como listar clientes da tabela Customers com CustomerID menor ou igual a 5?
SELECT customers.customerid, customers.customername FROM customers WHERE customerid <= 5

--5. Como selecionar clientes da Germany que também estão na cidade de Berlin?
SELECT country, city, country FROM customers
WHERE country = 'Germany' and city = 'Berlin'

--6. Quais são os títulos de contato únicos dos clientes da Germany?
SELECT DISTINCT(customers.postalcode), customers.country FROM customers
 WHERE customers.country = 'Germany'

--7. Retorne apenas os primeiros 5 registros da tabela Customers.
SELECT * FROM customers LIMIT 5

-- agrupamento

SELECT country, count(*) FROM customers GROUP by country

SELECT country, count(*) FROM customers GROUP by country HAVING count(*) >= 5

--desafio 2
--1. Selecione todos os clientes que estão localizados em “Rio de Janeiro” ou “São Paulo”.
SELECT customers.customername, customers.city
FROM customers WHERE customers.city LIKE '%Paulo' OR customers.city = 'Rio de Janeiro'

--2. Selecione o nome do cliente, o nome do contato e a cidade para todos os clientes que não estão no Brasil.
select customers.customername, customers.contactname from customers where customers.country <> 'Brazil'

--3. Liste os países com pelo menos um cliente e ordene alfabeticamente.
select count(customers.country), customers.country from customers
group by customers.country HAVING count(customers.country) >= 1
order by customers.country ASC
	
--4. Selecione o nome do cliente e a cidade para todos os clientes cujo nome do contato é “John Doe”.
select customername, city , contactname from customers where contactname like 'J%' -- não tem John Doe


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

--Desafios LIKE, HAVING, GROUP BY
--Questionário 3

--1. Quais países têm mais de 5 clientes e quantos clientes eles têm?
SELECT COUNT(DISTINCT(customerid)), country FROM customers
group by country  HAVING COUNT(DISTINCT(customerid)) > 5

--2. Conte quantos clientes existem em cada país.
SELECT COUNT(DISTINCT(customers.customerid)),country from customers group by country

--3. Selecione todos os clientes que têm “A” no início do nome do cliente ou “B” no início do nome do contato.
SELECT customers.customername, contactname from customers
where customername like 'A%' or contactname like 'B%'

--4. Liste o número de clientes em cada cidade que tenha mais de 2 clientes.
select city, COUNT(DISTINCT(customers.customerid)) from customers
group by city HAVING COUNT(DISTINCT(customers.customerid)) > 2

--5. Selecione todos os clientes que estão localizados em “Brazil” e cujo código postal não está vazio.
SELECT customers.customername, country from customers
where country = 'Brazil' and customers.postalcode is not null

--Desafio Joins
--Tabelas utilizadas: Customers, Orders e Employees.
--1. Como você consultaria o nome do cliente (CustomerName) e o nome do funcionário (FirstName, LastName) para cada pedido?
SELECT a.*,b.contactname,c.firstname,c.lastname from orders as a
left join customers as b on a.customerid = b.customerid
left join employees as c on a.employeeid = c.employeeid

--2. Como você encontraria todos os pedidos feitos por clientes de um determinado país, por exemplo, “Brasil”?
select a.*, b.country from orders as a
left join customers as b on a.customerid = b.customerid
where b.country = 'Brazil'

--3. Como você listaria todos os clientes e os pedidos associados a eles, incluindo clientes que não
--		fizeram nenhum pedido?
select a.*, b.orderid from customers as a
left join orders as b on a.customerid=b.customerid
	
--5. Como você listaria todos os clientes e todos os pedidos, mostrando as correspondências onde
--		existem e os registros sem correspondência de ambas as tabelas?
SELECT a.customername,b.orderid
from public.customers as a
full join public.orders as b
on a.customerid = b.customerid
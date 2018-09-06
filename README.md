# SQLSERVER
Sintaxis para querys en SQLSERVER


use Northwind
--Definir una variable 
Declare @variable varchar(100)
Set @variable = 'Sql Server'
Select @variable

-- Consulta una tabla 
select companyname, contactname
from Customers


--variables con dos arrobas del sistema
Select @@error

--Concatenar
Select companyname + ' ' + contactname
from Customers

--Operaciones basicas
Select productname, unitprice, UnitsInStock,
UnitPrice * UnitsInStock
from products

-- Distinct
select DISTINCT country 
from Customers
order by Country

-- XML
select companyname, contactname, country
from Customers
for xml auto

-- XML
select companyname, contactname, country
from Customers
for xml path

-- XML
select companyname, contactname, country
from Customers
for xml raw

-----------Alias---------------------
Select productname, unitprice, UnitsInStock,
UnitPrice * UnitsInStock as total
from products as p


-- Use de la funcion Case
Select productname, unitprice, 
case categoryid
	when 1 then 'Pastas'
	when 2 then 'Bebidas'
	when 3 then 'Alimentos'
	else 'Otros'
end as categoria
from products

-- Use de la funcion Case
Select productname, unitprice, categoria=
case categoryid
	when 1 then 'Pastas'
	when 2 then 'Bebidas'
	when 3 then 'Alimentos'
	else 'Otros'
end
from products


--Instruccion select
Select * from Customers
where country='France'
and city='Versailles'

--Instruccion select
Select * from Customers
where country='France'
or country='Canada'
order by country

/*
ORDER FROM QUERY SQL SERVER
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
*/
--Instruccion Select con Group By
Select country, count(companyname)
from Customers
where Country like 'A%'
group by Country
having count(companyname) > 2

#Join

Use Northwind
go

--joins de varias tablas
Select * from customers
Select * from orders

-- join interno
--ANSI 89
Select Customers.CompanyName, Customers.Country,
orders.OrderID, orders.OrderDate
from customers, orders
where customers.CustomerID = orders.CustomerID

--ANSI 92
Select Customers.CompanyName, Customers.Country,
orders.OrderID, orders.OrderDate
from customers INNER JOIN orders
on customers.CustomerID = orders.CustomerID

--join externo
Select Customers.CompanyName, Customers.Country,
orders.OrderID, orders.OrderDate
from customers LEFT OUTER JOIN orders
on customers.CustomerID = orders.CustomerID

-- alias and null
Select c.CompanyName, c.Country,
o.OrderID, o.OrderDate
from Orders AS o RIGHT OUTER JOIN Customers c
on c.CustomerID = o.CustomerID
where OrderID is null

--unir mas de dos tablas
Select C.CompanyName, C.Country,
O.OrderID, O.OrderDate, P.ProductName, D.UnitPrice
from Customers as C INNER JOIN Orders as O
on C.CustomerID = O.CustomerID
INNER JOIN [Order Details] as D
on O.OrderID = D.OrderID
INNER JOIN Products as P
on P.ProductID = D.ProductID
WHERE P.ProductName='Queso Cabrales'

--cross join
Select Customers.CompanyName, Customers.Country,
orders.OrderID, orders.OrderDate
from customers INNER JOIN orders
on customers.CustomerID = orders.CustomerID

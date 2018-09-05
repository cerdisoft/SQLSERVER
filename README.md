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

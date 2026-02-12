```sql
-- ============================================================
-- CONSULTAS CON INNER JOIN
-- ============================================================

-- 1. Unimos empleados con sus departamentos (INNER JOIN).
SELECT e.nombre, d.nombre
FROM empleados e
INNER JOIN dptos d
ON e.id = d.id;

-- 2. Obtenemos el nombre del empleado y el nombre de su departamento.
SELECT e.nombre AS empleado, d.nombre AS departamento
FROM empleados e
INNER JOIN dptos d
ON e.id = d.id;

-- 3. Contamos cuántos empleados hay en cada departamento.
SELECT d.nombre, COUNT(*) AS total_empleados
FROM dptos d
INNER JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre;

-- 4. Obtenemos el departamento que tiene más empleados.
SELECT d.nombre, COUNT(*) AS total_empleados
FROM dptos d
INNER JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre
ORDER BY total_empleados DESC
LIMIT 1;

-- 5. Obtenemos el salario máximo por departamento.
SELECT d.nombre, MAX(e.salario) AS salario_maximo
FROM dptos d
INNER JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre;

-- 6. Obtenemos el salario medio por departamento.
SELECT d.nombre, AVG(e.salario) AS salario_medio
FROM dptos d
INNER JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre;

-- 7. Mostramos empleados con su departamento ordenados por nombre de departamento.
SELECT e.nombre, d.nombre
FROM empleados e
INNER JOIN dptos d
ON e.id = d.id
ORDER BY d.nombre ASC;


-- ============================================================
-- APUNTES SOBRE ALIAS EN INNER JOIN
-- ============================================================

-- Usar alias en una consulta NO cambia el resultado.
-- Solo sirve para escribir consultas más cortas y legibles.

-- FROM empleados e
-- La letra "e" representa a la tabla empleados.

-- FROM dptos d
-- La letra "d" representa a la tabla dptos.

-- Por tanto:
-- e.dni      = empleados.dni
-- e.nombre   = empleados.nombre
-- e.salario  = empleados.salario
-- d.nombre   = dptos.nombre

-- Con alias:
SELECT e.dni, e.nombre, e.salario, d.nombre
FROM empleados e
INNER JOIN dptos d
ON e.id = d.id;

-- Sin alias:
SELECT empleados.dni, empleados.nombre, empleados.salario, dptos.nombre
FROM empleados
INNER JOIN dptos
ON empleados.id = dptos.id;


-- ============================================================
-- EJERCICIOS CON INNER JOIN + GROUP BY
-- ============================================================

-- EJERCICIO 1
SELECT e.dni, e.nombre, e.salario, d.nombre
FROM empleados e
INNER JOIN dptos d
ON e.id = d.id;

-- RESULTADO ESPERADO:
-- 04856665F | S4vitar  | 30000 | RRHH
-- 12345678A | Laura    | 28000 | Contabilidad
-- 23456789B | Carlos   | 32000 | Ciberseguridad
-- 34567890C | Marta    | 35000 | RRHH
-- 45678901D | Javier   | 40000 | RRHH
-- 56789012E | Ana      | 27000 | Ciberseguridad
-- 56789012R | AnaMaria | 28000 | Ciberseguridad


-- EJERCICIO 2
SELECT d.nombre, COUNT(*) AS total_empleados
FROM dptos d
INNER JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre;

-- RESULTADO ESPERADO:
-- Contabilidad     | 1
-- Ciberseguridad   | 3
-- RRHH             | 3


-- EJERCICIO 3
SELECT d.nombre, COUNT(*) AS total_empleados
FROM dptos d
INNER JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre
ORDER BY total_empleados DESC
LIMIT 1;


-- EJERCICIO 4
SELECT d.nombre, MAX(e.salario) AS salario_maximo
FROM dptos d
INNER JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre;


-- EJERCICIO 5
SELECT d.nombre, AVG(e.salario) AS salario_medio
FROM dptos d
INNER JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre
ORDER BY salario_medio DESC;


-- EJERCICIO 6
SELECT d.nombre, COUNT(*) AS total_empleados
FROM dptos d
INNER JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre
HAVING COUNT(*) > 2;


-- EJERCICIO 7
SELECT codigoPostal, MAX(salario) AS salario_maximo
FROM empleados
GROUP BY codigoPostal
ORDER BY salario_maximo DESC;


-- EJERCICIO 8
SELECT d.nombre, MAX(e.salario) AS salario_maximo
FROM dptos d
INNER JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre
ORDER BY salario_maximo DESC
LIMIT 1;


-- EJERCICIO 9
SELECT d.nombre, e.genero, COUNT(*) AS total_empleados
FROM dptos d
INNER JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre, e.genero;
```

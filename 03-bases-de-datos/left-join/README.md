## left-join

```sql
-- ============================================================
-- CONSULTAS CON LEFT JOIN            -- By: @bitsofalber
-- ============================================================

-- LEFT JOIN se utiliza cuando queremos mostrar TODOS los registros
-- de la tabla de la izquierda, aunque no tengan coincidencia
-- en la tabla de la derecha.

-- A diferencia de INNER JOIN, LEFT JOIN NO elimina filas
-- de la tabla principal (la de la izquierda).


-- 1. Unimos departamentos con sus empleados (LEFT JOIN).
--    Se mostrarán todos los departamentos, tengan empleados o no.
SELECT d.nombre, e.nombre
FROM dptos d
LEFT JOIN empleados e
ON d.id = e.id;


-- 2. Obtenemos el nombre del departamento y el nombre del empleado (si existe).
--    Si un departamento no tiene empleados, el nombre del empleado será NULL.
SELECT d.nombre AS departamento, e.nombre AS empleado
FROM dptos d
LEFT JOIN empleados e
ON d.id = e.id;


-- 3. Contamos cuántos empleados hay en cada departamento (incluyendo los vacíos).
--    Usamos COUNT(e.dni) para que los departamentos sin empleados devuelvan 0.
SELECT d.nombre, COUNT(e.dni) AS total_empleados
FROM dptos d
LEFT JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre;


-- 4. Obtenemos el departamento que tiene más empleados.
--    Los departamentos sin empleados no se excluyen.
SELECT d.nombre, COUNT(e.dni) AS total_empleados
FROM dptos d
LEFT JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre
ORDER BY total_empleados DESC
LIMIT 1;


-- 5. Obtenemos el salario máximo por departamento.
--    Si un departamento no tiene empleados, el salario será NULL.
SELECT d.nombre, MAX(e.salario) AS salario_maximo
FROM dptos d
LEFT JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre;


-- 6. Obtenemos el salario medio por departamento.
--    Los departamentos sin empleados devolverán NULL.
SELECT d.nombre, AVG(e.salario) AS salario_medio
FROM dptos d
LEFT JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre;


-- 7. Mostramos departamentos con sus empleados ordenados por nombre de departamento.
SELECT d.nombre AS departamento, e.nombre AS empleado
FROM dptos d
LEFT JOIN empleados e
ON d.id = e.id
ORDER BY d.nombre ASC;



-- ============================================================
-- APUNTES CLAVE SOBRE LEFT JOIN           -- By: @bitsofalber
-- ============================================================

-- LEFT JOIN conserva SIEMPRE la tabla de la izquierda.
-- Si no hay coincidencia con la tabla derecha:
--   - Las columnas de la tabla derecha aparecen como NULL.

-- LEFT JOIN es muy útil para:
--   - Detectar registros sin relación
--   - Ver datos incompletos
--   - Auditorías y análisis reales

-- Diferencia clave:
-- INNER JOIN elimina filas sin coincidencia.
-- LEFT JOIN las mantiene.



-- ============================================================
-- EJERCICIOS CON LEFT JOIN + GROUP BY (CON RESULTADOS)
-- ============================================================

-- EJERCICIO 1
-- Mostrar todos los departamentos con sus empleados (si existen).
SELECT d.nombre, e.nombre
FROM dptos d
LEFT JOIN empleados e
ON d.id = e.id;

-- RESULTADO ESPERADO (ejemplo):
-- Contabilidad     | Laura
-- Ciberseguridad   | Carlos
-- Ciberseguridad   | Ana
-- RRHH             | Marta
-- RRHH             | Javier
-- RRHH             | NULL



-- ============================================================
-- EXPLICACIÓN PASO A PASO DEL EJERCICIO 1
-- ============================================================

-- 1. Queremos mostrar TODOS los departamentos,
--    incluso aquellos que no tengan empleados asignados.

-- 2. En el SELECT indicamos:
--    - d.nombre → nombre del departamento
--    - e.nombre → nombre del empleado (si existe)
SELECT d.nombre, e.nombre

-- 3. Empezamos desde la tabla dptos porque es la que
--    queremos conservar completa.
FROM dptos d

-- 4. Usamos LEFT JOIN para unir empleados sin eliminar
--    departamentos sin empleados.
LEFT JOIN empleados e

-- 5. Condición del JOIN:
--    - d.id es el ID del departamento
--    - e.id es el ID del departamento en empleados
ON d.id = e.id;

-- 6. Si un departamento no tiene empleados:
--    - SQL mantiene la fila
--    - Las columnas de empleados aparecen como NULL



-- ============================================================
-- EJERCICIO 2
-- Obtener los departamentos que NO tienen empleados.
-- ============================================================

SELECT d.nombre
FROM dptos d
LEFT JOIN empleados e
ON d.id = e.id
WHERE e.id IS NULL;

-- RESULTADO ESPERADO:
-- Departamentos sin empleados



-- ============================================================
-- EJERCICIO 3
-- Obtener el número de empleados por departamento
-- incluyendo los departamentos vacíos.
-- ============================================================

SELECT d.nombre, COUNT(e.dni) AS total_empleados
FROM dptos d
LEFT JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre;

-- RESULTADO ESPERADO:
-- Contabilidad     | 1
-- Ciberseguridad   | 3
-- RRHH             | 3
-- (Departamentos sin empleados → 0)



-- ============================================================
-- EJERCICIO 4
-- Obtener el salario máximo por departamento
-- aunque no tenga empleados.
-- ============================================================

SELECT d.nombre, MAX(e.salario) AS salario_maximo
FROM dptos d
LEFT JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre;

-- RESULTADO ESPERADO:
-- Contabilidad     | 28000
-- Ciberseguridad   | 32000
-- RRHH             | 40000
-- (Departamentos sin empleados → NULL)



-- ============================================================
-- EJERCICIO 5
-- Obtener los departamentos con más de 2 empleados
-- usando LEFT JOIN + HAVING.
-- ============================================================

SELECT d.nombre, COUNT(e.dni) AS total_empleados
FROM dptos d
LEFT JOIN empleados e
ON d.id = e.id
GROUP BY d.nombre
HAVING COUNT(e.dni) > 2;

-- RESULTADO ESPERADO:
-- Ciberseguridad | 3
-- RRHH           | 3



-- ============================================================
-- CUÁNDO USAR LEFT JOIN EN ASIR
-- ============================================================

-- LEFT JOIN se usa en ASIR para:
--   - Detectar usuarios sin grupo
--   - Ver servicios sin asignación
--   - Auditar bases de datos
--   - Encontrar errores de integridad
--   - Analizar datos reales

-- INNER JOIN limpia datos.
-- LEFT JOIN muestra la realidad.

-- https://www.youtube.com/@bitsofalber   -- By: @bitsofalber
```

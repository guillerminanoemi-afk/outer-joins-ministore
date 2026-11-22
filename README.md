# MiniStore — Análisis de ventas con SQL Outer JOINs

## 1. Descripción del proyecto

Este proyecto consiste en un ejercicio práctico de SQL enfocado en el uso de `LEFT JOIN`, `RIGHT JOIN` y `FULL OUTER JOIN` para analizar la relación entre un catálogo de productos y sus ventas.

El objetivo es resolver diferentes preguntas de negocio, como identificar productos que nunca fueron vendidos, detectar ventas asociadas a productos inexistentes en el catálogo y realizar una auditoría completa de ambas tablas.

Este análisis permite detectar posibles errores de carga de datos y obtener información útil para la gestión comercial.

## 2. Estructura del repositorio

```text
outer-joins-ministore/
├── schema.sql
├── soluciones.sql
└── README.md
```

- **schema.sql:** Contiene la creación de las tablas `productos` y `ventas`, junto con los datos de prueba.
- **soluciones.sql:** Contiene las tres consultas SQL utilizando LEFT JOIN, RIGHT JOIN y FULL OUTER JOIN.
- **README.md:** Contiene la descripción del proyecto, las instrucciones de ejecución y las respuestas a las preguntas teóricas.

## 3. Entorno y herramientas

**Gestor de base de datos utilizado:** SQL Server (Microsoft SQL Server).

**Versión recomendada:** SQL Server 2019 o superior.

**Herramienta recomendada:** SQL Server Management Studio (SSMS).

**Lenguaje:** SQL (T-SQL).

La base de datos utilizada se denomina `MiniStore` y contiene dos tablas:

- **productos:** 9 registros de productos del catálogo.
- **ventas:** 10 registros de transacciones.

Los datos incluyen dos productos que nunca fueron vendidos y una venta asociada a un producto inexistente en el catálogo.

## 4. Instrucciones de ejecución

Para reproducir el ejercicio en SQL Server, seguir los siguientes pasos:

**Paso 1: Crear la base de datos**

Abrir SQL Server Management Studio (SSMS), conectarse al servidor y ejecutar:

```sql
IF DB_ID('MiniStore') IS NULL
    CREATE DATABASE MiniStore;
GO

USE MiniStore;
GO
```

**Paso 2: Ejecutar schema.sql**

Seleccionar la base de datos `MiniStore`, abrir el archivo `schema.sql` y ejecutar su contenido.

Este archivo crea las tablas `productos` y `ventas` e inserta los datos de prueba.

**Paso 3: Verificar los datos**

Ejecutar las siguientes consultas:

```sql
SELECT * FROM productos;
SELECT * FROM ventas;
```

Se deben obtener 9 productos y 10 ventas.

**Paso 4: Ejecutar soluciones.sql**

Abrir el archivo `soluciones.sql`, asegurarse de que la base de datos activa sea `MiniStore` y ejecutar las tres consultas.

El archivo `soluciones.sql` debe contener las consultas de análisis, sin eliminar ni volver a crear las tablas.

## 5. Consultas y resultados esperados

### Consulta 1 — LEFT JOIN

**Pregunta de negocio:** ¿Qué productos del catálogo nunca fueron vendidos?

Se utiliza LEFT JOIN para mostrar todos los productos y sus ventas asociadas, incluyendo los productos que no tienen ventas.

**Resultado esperado:** 11 filas correspondientes a los 9 productos del catálogo. Los productos 108 y 109 aparecen con `venta_id = NULL`.

### Consulta 2 — RIGHT JOIN

**Pregunta de negocio:** ¿Existen ventas registradas con productos que no figuran en nuestro catálogo?

Se utiliza RIGHT JOIN para conservar todas las ventas y detectar aquellas que no tienen un producto asociado.

**Resultado esperado:** 1 venta huérfana, correspondiente a `venta_id = 10`, con `producto_id = 999`.

### Consulta 3 — FULL OUTER JOIN

**Pregunta de negocio:** Obtener una vista completa de auditoría que muestre todos los productos y todas las ventas sin perder registros.

Se utiliza FULL OUTER JOIN para conservar los registros de ambas tablas, incluso cuando no existen coincidencias.

**Resultado esperado:** 12 filas, incluyendo los productos sin ventas y la venta sin producto asociado.

---

## 6. Preguntas teóricas

### ¿Por qué usaste LEFT JOIN para la Consulta 1 y no INNER JOIN? ¿Qué se perdería si usaras INNER JOIN?

En la Consulta 1 usé LEFT JOIN porque necesitaba obtener todos los productos de la tabla de la izquierda (productos), incluyendo aquellos que no tienen coincidencias en la tabla de la derecha (ventas). En esos casos, las columnas de ventas aparecen como NULL.

Si utilizara INNER JOIN, perdería los productos que nunca fueron vendidos, como los productos 108 y 109.

### ¿Por qué usaste RIGHT JOIN para la Consulta 2? ¿Qué tabla está a la izquierda y cuál a la derecha en tu consulta?

En la Consulta 2 usé RIGHT JOIN porque necesitaba obtener todas las ventas registradas (tabla 2), incluso aquellas que no tengan un producto asociado en el catálogo (tabla 1).

En mi consulta, la tabla de la izquierda es productos y la tabla de la derecha es ventas.

RIGHT JOIN conserva todas las filas de ventas y, cuando no encuentra coincidencia en productos, devuelve NULL en las columnas de esa tabla.

Esto permite identificar las ventas asociadas a productos inexistentes en el catálogo.

### ¿Qué representan los valores NULL en cada resultado? Explicá con un ejemplo concreto de los datos qué significa que venta_id sea NULL en la Consulta 1 y que producto_id de productos sea NULL en la Consulta 2.

Los valores NULL en estos resultados indican que no se encontró una coincidencia entre las tablas.

En la Consulta 1, que `venta_id` sea NULL significa que no existe una venta asociada para ese producto. Por ejemplo, el producto 108 (Hub USB-C 7p) aparece con `venta_id = NULL` porque nunca fue vendido.

En la Consulta 2, que `producto_id` de la tabla productos sea NULL significa que existe una venta registrada cuyo producto no aparece en el catálogo.

Por ejemplo, la venta 10 tiene asociado el producto 999, que no existe en la tabla productos.

### ¿Cuándo usarías FULL OUTER JOIN en un caso real de negocio?

Usaría FULL OUTER JOIN si necesitara obtener una lista completa de las ventas y los productos registrados, para observar tanto las ventas que no tienen un producto asociado como los productos que no tuvieron ventas.

Esto permitiría detectar posibles errores en el catálogo y, al mismo tiempo, identificar productos sin ventas para evaluar campañas de marketing o promociones.

De esta manera, podría analizar ambas situaciones en una sola consulta, sin perder registros de ninguna de las dos tablas.

---

## 7. Conclusión

Este ejercicio me permitió comprender las diferencias entre LEFT JOIN, RIGHT JOIN y FULL OUTER JOIN,

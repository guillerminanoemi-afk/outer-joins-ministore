-- GESTOR UTILIZADO:  SQL Server 
______________________________________________

--- ¿Por qué usaste LEFT JOIN para la Consulta 1 y no INNER JOIN? ¿Qué se perdería si usaras INNER JOIN?

-- En la consulta 1 usé LEFT JOIN porque la pregunta busca que la consulta traiga todos los productos (tabla de la izquierda) con los pedidos que nunca 
--se hayan vendido, incluyendo los que no tienen coincidencia en la tabla 2 (tabla de la derecha) y los devuelve como NULL. Al filtrar con WHERE, solo
-- nos arroja los productos (tabla 1) que no tienen ventas (tabla 2). Si utilizara INNER JOIN, perdería los productos que nunca fueron vendidos, como los productos 108 y 109

-- ¿Por qué usaste RIGHT JOIN para la Consulta 2? ¿Qué tabla está a la izquierda y cuál a la derecha en tu consulta?

-- En la consulta 2 usé RIGHT JOIN porque necesitaba obtener todas las ventas registradas (tabla 2), incluso aquellas que no tengan un producto asociado en el catálogo (tabla 1) y que aparezcan como NULL si no hay coincidencia. 
-- En mi consulta la tabla de la izquierda es productos (trae solo los datos que coincida con la tabla de la derecha) y mi tabla derecha es ventas (trae todo los datos de la tabla ventas)

-- ¿Qué representan los valores NULL en cada resultado? Explicá con un ejemplo concreto de los datos qué significa que venta_id sea NULL en la Consulta 1 y que producto_id de productos sea NULL en la Consulta 2.

-- El NULL en cada resultado indica que no hay coincidencia en la tablas para esa combinación.
-- Ejemplo: que venta_id sea NULL en la consulta 1 significa que no existe una venta asociada para el producto de la tabla de la izquierda
-- Que producto_id sea NULL en la consulta 2 significa que hay ventas registradas para productos que no aparecen en la tabla Productos

-- ¿Cuándo usarías FULL OUTER JOIN en un caso real de negocio?

-- Usaría FULL OUTER JOIN si se solicita obtener una lista con todas las ventas y productos que tuvimos en X tiempo, para observar tanto las ventas que no tienen un producto
-- y ver el error de catálogo, como los productos que no tuvieron ventas para la campaña de marketing , en una sola consulta


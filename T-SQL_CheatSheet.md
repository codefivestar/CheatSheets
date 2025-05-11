
# T-SQL Cheat Sheet

## 📌 Consultas Básicas

```sql

-- Seleccionar datos
SELECT * FROM tabla;
SELECT col1, col2 FROM tabla;
SELECT DISTINCT col1 FROM tabla;
SELECT TOP 10 * FROM tabla;

-- Filtros
SELECT * FROM tabla WHERE col1 = 'valor';
SELECT * FROM tabla WHERE col1 > 100 AND col2 = 'activo';
SELECT * FROM tabla WHERE col1 BETWEEN 10 AND 20;
SELECT * FROM tabla WHERE col1 IN (1, 2, 3);
SELECT * FROM tabla WHERE col1 LIKE 'A%';
SELECT * FROM tabla WHERE col1 IS NULL;

-- Ordenamiento
SELECT * FROM tabla ORDER BY col1 DESC;
SELECT * FROM tabla ORDER BY col1 ASC, col2 DESC;

```

## 🔗 JOINS

```sql

-- INNER JOIN
SELECT t1.col1, t2.col2 
FROM tabla1 t1
INNER JOIN tabla2 t2 ON t1.id = t2.id_tabla1;

-- LEFT JOIN
SELECT t1.col1, t2.col2 
FROM tabla1 t1
LEFT JOIN tabla2 t2 ON t1.id = t2.id_tabla1;

-- RIGHT JOIN
SELECT t1.col1, t2.col2 
FROM tabla1 t1
RIGHT JOIN tabla2 t2 ON t1.id = t2.id_tabla1;

-- FULL JOIN
SELECT t1.col1, t2.col2 
FROM tabla1 t1
FULL JOIN tabla2 t2 ON t1.id = t2.id_tabla1;

-- CROSS JOIN
SELECT t1.col1, t2.col2 FROM tabla1 t1 CROSS JOIN tabla2 t2;

```

## 📊 Agregación

```sql

-- Funciones básicas
SELECT COUNT(*) AS total, AVG(col1) AS promedio, 
       SUM(col1) AS suma, MIN(col1), MAX(col1)
FROM tabla;

-- GROUP BY
SELECT col1, COUNT(*) AS cantidad
FROM tabla
GROUP BY col1;

-- HAVING
SELECT col1, COUNT(*) AS cantidad
FROM tabla
GROUP BY col1
HAVING COUNT(*) > 5;

```


## ✏️ Modificación de Datos

```sql

-- INSERT
INSERT INTO tabla (col1, col2) VALUES (1, 'A');
INSERT INTO tabla SELECT col1, col2 FROM otra_tabla;

-- UPDATE
UPDATE tabla SET col1 = 100 WHERE col2 = 'activo';
UPDATE t1 SET t1.col1 = t2.col2 
FROM tabla1 t1 JOIN tabla2 t2 ON t1.id = t2.id;

-- DELETE
DELETE FROM tabla WHERE col1 < 10;
TRUNCATE TABLE tabla;

```


## 🏷️ DDL (Estructura de Datos)

```sql

-- Crear tabla
CREATE TABLE tabla (
    id INT IDENTITY(1,1) PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    fecha DATETIME DEFAULT GETDATE()
);

-- Modificar tabla
ALTER TABLE tabla ADD col_nueva INT NULL;
ALTER TABLE tabla DROP COLUMN col_antigua;
ALTER TABLE tabla ALTER COLUMN col1 VARCHAR(200);

-- Eliminar tabla
DROP TABLE tabla;

```


## 🔍 Subconsultas

```sql

-- Subconsulta en WHERE
SELECT * FROM tabla 
WHERE col1 IN (SELECT col1 FROM otra_tabla WHERE col2 = 'X');

-- Subconsulta en FROM
SELECT t.col1 
FROM (SELECT col1 FROM tabla WHERE col2 > 100) t;

-- EXISTS
SELECT * FROM tabla t1
WHERE EXISTS (SELECT 1 FROM tabla2 t2 WHERE t2.id = t1.id);

```


## 🧩 Common Table Expressions (CTEs)

``` sql

WITH cte_ejemplo AS (
    SELECT col1, col2 
    FROM tabla 
    WHERE col1 > 100
)
SELECT * FROM cte_ejemplo;

```

## 🛠️ Funciones Avanzadas

```sql

-- Funciones de ventana
SELECT col1, 
       ROW_NUMBER() OVER(ORDER BY col2) AS row_num,
       RANK() OVER(PARTITION BY col3 ORDER BY col2) AS rank
FROM tabla;

-- Funciones de cadena
SELECT CONCAT(col1, ' ', col2), SUBSTRING(col1, 1, 3), 
       REPLACE(col1, 'old', 'new'), LEN(col1)
FROM tabla;

-- Funciones de fecha
SELECT GETDATE(), DATEADD(DAY, 7, fecha), 
       DATEDIFF(DAY, fecha1, fecha2), DATEPART(YEAR, fecha)
FROM tabla;

```

## 💾 Procedimientos Almacenados

```sql

CREATE PROCEDURE sp_ejemplo
    @param1 INT,
    @param2 VARCHAR(100)
AS
BEGIN
    SET NOCOUNT ON;
    SELECT * FROM tabla 
    WHERE col1 = @param1 AND col2 LIKE '%' + @param2 + '%';
END;

-- Ejecutar
EXEC sp_ejemplo @param1 = 100, @param2 = 'test';

```

## 🔄 Transacciones

```sql

BEGIN TRANSACTION;
BEGIN TRY
    UPDATE tabla1 SET col1 = 100 WHERE id = 1;
    INSERT INTO tabla2 (col1) VALUES ('nuevo');
    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    ROLLBACK TRANSACTION;
    SELECT ERROR_MESSAGE() AS ErrorMessage;
END CATCH;

```

## 📑 Índices

```sql

-- Crear índices
CREATE INDEX idx_col1 ON tabla (col1);
CREATE UNIQUE INDEX idx_unique ON tabla (col1, col2);

-- Eliminar índice
DROP INDEX idx_col1 ON tabla;

```


## 📌 Tips Rápidos

``` sql

-- Consultar metadatos
SELECT * FROM INFORMATION_SCHEMA.TABLES;
SELECT * FROM sys.indexes WHERE object_id = OBJECT_ID('tabla');

-- Variables
DECLARE @var INT = 10;
 SELECT @var = COUNT(*) FROM tabla;

-- Depuración
PRINT 'Mensaje de debug';

```


## 📚 Recursos Adicionales

```sql

    WITH (NOLOCK) -- para lecturas sin bloqueo

    SET STATISTICS TIME ON -- para analizar rendimiento

    OPTION (OPTIMIZE FOR UNKNOWN) -- para problemas de parametrización

```


Aquí tienes una **sección adicional sobre funciones JSON en T-SQL** que puedes agregar a tu Cheat Sheet, con ejemplos prácticos:

```markdown
## 🌐 Funciones JSON en T-SQL

### 1. **Convertir datos a JSON**
```sql
-- Tabla → JSON (FOR JSON AUTO)
SELECT id, nombre, fecha FROM clientes FOR JSON AUTO;

-- Resultado: 
-- [{"id":1,"nombre":"Ana","fecha":"2023-01-15"},{"id":2,"nombre":"Carlos","fecha":"2023-02-20"}]

-- Personalizado (FOR JSON PATH)
SELECT id AS 'cliente.id', 
       nombre AS 'cliente.datos.nombre'
FROM clientes FOR JSON PATH;

-- Resultado:
-- [{"cliente":{"id":1,"datos":{"nombre":"Ana"}},...}]
```

### 2. **Convertir JSON a tabla**
```sql
-- JSON → Tabla (OPENJSON)
DECLARE @json NVARCHAR(MAX) = 
'[{"id":1,"nombre":"Ana"},{"id":2,"nombre":"Carlos"}]';

SELECT * FROM OPENJSON(@json)
WITH (
    id INT '$.id',
    nombre VARCHAR(100) '$.nombre'
);

-- Resultado:
-- | id | nombre  |
-- |----|---------|
-- | 1  | Ana     |
-- | 2  | Carlos  |
```

### 3. **Extraer valores de JSON**
```sql
DECLARE @json NVARCHAR(MAX) = 
'{"cliente":{"id":1,"datos":{"nombre":"Ana","activo":true}}}';

-- Extraer valor específico (JSON_VALUE)
SELECT JSON_VALUE(@json, '$.cliente.datos.nombre') AS nombre; -- "Ana"

-- Extraer fragmento JSON (JSON_QUERY)
SELECT JSON_QUERY(@json, '$.cliente.datos') AS datos; -- {"nombre":"Ana","activo":true}

-- Verificar propiedad (JSON_PATH_EXISTS)
SELECT CASE WHEN JSON_PATH_EXISTS(@json, '$.cliente.datos.activo') = 1 
       THEN 'Sí' ELSE 'No' END AS tiene_activo; -- "Sí"
```

### 4. **Modificar JSON**
```sql
DECLARE @json NVARCHAR(MAX) = '{"id":1,"nombre":"Ana"}';

-- Actualizar propiedad (JSON_MODIFY)
SET @json = JSON_MODIFY(@json, '$.nombre', 'Ana Martínez');
-- Resultado: {"id":1,"nombre":"Ana Martínez"}

-- Agregar nueva propiedad
SET @json = JSON_MODIFY(@json, '$.activo', CAST(1 AS BIT));
-- Resultado: {"id":1,"nombre":"Ana Martínez","activo":true}

-- Eliminar propiedad
SET @json = JSON_MODIFY(@json, '$.activo', NULL);
-- Resultado: {"id":1,"nombre":"Ana Martínez"}
```

### 5. **Validar JSON**
```sql
DECLARE @json_valido NVARCHAR(MAX) = '{"id":1}';
DECLARE @json_invalido NVARCHAR(MAX) = '{id:1}'; -- Falta comillas

SELECT ISJSON(@json_valido) AS es_valido_1; -- 1 (true)
SELECT ISJSON(@json_invalido) AS es_valido_2; -- 0 (false)
```

### 6. **Ejemplo Completo: API REST Simulada**
```sql
-- Crear tabla con columna JSON
CREATE TABLE pedidos (
    id INT IDENTITY PRIMARY KEY,
    datos NVARCHAR(MAX) CHECK (ISJSON(datos) = 1)
);

-- Insertar pedido en formato JSON
INSERT INTO pedidos (datos) VALUES (
'{
    "cliente_id": 100,
    "items": [
        {"producto_id": 501, "cantidad": 2},
        {"producto_id": 205, "cantidad": 1}
    ],
    "total": 59.99
}');

-- Consultar items de pedido (con OPENJSON y JOIN)
SELECT 
    p.id,
    j.producto_id,
    j.cantidad,
    pr.nombre
FROM pedidos p
CROSS APPLY OPENJSON(p.datos, '$.items')
WITH (
    producto_id INT '$.producto_id',
    cantidad INT '$.cantidad'
) j
JOIN productos pr ON j.producto_id = pr.id;
```

### 📌 Tips Avanzados:
1. Usar `WITH (SCHEMABINDING)` en funciones que procesen JSON para mejor rendimiento.
2. Para JSON grandes (>100MB), considerar usar `NVARCHAR(MAX)` con compresión.
3. Combinar `JSON_VALUE` con índices computados para búsquedas rápidas:
```sql
ALTER TABLE pedidos 
ADD cliente_id AS CAST(JSON_VALUE(datos, '$.cliente_id') AS INT);

CREATE INDEX idx_cliente_id ON pedidos(cliente_id);
```


Aquí tienes una **sección avanzada sobre manejo de errores en T-SQL** lista para integrar en tu Cheat Sheet, con técnicas profesionales y ejemplos prácticos:

```markdown
## 🛠️ Manejo Avanzado de Errores en T-SQL

### 1. **Estructura TRY-CATCH Básica**
```sql
BEGIN TRY
    -- Código que puede fallar
    INSERT INTO clientes (id, nombre) VALUES (1, 'Ana');
END TRY
BEGIN CATCH
    SELECT 
        ERROR_NUMBER() AS ErrorCode,
        ERROR_MESSAGE() AS ErrorMessage,
        ERROR_SEVERITY() AS ErrorSeverity,
        ERROR_STATE() AS ErrorState,
        ERROR_PROCEDURE() AS ErrorProcedure,
        ERROR_LINE() AS ErrorLine;
END CATCH
```

### 2. **Manejo de Transacciones con Errores**
```sql
BEGIN TRANSACTION;
BEGIN TRY
    UPDATE cuenta SET saldo = saldo - 100 WHERE id = 1;
    INSERT INTO transacciones (cuenta_id, monto) VALUES (1, 100);
    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    IF @@TRANCOUNT > 0
        ROLLBACK TRANSACTION;
    
    DECLARE @ErrorMsg NVARCHAR(4000) = 
        'Error en procedimiento: ' + ISNULL(ERROR_PROCEDURE(), 'N/A') + 
        ', Línea: ' + CAST(ERROR_LINE() AS NVARCHAR(10)) + 
        ' - ' + ERROR_MESSAGE();
    
    RAISERROR(@ErrorMsg, 16, 1);
END CATCH
```

### 3. **Jerarquía de Errores Personalizados**
```sql
-- Definir errores personalizados
EXEC sp_addmessage 
    @msgnum = 50001, 
    @severity = 16,
    @msgtext = 'Saldo insuficiente: el cliente no tiene fondos suficientes',
    @lang = 'us_english';

-- Uso en código
BEGIN TRY
    IF (SELECT saldo FROM cuenta WHERE id = 1) < 100
        RAISERROR(50001, 16, 1);
END TRY
BEGIN CATCH
    IF ERROR_NUMBER() = 50001
        PRINT 'Error manejado: ' + ERROR_MESSAGE();
    ELSE
        THROW; -- Relanza el error original
END CATCH
```

### 4. **THROW vs RAISERROR**
| Característica       | `THROW`                          | `RAISERROR`                     |
|----------------------|----------------------------------|----------------------------------|
| Versión              | SQL Server 2012+                 | Todas las versiones             |
| Parámetros           | Solo número/mensaje              | Permite formato estilo printf   |
| Severidad predet.    | Siempre 16                       | Configurable                    |
| Re-lanzar errores    | Ideal para CATCH                 | Requiere parámetros manuales   |

```sql
-- Ejemplo THROW
BEGIN CATCH
    PRINT 'Error capturado, relanzando...';
    THROW; -- Mantiene el error original
END CATCH

-- Ejemplo RAISERROR
RAISERROR('Error personalizado: %s', 16, 1, 'Descripción del problema');
```

### 5. **Manejo de Errores en Lotes**
```sql
BEGIN TRY
    BEGIN TRANSACTION;
        -- Bloque 1
        INSERT INTO tabla1 VALUES (1);
        
        -- Bloque 2 con error controlado
        BEGIN TRY
            INSERT INTO tabla1 VALUES ('texto-en-campo-int');
        END TRY
        BEGIN CATCH
            PRINT 'Error en bloque 2: ' + ERROR_MESSAGE();
            -- Continuar ejecución
        END CATCH
        
        -- Bloque 3
        UPDATE tabla2 SET col1 = 100;
    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    IF @@TRANCOUNT > 0
        ROLLBACK TRANSACTION;
    THROW;
END CATCH
```

### 6. **Logging Profesional de Errores**
```sql
CREATE TABLE error_log (
    log_id INT IDENTITY PRIMARY KEY,
    error_time DATETIME2 DEFAULT SYSUTCDATETIME(),
    error_number INT,
    error_severity INT,
    error_state INT,
    error_procedure NVARCHAR(128),
    error_line INT,
    error_message NVARCHAR(4000),
    user_name NVARCHAR(128) = SUSER_SNAME(),
    additional_info XML
);

-- Procedimiento para logging
CREATE PROCEDURE log_error
    @AdditionalInfo XML = NULL
AS
BEGIN
    INSERT INTO error_log (
        error_number, error_severity, error_state,
        error_procedure, error_line, error_message,
        additional_info
    )
    VALUES (
        ERROR_NUMBER(), ERROR_SEVERITY(), ERROR_STATE(),
        ERROR_PROCEDURE(), ERROR_LINE(), ERROR_MESSAGE(),
        @AdditionalInfo
    );
    
    RETURN SCOPE_IDENTITY();
END;
```

### 7. **Patrón de Retry para Errores Transitorios**
```sql
DECLARE @retry INT = 0, @max_retries INT = 3, @success BIT = 0;

WHILE @retry < @max_retries AND @success = 0
BEGIN
    BEGIN TRY
        BEGIN TRANSACTION;
            -- Operación crítica (ej: llamada a servicio externo)
            EXEC sp_operacion_sensible;
        COMMIT TRANSACTION;
        SET @success = 1;
    END TRY
    BEGIN CATCH
        IF @@TRANCOUNT > 0
            ROLLBACK TRANSACTION;
            
        IF ERROR_NUMBER() IN (1205, 3960) -- Deadlock o snapshot conflict
        BEGIN
            SET @retry += 1;
            WAITFOR DELAY '00:00:01'; -- Espera 1 segundo
        END
        ELSE
            THROW;
    END CATCH
END

IF @success = 0
    RAISERROR('Falló después de %d intentos', 16, 1, @max_retries);
```

### 8. **Errores con XACT_ABORT**
```sql
SET XACT_ABORT ON; -- Rollback automático en errores

BEGIN TRY
    BEGIN TRANSACTION;
        INSERT INTO tabla1 VALUES (1);
        INSERT INTO tabla2 VALUES ('error'); -- Fallará
    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    SELECT ERROR_MESSAGE() AS MensajeError;
    -- No necesita ROLLBACK explícito (XACT_ABORT lo maneja)
END CATCH
```

### 📌 Buenas Prácticas
1. **Niveles de severidad**:
   - 0-10: Informativos
   - 11-16: Errores manejables (ej: reglas de negocio)
   - 17-19: Errores graves (ej: recursos)
   - 20-25: Errores fatales (ej: corrupción datos)

2. **THROW** es preferible sobre RAISERROR en código nuevo (más simple y consistente).

3. **Siempre** verificar `@@TRANCOUNT` antes de hacer ROLLBACK.

4. **Registrar** todos los errores inesperados con contexto completo.

5. **Pruebas** de errores deliberados para validar el manejo.
```

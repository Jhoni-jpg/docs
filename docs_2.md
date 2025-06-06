# Documentación de la Base de Datos - Tienda ARA

## 1. Estructura de Tablas

### Tabla `clientes`

```sql
CREATE TABLE clientes (
    id_cliente SERIAL PRIMARY KEY,
    nombre VARCHAR(100),
    correo VARCHAR(100),
    fecha_registro DATE
);
```

### Tabla `productos`

```sql
CREATE TABLE productos (
    id_producto SERIAL PRIMARY KEY,
    nombre VARCHAR(100),
    precio NUMERIC(10, 2),
    stock INT
);
```

### Tabla `ventas`

```sql
CREATE TABLE ventas (
    id_ventas SERIAL PRIMARY KEY,
    cliente_id INT REFERENCES clientes(id_cliente),
    producto_id INT REFERENCES productos(id_producto),
    cantidad INT,
    fecha_venta DATE
);
```

## 2. Datos de Ejemplo

### Clientes

```sql
INSERT INTO clientes (nombre, correo, fecha_registro) VALUES
('Juan Pérez', 'juan.perez@email.com', '2025-06-01'),
('María Gómez', 'maria.gomez@email.com', '2025-05-15'),
('Carlos Ramírez', 'carlos.ramirez@email.com', '2025-04-10'),
('Ana Torres', 'ana.torres@email.com', '2025-03-25'),
('Luis Martínez', 'luis.martinez@email.com', '2025-06-05');
```

### Productos

```sql
INSERT INTO productos (nombre, precio, stock) VALUES
('Laptop Lenovo', 1200.99, 15),
('Mouse inalámbrico', 25.50, 50),
('Teclado mecánico', 89.99, 30),
('Monitor 24 pulgadas', 199.99, 20),
('Auriculares Bluetooth', 59.99, 40);
```

### Ventas

```sql
INSERT INTO ventas (cliente_id, producto_id, cantidad, fecha_venta) VALUES
(1, 1, 1, '2025-06-03'),
(2, 3, 2, '2025-06-04'),
(3, 5, 1, '2025-06-05'),
(4, 2, 3, '2025-06-06'),
(5, 4, 1, '2025-06-07');
```

## 3. Funciones PL/pgSQL

### Punto 1 - Total Pagado por Cliente

```sql
create or replace function totalPagado(idCliente int) returns table(...) as $$
...
$$ language plpgsql;
```

Devuelve el nombre del cliente, productos comprados, cantidades y total pagado.

### Punto 2 - Total de Productos por Cliente

```sql
create or replace function totalCantidad(idCliente int) returns table(...) as $$
...
$$ language plpgsql;
```

Muestra las cantidades de productos comprados por un cliente.

### Punto 3 - Producto Más Vendido

```sql
create or replace function masVendido() returns table(...) as $$
...
$$ language plpgsql;
```

Devuelve el producto con mayor cantidad vendida.

### Punto 4 - Total de Ventas

```sql
create or replace function facturacionTotal() returns table(...) as $$
...
$$ language plpgsql;
```

Cuenta el total de registros de ventas.

### Punto 5 - Producto Específico Comprado por un Cliente

```sql
create or replace function productoEspecifico(...) returns table(...) as $$
...
$$ language plpgsql;
```

Consulta si un cliente compró un producto específico.

### Punto 6 - Total de Clientes que Han Comprado

```sql
create or replace function totalClientes_compras() returns int as $$
...
$$ language plpgsql;
```

Cuenta cuántos clientes han realizado al menos una compra.

### Punto 7 - Cliente con Mayor Cantidad Comprada

```sql
create or replace function clienteCompra() returns varchar as $$
...
$$ language plpgsql;
```

Devuelve el nombre del cliente con mayor volumen de productos adquiridos.

### Punto 8 - Productos Sin Ventas

```sql
create or replace function producto_sinVentas() returns table(...) as $$
...
$$ language plpgsql;
```

Lista los productos que no han sido vendidos.

### Punto 9 - Total Vendido de un Producto

```sql
create or replace function totalVendido(idProducto integer) returns int as $$
...
$$ language plpgsql;
```

Suma la cantidad total vendida de un producto.

### Punto 10 - Días Desde Última Compra de un Cliente

```sql
create or replace function ultimaCompra_dias(clienteId_producto INT) returns int as $$
...
$$ language plpgsql;
```

Calcula los días transcurridos desde la última compra de un cliente.

### Punto 11 - Listado de Ventas con Cursor

```sql
create or replace function listarVentas_cursor(p_cliente_id INT) returns table(...) as $$
...
$$ language plpgsql;
```

Utiliza cursor para recorrer y devolver las ventas de un cliente.

## 4. Comentarios Finales

### Punto 12

La base de datos ARA tiene una estructura modular que mejora la eficiencia. La separación de ventas y sus detalles (a través de una tabla intermedia como `Tb_detalles_ventas`) permite una mejor normalización y consulta de datos.

### Punto 13

La estructura ARA es más eficiente para facturación real, ya que permite asociar múltiples productos a una misma venta. A diferencia del modelo de "Olímpica", evita la redundancia de datos como la repetición de datos de cliente para cada producto.

---

> **Nota:** Algunas funciones tienen errores leves como referencias incorrectas de columnas o alias. Se recomienda realizar pruebas unitarias antes de utilizarlas en producción.


# 📚 Documentación de Funciones - Tienda ARA

## 1. `total_gastado(idCliente_parametro int)`

**Descripción:**  
Retorna el detalle de compras de un cliente específico, incluyendo la fecha, cantidad y subtotal de cada compra.

**Parámetros:**  
- `idCliente_parametro` (int): ID del cliente.

**Retorna:**  

| Campo            | Tipo     | Descripción                            |
|------------------|----------|----------------------------------------|
| Nombre_cliente   | varchar  | Nombre del cliente                     |
| Fecha            | date     | Fecha de la compra                     |
| Cantidad         | int      | Cantidad de productos comprados        |
| Subtotal         | decimal  | Subtotal de la compra                  |

---

## 2. `cantidad_producto(idProducto int, cantidadProducto int)`

**Descripción:**  
Verifica si hay suficiente stock disponible para un producto específico.

**Parámetros:**  
- `idProducto` (int): ID del producto.  
- `cantidadProducto` (int): Cantidad solicitada.

**Retorna:**  

| Campo        | Tipo     | Descripción                         |
|--------------|----------|-------------------------------------|
| IdProductos  | int      | ID del producto                     |
| cantidad     | int      | Stock actual del producto           |
| validacion   | text     | Mensaje sobre disponibilidad        |

---

## 3. `productosOrdenados_cantidad()`

**Descripción:**  
Lista los productos ordenados por su valor total (precio * stock) de mayor a menor.

**Parámetros:**  
- Ninguno

**Retorna:**  

| Campo           | Tipo     | Descripción                          |
|-----------------|----------|--------------------------------------|
| NombreProducto  | varchar  | Nombre del producto                  |
| StockProducto   | int      | Stock disponible                     |
| PrecioProducto  | decimal  | Precio unitario del producto         |
| TotalProducto   | decimal  | Valor total del producto en stock    |

---

## 4. `nombreProductos()`

**Descripción:**  
Retorna los productos cuyo stock es menor o igual a 5.

**Parámetros:**  
- Ninguno

**Retorna:**  
- Todas las columnas de la tabla `productos`.

---

## 5. `mayorCompra()`

**Descripción:**  
Obtiene el cliente con la compra más costosa según la cantidad * subtotal.

**Parámetros:**  
- Ninguno

**Retorna:**  

| Campo            | Tipo     | Descripción                       |
|------------------|----------|-----------------------------------|
| NombreCliente    | varchar  | Nombre del cliente                |
| SubtotalCliente  | decimal  | Subtotal de la compra             |
| TotalCliente     | decimal  | Total (cantidad * subtotal)       |

> ⚠️ Revisión sugerida: `JOIN` incorrecto por `id_venta`.

---

## 6. `listaFechas(fechaInicio date, fechaFin date)`

**Descripción:**  
Lista los clientes que realizaron compras entre dos fechas específicas.

**Parámetros:**  
- `fechaInicio` (date): Fecha de inicio del rango.  
- `fechaFin` (date): Fecha de fin del rango.

**Retorna:**  

| Campo           | Tipo     | Descripción                    |
|-----------------|----------|--------------------------------|
| NombreCliente   | varchar  | Nombre del cliente             |
| fechCliente     | date     | Fecha de la compra             |

---

## 7. `stockActual(nombreProducto varchar)`

**Descripción:**  
Consulta el stock actual de un producto según su nombre.

**Parámetros:**  
- `nombreProducto` (varchar): Nombre del producto.

**Retorna:**  

| Campo            | Tipo     | Descripción                    |
|------------------|----------|--------------------------------|
| Nombre_Producto  | varchar  | Nombre del producto            |
| Stock_Actual     | int      | Stock actual                   |

---

## 8. `aumentarStock(nombreProducto varchar, numeroAumento int)`

**Descripción:**  
Actualiza el stock de un producto asignándole un nuevo valor.

**Parámetros:**  
- `nombreProducto` (varchar): Nombre del producto.  
- `numeroAumento` (int): Nuevo valor para el stock.

**Retorna:**  
- `void`. Muestra un mensaje: `'Datos actualizados!'`

---

## 9. `productosComprados(clienteEspecificado varchar)`

**Descripción:**  
Lista los productos comprados por un cliente según su nombre.

**Parámetros:**  
- `clienteEspecificado` (varchar): Nombre del cliente.

**Retorna:**  

| Campo           | Tipo     | Descripción                    |
|-----------------|----------|--------------------------------|
| NombreCliente   | varchar  | Nombre del cliente             |
| ProductName     | varchar  | Nombre del producto comprado   |

> ⚠️ Revisión sugerida: errores de `JOIN` (mal uso de `id_cliente` en lugar de `id_venta` y `id_producto`).

---

## 10. `eliminar_venta(venta_id int)`

**Descripción:**  
Elimina una venta, actualizando primero el stock de los productos asociados a ella.

**Parámetros:**  
- `venta_id` (int): ID de la venta a eliminar.

**Retorna:**  
- `void`

> ⚠️ Revisión sugerida: error en la condición del `UPDATE` (`id_venta` no referenciado correctamente).


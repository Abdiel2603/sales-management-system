# Sistema de Ventas en PostgreSQL

## Descripción General

El presente proyecto consiste en el diseño, desarrollo e implementación de una base de datos relacional para la administración de un sistema de ventas utilizando PostgreSQL. El objetivo principal fue construir una estructura sólida, organizada y escalable que permitiera gestionar de forma eficiente productos, clientes, sucursales, inventario, ventas, facturación y movimientos de almacén dentro de una empresa comercial.

La base de datos fue desarrollada mediante la separación lógica por esquemas (`catalogo`, `inventario` y `ventas`), permitiendo una mejor administración de la información, mayor orden estructural y facilidad de mantenimiento. Además, se implementaron relaciones entre tablas, restricciones de integridad, validaciones mediante `CHECK`, claves primarias, claves foráneas, índices únicos y generación masiva de registros para simular un entorno empresarial real.

Este proyecto forma parte de las prácticas de Bases de Datos Avanzadas, enfocado en reforzar conocimientos de modelado relacional, optimización de consultas SQL y administración de grandes volúmenes de información.

---

## Objetivo

Desarrollar una base de datos robusta para un sistema de ventas que permita controlar de manera eficiente:

- catálogo de productos  
- inventario por sucursal  
- movimientos de entrada y salida  
- clientes y datos fiscales  
- ventas realizadas  
- detalle de productos vendidos  
- facturación electrónica  
- control administrativo y operativo del negocio  

---

## Tecnologías Utilizadas

- PostgreSQL  
- SQL  
- pgAdmin 4  
- PL/pgSQL  
- generate_series() para carga masiva de datos  
- UUID para folios fiscales  
- JSON y estructuras avanzadas de validación  

---

## Estructura de la Base de Datos

La base de datos se encuentra organizada en tres schemas principales:

---

## Schema: catalogo

Este esquema se encarga de la administración general de productos.

### Tabla: producto

Contiene la información principal de cada producto registrado.

#### Campos principales:

- id_producto  
- nombre  
- sku  
- precio  
- activo  
- fecha_creacion  

#### Funcionalidad:

Permite registrar y controlar productos disponibles para venta, asegurando que cada SKU sea único y que los precios sean válidos.

---

## Schema: inventario

Este esquema administra el control físico del inventario en las distintas sucursales.

### Tablas principales:

- sucursal  
- inventario  
- movimiento_inventario  

#### Funcionalidad:

Permite llevar control sobre:

- existencias disponibles  
- stock mínimo  
- movimientos operativos  
- abastecimiento  
- salidas por venta  
- ajustes manuales de almacén  

---

## Schema: ventas

Este esquema controla toda la operación comercial.

### Tablas principales:

- cliente  
- cliente_rfc  
- venta  
- detalle_venta  
- factura  

#### Funcionalidad:

Permite administrar:

- clientes registrados  
- ventas generadas  
- productos vendidos  
- control de pagos  
- emisión de facturas  
- historial comercial completo  

---

## Relaciones Implementadas

El sistema utiliza integridad referencial mediante relaciones entre tablas:

- cliente → cliente_rfc  
- venta → cliente  
- venta → sucursal  
- detalle_venta → venta  
- detalle_venta → producto  
- factura → venta  
- factura → cliente_rfc  
- inventario → sucursal  
- inventario → producto  
- movimiento_inventario → inventario  

Esto garantiza consistencia, evita registros inválidos y mejora el control de la información.

---

## Validaciones Aplicadas

Se implementaron múltiples restricciones para asegurar calidad de datos.

### Restricciones CHECK

- precios mayores a cero  
- stock no negativo  
- stock mínimo válido  
- cantidades mayores a cero  
- tipo de movimiento permitido  
- estatus válidos de venta  

### Restricciones UNIQUE

- SKU único por producto  
- email único por cliente  
- RFC único por cliente  
- nombre único por sucursal  
- una factura por venta  

### Otros controles

- UUID automático para folio fiscal  
- eliminación en cascada para relaciones necesarias  
- valores por defecto automáticos  
- timestamps automáticos de registro  

---

## Carga Masiva de Datos

Para simular un entorno real de trabajo se realizó inserción masiva de registros utilizando `generate_series()`.

### Registros generados:

- 500 productos  
- 10 sucursales  
- inventario completo por sucursal  
- 500 clientes  
- 500 registros fiscales  
- 10,000 ventas  
- 100,000 detalles de venta  
- 10,000 movimientos de inventario  
- 500 facturas  

Esto permitió probar rendimiento, relaciones y consultas complejas sobre grandes volúmenes de información.

---

## Consultas Realizadas

Además de la creación completa de la base de datos, se desarrollaron múltiples consultas para validación, análisis y explotación de información.


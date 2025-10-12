## 📘 Modelo Entidad-Relación – Librería en Línea

Este diagrama representa el **modelo entidad-relación (ER)** de una **librería en línea**.  
A continuación se describen las **entidades, atributos y relaciones** principales:

---

### 🧩 Entidades y Atributos

#### **CLIENTE**
- `id_cliente` *(PK)*  
- `nombre`  
- `correo`  
- `direccion_envio`  
Representa a los clientes que realizan compras en la librería.

#### **LIBRO**
- `ISBN` *(PK)*  
- `titulo`  
- `autor`  
- `precio`  
Contiene la información de los libros disponibles para la venta.

#### **PEDIDO**
- `id_pedido` *(PK)*  
- `fecha_pedido`  
- `total`  
- `id_cliente` *(FK)*  
Registra cada compra realizada por un cliente.

#### **CATEGORIA**
- `id_categoria` *(PK)*  
- `nombre_categoria`  
Agrupa los libros según su tipo o temática (por ejemplo, *Novela*, *Ciencia*, etc.).

#### **DETALLE_PEDIDO**
- `id_detalle` *(PK)*  
- `id_pedido` *(FK)*  
- `ISBN` *(FK)*  
- `cantidad`  
- `subtotal`  
Representa los productos (libros) que forman parte de un pedido.

#### **LIBRO_CATEGORIA**
- `ISBN` *(FK)*  
- `id_categoria` *(FK)*  
Es una tabla intermedia para manejar la relación **muchos a muchos** entre libros y categorías.

---

### 🔗 Relaciones

- **CLIENTE → PEDIDO**  
  Un cliente puede *realizar varios pedidos*, pero cada pedido pertenece a *un solo cliente*.

- **PEDIDO → DETALLE_PEDIDO**  
  Un pedido *contiene varios detalles* (libros comprados), y cada detalle pertenece a *un solo pedido*.

- **LIBRO → DETALLE_PEDIDO**  
  Un libro puede *aparecer en muchos detalles de pedido* (si varios clientes lo compran).

- **LIBRO ↔ CATEGORIA**  
  Representadas mediante la tabla `LIBRO_CATEGORIA`, donde:
  - Un libro puede *pertenecer a varias categorías*.
  - Una categoría puede *incluir varios libros*.

---

### 📊 Diagrama ER (Mermaid)

```mermaid
erDiagram
    CLIENTE {
        int id_cliente PK
        VARCHAR nombre
        VARCHAR correo
        VARCHAR direccion_envio
    }

    LIBRO {
        VARCHAR ISBN PK
        VARCHAR titulo
        VARCHAR autor
        float precio
    }

    PEDIDO {
        int id_pedido PK
        date fecha_pedido
        float total
        int id_cliente FK
    }

    CATEGORIA {
        int id_categoria PK
        VARCHAR nombre_categoria
    }

    DETALLE_PEDIDO {
        int id_detalle PK
        int id_pedido FK
        VARCHAR ISBN FK
        int cantidad
        float subtotal
    }

    LIBRO_CATEGORIA {
        VARCHAR ISBN FK
        int id_categoria FK
    }

    %% Relaciones
    CLIENTE ||--o{ PEDIDO : "realiza"
    PEDIDO ||--o{ DETALLE_PEDIDO : "contiene"
    LIBRO ||--o{ DETALLE_PEDIDO : "incluye"
    LIBRO ||--o{ LIBRO_CATEGORIA : "pertenece a"
    CATEGORIA ||--o{ LIBRO_CATEGORIA : "agrupa"



![Diagrama ER](Diagrama_ER.svg)

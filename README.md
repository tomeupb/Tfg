# Sistema de Administración de Videoclub

## Tecnologías

- **Base de Datos:** MySQL
- **Backend:** Spring Boot
- **Frontend:** Thymeleaf, HTML, CSS, Bootstrap, JavaScript (no seguro 100%)

## Estructura del Proyecto

### Controller

- CRUD (Post, GET, etc.)

### Model

- Definir las clases y enlazarlas con la base de datos.

### Repository

- Interfaz que extiende los métodos del CRUD.

### Service

- Lógica de negocio.

## Funcionalidades del Administrador

- CRUD de **Películas**.
- CRUD de **Usuarios**.
- Gestión de **Alquileres**.
- Buscar **Películas** por ID, nombre, fecha, etc.

## Funcionalidades del Usuario

- Buscar **Películas**.
- Apartado **Personal**.
- Marcar películas como **Vistas**, **Pendientes**, **En Posesión**.

## Estructura de Base de Datos

### 1. Tabla de Usuarios (usuarios)

| Campo        | Tipo             | Descripción                                        |
|--------------|------------------|----------------------------------------------------|
| id_usuario   | INT (PK, AUTO_INCREMENT) | Identificador único del usuario.                 |
| nombre       | VARCHAR(100)      | Nombre del usuario.                               |
| email        | VARCHAR(100) (único) | Correo electrónico del usuario.                   |
| contraseña   | VARCHAR(100)      | Contraseña del usuario.                           |

### 2. Tabla de Películas (peliculas)

| Campo        | Tipo             | Descripción                                        |
|--------------|------------------|----------------------------------------------------|
| id_pelicula  | INT (PK, AUTO_INCREMENT) | Identificador único de la película.              |
| titulo       | VARCHAR(255)      | Título de la película.                             |
| descripcion  | TEXT              | Descripción de la película.                        |
| genero       | VARCHAR(50)       | Género de la película.                             |
| año          | INT               | Año de estreno de la película.                     |
| imagen       | VARCHAR(255)      | URL o ruta de la imagen de la película.            |
| disponible   | BOOLEAN           | Indica si la película está disponible para alquilar o no. |

### 3. Tabla de Alquileres (alquileres)

| Campo           | Tipo             | Descripción                                        |
|-----------------|------------------|----------------------------------------------------|
| id_alquiler     | INT (PK, AUTO_INCREMENT) | Identificador único del alquiler.                |
| id_usuario      | INT (FK)         | Referencia al usuario que alquiló la película.     |
| id_pelicula     | INT (FK)         | Referencia a la película alquilada.                |
| fecha_alquiler  | DATE             | Fecha en que se alquiló la película.               |
| fecha_devolucion| DATE             | Fecha en que se devolvió la película.              |
| estado          | ENUM('ALQUILADA', 'DEVUELTA', 'PENDIENTE') | Estado del alquiler. |

### 4. Tabla de Estados de Películas (estados_peliculas)

| Campo           | Tipo             | Descripción                                        |
|-----------------|------------------|----------------------------------------------------|
| id_estado       | INT (PK, AUTO_INCREMENT) | Identificador único del estado.                   |
| id_usuario      | INT (FK)         | Referencia al usuario que marcó el estado.         |
| id_pelicula     | INT (FK)         | Referencia a la película que tiene un estado.      |
| estado          | ENUM('VISTA', 'PENDIENTE', 'EN_POSESION') | Estado de la película según el usuario.           |

## Relaciones Entre Clases

- **Usuario (1:N) Alquiler:** Un usuario puede alquilar varias películas.
- **Película (1:N) Alquiler:** Una película puede ser alquilada varias veces.
- **Usuario (1:N) EstadoPelicula:** Un usuario puede marcar varias películas con diferentes estados.
- **Película (1:N) EstadoPelicula:** Una película puede estar en distintos estados según el usuario.

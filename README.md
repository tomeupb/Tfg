## Descripción del Proyecto

El **Sistema de Administración ** tendrá como objetivo la gestión de una página web sobre películas con dos roles principales: **Usuarios** y **Administrador**. Cada uno de los roles podrá realizar acciones dependiendo de su nivel de acceso.

- **Administrador:** Tendrá acceso a funcionalidades de gestión de todo el sistema, incluyendo la administración de películas y usuarios. Podrá realizar operaciones CRUD (Crear, Leer, Actualizar, Eliminar) sobre las películas y los usuarios, así como gestionar la parte no visible para los usuarios regulares.
- **Usuario:** Podrá registrarse, iniciar sesión, y acceder a su propio apartado personal donde podrá interactuar con las películas. Los usuarios podrán marcar las películas según el estado en el que se encuentren (por ejemplo, vistas, pendientes o en posesión) junto otras acciones.

## Funcionalidades

### Funcionalidades del Administrador

1. **CRUD de Películas:** El administrador podrá agregar, editar y eliminar películas del sistema.
2. **CRUD de Usuarios:** El administrador podrá gestionar los usuarios del sistema, incluyendo la creación, edición y eliminación de cuentas.
3. **Gestión del Videoclub:** El administrador podrá gestionar el inventario de películas disponibles para alquilar y mantener el control de los usuarios y sus alquileres.

### Métodos

  -Estadísticas 
  -Peliculas vistas por genero/sexo
  -Peliculas mas vistas
  -Peliculas menos vistas
  -Generos mas vistos
  
  -Lógica
  -Alquiler
  -Retrasos
  -Insertar Dinero
  -Retirar dinero
  -Disponibilidad
  -Comprar
  -...
### Funcionalidades del Usuario

1. **Registro y Login:** Los usuarios podrán registrarse en el sistema y acceder con sus credenciales.
2. **Buscar Películas:** Los usuarios podrán buscar películas disponibles en el videoclub.
3. **Apartado Personal:** Los usuarios tendrán un apartado donde podrán ver las películas que han alquilado y su estado.
4. **Marcar Películas por Estado:** Los usuarios podrán marcar las películas según su estado:
   - **Vistas:** Las películas que ya han visto.
   - **Pendientes:** Las películas que desean ver en el futuro.
   - **En Posesión:** Las películas que han alquilado pero aún no han devuelto.
5. **Ver trailer con link:** Podrán ver los trialer con links
6.  **Filtrar Peliculas:** Dependiento del estado
7.  **Calificar peliculas:** 1 a 5 
   
## Tecnologías

## Relaciones Entre Clases
- **Backend:** Spring Boot
- **Frontend:** Thymeleaf, HTML, CSS, Bootstrap, JavaScript (no seguro 100%)

## Estructura del Proyecto

### Controller

- CRUD (Post, GET, etc.)

### Model

- Definir las clases y enlazarlas con la base de datos.

### Repository

- Interfaz que extiende los métodos del CRUD.


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
| id_usuario   | INT (PK, AUTO_INCREMENT) | Identificador único del usuario.           |
| nombre       | VARCHAR(100)      | Nombre del usuario.                               |
| email        | VARCHAR(100) (único) | Correo electrónico del usuario.                |
| contraseña   | VARCHAR(100)      | Contraseña del usuario.                           |
| rol          | VARCHAR(100)      | ADMIN-USER                                        |
| credito      | Decimal   (100)      | Dinero para gastar                                |
| deuda        | Decimal (100)      | Dinero que sobrepassa el actual                   |
| sexo         | VARCHAR(100)      | Homber / mujer                                    |

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
| formato   |  ENUM                 |DVD, blueray, |
| trailer   | VARCHAR(255)        | Direccion url para ver el trailer. |

### 3. Tabla de Alquileres (alquileres)

| Campo           | Tipo             | Descripción                                        |
|-----------------|------------------|----------------------------------------------------|
| id_alquiler     | INT (PK, AUTO_INCREMENT) | Identificador único del alquiler.                |
| id_usuario      | INT (FK)         | Referencia al usuario que alquiló la película.     |
| id_pelicula     | INT (FK)         | Referencia a la película alquilada.                |
| fecha_alquiler  | DATE             | Fecha en que se alquiló la película.               |
| fecha_devolucion| DATE             | Fecha en que se devolvió la película.              |
| estado          | ENUM('ALQUILADA', 'DEVUELTA', 'PENDIENTE') | Estado del alquiler. |
| duracion          | INT | Duracion de la pelicula |
| precioCompra        | Decimal | Precio de la pelicula comprada |
| precioAlquiler       | Decimal | Pecio de la pelicula Alquilada |

### 4. Tabla de Estados de Películas (estados_peliculas)

| Campo           | Tipo             | Descripción                                        |
|-----------------|------------------|----------------------------------------------------|
| id_estado       | INT (PK, AUTO_INCREMENT) | Identificador único del estado.                   |
| id_usuario      | INT (FK)         | Referencia al usuario que marcó el estado.         |
| id_pelicula     | INT (FK)         | Referencia a la película que tiene un estado.      |
| estado          | ENUM('VISTA', 'PENDIENTE', 'EN_POSESION') | Estado de la película según el usuario.           |
| devuelta        | Boolean | Estado de si ha sido devuelta         |



### 5. Tabla (usuarios_peliculas)

| Campo           | Tipo              | Descripción                                        |
|-----------------|------------------ |----------------------------------------------------|
| id_usuario      | INT (FK)          | Referencia al usuario que marcó el estado.         |
| id_pelicula     | INT (FK)          | Referencia a la película que tiene un estado.      |
| fecha_visto     | DateTime          | Estado de la película según el usuario.           |
| calificacion     | INT              | Estado de la película según el usuario.           |



## Relaciones Entre Clases(No seguro 100%)

- **Usuario (1:N) Alquiler:** Un usuario puede alquilar varias películas.
- **Película (1:N) Alquiler:** Una película puede ser alquilada varias veces.
- **Usuario (1:N) EstadoPelicula:** Un usuario puede marcar varias películas con diferentes estados.
- **Película (1:N) EstadoPelicula:** Una película puede estar en distintos estados según el usuario.
 - **Usuario (N:N) Peliculas:** Una película puede estar en distintos estados según el usuario.

 ## Dockerizar el proyecto

 ## Diagrama 




 

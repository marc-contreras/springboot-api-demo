# Spring Boot API Demo

API REST desarrollada con Spring Boot para la gestión de usuarios utilizando JPA y MySQL.

## Características

* Crear usuarios
* Obtener todos los usuarios
* Buscar usuario por ID
* Buscar usuarios por prioridad
* Eliminar usuarios
* Persistencia de datos mediante MySQL
* Arquitectura en capas (Controller, Service, Repository, Model)

---

## Tecnologías utilizadas

* Java 17
* Spring Boot 3.5
* Spring Web
* Spring Data JPA
* MySQL
* Maven

---

## Estructura del proyecto

```text
src/main/java/com/example/demo2
│
├── controllers
│   └── UsuarioController.java
│
├── services
│   └── UsuarioService.java
│
├── repositories
│   └── UsuarioRepository.java
│
├── models
│   └── UsuarioModel.java
│
└── Demo2Application.java
```

---

## Modelo de datos

### Usuario

| Campo     | Tipo    |
| --------- | ------- |
| id        | Long    |
| nombre    | String  |
| email     | String  |
| prioridad | Integer |

La entidad se almacena en la tabla:

```sql
usuario
```

### Ejemplo de creación de tabla

```sql
CREATE TABLE usuario (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(255),
    email VARCHAR(255),
    prioridad INT
);
```

---

# Instalación

## 1. Clonar el repositorio

```bash
git clone <url-del-repositorio>
cd springboot-api-demo
```

## 2. Crear la base de datos

```sql
CREATE DATABASE springboot;
```

## 3. Configurar conexión MySQL

Editar el archivo:

```properties
src/main/resources/application.properties
```

Ejemplo:

```properties
spring.datasource.url=jdbc:mysql://127.0.0.1/springboot
spring.datasource.username=root
spring.datasource.password=TU_PASSWORD

spring.jpa.hibernate.ddl-auto=none
```

> Se recomienda no subir credenciales reales al repositorio.

---

## 4. Compilar el proyecto

### Linux / Mac

```bash
./mvnw clean install
```

### Windows

```cmd
mvnw.cmd clean install
```

---

## 5. Ejecutar la aplicación

### Linux / Mac

```bash
./mvnw spring-boot:run
```

### Windows

```cmd
mvnw.cmd spring-boot:run
```

La API estará disponible en:

```text
http://localhost:8080
```

---

# Endpoints de la API

Base URL:

```text
http://localhost:8080/usuario
```

---

## Obtener todos los usuarios

### Request

```http
GET /usuario
```

### Respuesta

```json
[
  {
    "id": 1,
    "nombre": "Juan",
    "email": "juan@email.com",
    "prioridad": 1
  }
]
```

### Método asociado

```java
@GetMapping()
public ArrayList<UsuarioModel> obtenerUsuarios()
```

Obtiene todos los usuarios registrados en la base de datos.

---

## Crear usuario

### Request

```http
POST /usuario
```

### Body

```json
{
  "nombre": "Juan",
  "email": "juan@email.com",
  "prioridad": 1
}
```

### Respuesta

```json
{
  "id": 1,
  "nombre": "Juan",
  "email": "juan@email.com",
  "prioridad": 1
}
```

### Método asociado

```java
@PostMapping()
public UsuarioModel guardarUsuario(@RequestBody UsuarioModel usuario)
```

Guarda un nuevo usuario en la base de datos.

---

## Obtener usuario por ID

### Request

```http
GET /usuario/{id}
```

### Ejemplo

```http
GET /usuario/1
```

### Respuesta

```json
{
  "id": 1,
  "nombre": "Juan",
  "email": "juan@email.com",
  "prioridad": 1
}
```

### Método asociado

```java
@GetMapping(path = "/{id}")
public Optional<UsuarioModel> obtenerUsuarioPorId(...)
```

Busca un usuario mediante su identificador.

---

## Buscar usuarios por prioridad

### Request

```http
GET /usuario/query?prioridad=1
```

### Respuesta

```json
[
  {
    "id": 1,
    "nombre": "Juan",
    "email": "juan@email.com",
    "prioridad": 1
  }
]
```

### Método asociado

```java
@GetMapping("/query")
public ArrayList<UsuarioModel> obtenerUsuariosPorPrioridad(...)
```

Obtiene todos los usuarios que tengan la prioridad indicada.

---

## Eliminar usuario

### Request

```http
DELETE /usuario/{id}
```

### Ejemplo

```http
DELETE /usuario/1
```

### Respuesta exitosa

```text
Se eliminó el usuario con id 1
```

### Respuesta de error

```text
No pudo eliminar el usuario con id 1
```

### Método asociado

```java
@DeleteMapping(path = "/{id}")
public String eliminarUsuarioPorId(...)
```

Elimina un usuario utilizando su ID.

---

# Arquitectura

## Controller

`UsuarioController`

Recibe las peticiones HTTP y expone los endpoints REST.

## Service

`UsuarioService`

Contiene la lógica de negocio y actúa como intermediario entre Controller y Repository.

## Repository

`UsuarioRepository`

Gestiona el acceso a datos mediante Spring Data JPA.

## Model

`UsuarioModel`

Representa la entidad Usuario dentro de la aplicación y la base de datos.

---

# Ejemplos con cURL

## Crear usuario

```bash
curl -X POST http://localhost:8080/usuario \
-H "Content-Type: application/json" \
-d '{
    "nombre":"Juan",
    "email":"juan@email.com",
    "prioridad":1
}'
```

## Obtener usuarios

```bash
curl http://localhost:8080/usuario
```

## Buscar por ID

```bash
curl http://localhost:8080/usuario/1
```

## Buscar por prioridad

```bash
curl http://localhost:8080/usuario/query?prioridad=1
```

## Eliminar usuario

```bash
curl -X DELETE http://localhost:8080/usuario/1
```

---

# Mejoras futuras

* Validación de datos con Bean Validation.
* Manejo global de excepciones.
* Documentación automática con Swagger/OpenAPI.
* Tests unitarios e integración.
* Paginación y ordenación de resultados.
* Variables de entorno para credenciales de base de datos.

---

# Autor

Proyecto de ejemplo desarrollado con Spring Boot y MySQL para aprendizaje de APIs REST.

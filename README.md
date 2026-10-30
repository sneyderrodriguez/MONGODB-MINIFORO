# 💬 MiniForo — API REST con MongoDB

> API REST desarrollada con **Java y Spring Boot** para gestionar usuarios, publicaciones y comentarios, utilizando **MongoDB** como base de datos documental.

![Java](https://img.shields.io/badge/Java-26-orange) ![Spring Boot](https://img.shields.io/badge/Spring_Boot-4.1.1-green) ![MongoDB](https://img.shields.io/badge/MongoDB-Database-darkgreen) ![Maven](https://img.shields.io/badge/Maven-Build-blue)

---

## 📌 Sobre el proyecto

**MiniForo** es un proyecto backend que permite crear y consultar usuarios, publicar contenido y añadir comentarios a las publicaciones. Su propósito es practicar la construcción de una API REST y la persistencia de documentos con Spring Data MongoDB.

El proyecto separa controladores, servicios, repositorios, modelos y DTO para mantener el código organizado.

## ✨ Características

- Registro y listado de usuarios, con datos de perfil flexibles.
- Creación y consulta de publicaciones.
- Consulta de publicaciones de un autor, ordenadas por fecha descendente.
- Incorporación de comentarios dentro de una publicación.
- Registro automático de la fecha de publicaciones y comentarios.
- Validación de campos obligatorios y del formato del correo electrónico mediante Bean Validation.
- Almacenamiento en las colecciones `usuarios` y `publicaciones` de MongoDB.

## 🧰 Tecnologías

- **Java 26**
- **Spring Boot 4.1.1** y Spring Web MVC
- **Spring Data MongoDB**
- **MongoDB**
- **Jakarta Bean Validation**
- **Maven** y Maven Wrapper
- **Spring Boot DevTools**

## 🧩 Estructura del proyecto

```text
MONGODB-MINIFORO/
├── pom.xml
├── mvnw
├── mvnw.cmd
└── src/
    ├── main/
    │   ├── java/com/generation/miniforo/
    │   │   ├── controller/
    │   │   │   ├── PublicacionController.java
    │   │   │   └── UsuarioController.java
    │   │   ├── dto/
    │   │   ├── model/
    │   │   │   ├── Comentario.java
    │   │   │   ├── Publicacion.java
    │   │   │   └── Usuario.java
    │   │   ├── repository/
    │   │   ├── service/
    │   │   └── MiniforoApplication.java
    │   └── resources/application.properties
    └── test/java/com/generation/miniforo/
        └── MiniforoApplicationTests.java
```

## 🌐 Endpoints de la API

La aplicación utiliza, por defecto, `http://localhost:8080`.

| Método | Ruta | Descripción |
|---|---|---|
| `POST` | `/api/usuarios` | Crear usuario |
| `GET` | `/api/usuarios` | Listar usuarios |
| `POST` | `/api/publicaciones` | Crear publicación |
| `GET` | `/api/publicaciones` | Listar publicaciones |
| `GET` | `/api/publicaciones/autor/{autorId}` | Consultar publicaciones de un autor |
| `POST` | `/api/publicaciones/{id}/comentarios` | Añadir un comentario |

### Ejemplos de solicitudes

**Crear usuario:** `POST /api/usuarios`

```json
{
  "nombre": "Usuario de ejemplo",
  "email": "usuario@example.com",
  "datosPerfil": {
    "intereses": ["Java", "MongoDB"]
  }
}
```

**Crear publicación:** `POST /api/publicaciones` (reemplaza `ID_DEL_USUARIO` por un ID real).

```json
{
  "autorId": "ID_DEL_USUARIO",
  "titulo": "Mi primera publicación",
  "contenido": "Hola, MiniForo."
}
```

**Agregar comentario:** `POST /api/publicaciones/{id}/comentarios` (reemplaza `{id}` por el ID de una publicación existente).

```json
{
  "autorNombre": "Visitante",
  "texto": "¡Excelente publicación!"
}
```

Los endpoints de creación de usuarios y publicaciones devuelven `201 Created`. Los campos obligatorios se validan antes de procesar la solicitud.

## 🗄️ Modelo de datos

- **Usuario:** `id`, `nombre`, `email` y `datosPerfil` (mapa de propiedades flexibles).
- **Publicación:** `id`, `autorId`, `titulo`, `contenido`, `fecha` y lista de `comentarios`.
- **Comentario:** `autorNombre`, `texto` y `fecha`; se almacena dentro del documento de la publicación.

## 🖥️ Ejecutar el proyecto localmente

### Requisitos

- JDK 26.
- Una instancia accesible de MongoDB, local o en Atlas.
- Conexión a Internet para descargar dependencias Maven, si aún no están instaladas.

### 1. Obtener el código

Descarga o clona el repositorio del proyecto y abre la carpeta `MONGODB-MINIFORO`.

### 2. Configurar MongoDB

Por seguridad, evita guardar usuarios y contraseñas directamente en el repositorio. En `src/main/resources/application.properties`, utiliza:

```properties
spring.application.name=miniforo
spring.mongodb.database=miniforo
spring.mongodb.uri=${MONGODB_URI}
```

Define `MONGODB_URI` en tu entorno con la cadena de conexión de tu instancia. Por ejemplo, para MongoDB local:

```bash
export MONGODB_URI='mongodb://localhost:27017/miniforo'
```

En PowerShell:

```powershell
$env:MONGODB_URI='mongodb://localhost:27017/miniforo'
```

> **Aviso de seguridad:** el archivo `application.properties` incluido en la versión examinada del proyecto contiene credenciales incrustadas. Sustitúyelas por una variable de entorno y rota la contraseña expuesta antes de compartir el repositorio. Este README no reproduce dichas credenciales.

### 3. Iniciar la aplicación

En macOS o Linux:

```bash
./mvnw spring-boot:run
```

En Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

Una vez iniciada, prueba `GET http://localhost:8080/api/usuarios` desde un navegador, Postman o una herramienta similar. Si MongoDB no está disponible o la URI es incorrecta, las operaciones de base de datos pueden fallar.

### 4. Ejecutar pruebas

```bash
./mvnw test
```

## 👨‍💻 Autor y contacto

**Sneyder Rodríguez — Full-Stack Java Developer**

- [GitHub](https://github.com/SneyderRodriguez)
- [LinkedIn](https://www.linkedin.com/in/sneyder-rodriguez-ingeniero-de-sistemas/)
- [Portafolio](https://sneyderrodriguez.netlify.app/)

## 📄 Licencia

Este proyecto está disponible bajo la licencia **MIT**.

Puedes utilizar, modificar y distribuir el código respetando los términos establecidos en dicha licencia.

---

⭐ **MiniForo:** práctica de desarrollo backend, APIs REST y persistencia documental con MongoDB.

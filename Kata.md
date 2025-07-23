# API de Gestión de Personas

¡Bienvenido/a a esta Kata de programación! El objetivo es que implementes una API RESTful que te permita gestionar información de personas. Este ejercicio te ayudará a familiarizarte con **Java 11**, **Spring Boot 3.x** y las mejores prácticas para construir servicios web.

---

## Requisitos Generales

* **Lenguaje:** Java 11.
* **Framework:** Spring Boot 3.x.x.
* **Base de Datos:** Para simplificar la configuración inicial, usa una **base de datos en memoria** como H2 o HSQLDB. Sin embargo, el diseño de tu solución debe permitir una fácil adaptación a una base de datos relacional externa (como PostgreSQL o MySQL) si fuera necesario.
* **Gestión de Dependencias:** Puedes elegir entre **Maven** o **Gradle**.
* **Control de Versiones:** Utiliza **Git** para gestionar tu proyecto. Un historial de commits claro y significativo es valorado.

---

## Funcionalidades de la API (ABM de Persona)

Tu API debe exponer los siguientes *endpoints* REST para la entidad `Persona`.

### 1. Entidad `Persona`

La entidad `Persona` debe contener, al menos, estos atributos:

* `id` (Long): Identificador único de la persona, **generado automáticamente**.
* `nombre` (String): Nombre de la persona.
* `apellido` (String): Apellido de la persona.
* `fechaNacimiento` (LocalDate): Fecha de nacimiento de la persona.
* `email` (String): Correo electrónico de la persona, que debe ser **único**.

### 2. Endpoints REST

| Método HTTP | Endpoint                       | Descripción                                                                                               |
| :---------- | :----------------------------- | :-------------------------------------------------------------------------------------------------------- |
| `POST`      | `/api/v1/personas`             | **Crear Persona (Alta):** Permite registrar una nueva persona en el sistema. Debe retornar la persona creada, incluyendo su `id` generado. |
| `GET`       | `/api/v1/personas/{id}`        | **Obtener Persona por ID:** Permite recuperar los datos de una persona específica utilizando su `id`.      |
| `GET`       | `/api/v1/personas`             | **Listar Personas:** Retorna un listado de todas las personas registradas en el sistema.                     |
| `PUT`       | `/api/v1/personas/{id}`        | **Actualizar Persona (Modificación):** Permite actualizar todos los datos de una persona existente, identificada por su `id`. |
| `DELETE`    | `/api/v1/personas/{id}`        | **Eliminar Persona (Baja):** Permite eliminar una persona del sistema utilizando su `id`.                   |

---

## Consideraciones Adicionales

* **Manejo de Errores:** La API debe responder con **códigos de estado HTTP apropiados** para cada situación. Por ejemplo:
    * `200 OK` para éxito general.
    * `201 Created` para la creación exitosa.
    * `400 Bad Request` para solicitudes mal formadas o validaciones fallidas.
    * `404 Not Found` si el recurso solicitado no existe.
    * `409 Conflict` si se intenta crear una persona con un email ya registrado.
    * `500 Internal Server Error` para errores inesperados del servidor.
* **Validación de Datos:** Implementa **validaciones básicas** para los campos de la entidad `Persona` (ej. `nombre` y `apellido` no vacíos, `email` con formato válido y único).
* **Estructura del Proyecto:** Organiza tu código en **capas claras** (controladores, servicios, repositorios, entidades) siguiendo las buenas prácticas de Spring Boot. Puedes considerar usar DTOs (Data Transfer Objects) si crees que mejoran el diseño.
* **Pruebas:** Aunque sea a un nivel básico, se valorará la inclusión de **pruebas unitarias o de integración** para los controladores y/o servicios.

---

## Cómo Entregar la Solución

1.  Crea un nuevo proyecto de Spring Boot (puedes usar Spring Initializr para comenzar). Asegúrate de seleccionar **Java 11** como la versión de Java.
2.  Implementa la API siguiendo todos los requisitos.
3.  Asegúrate de que el proyecto pueda ser ejecutado fácilmente.
4.  Proporciona **instrucciones claras** en este mismo `README.md` sobre cómo levantar la aplicación y cómo probar cada *endpoint* (puedes incluir ejemplos con `curl` o Postman/Insomnia).
5.  Sube tu solución a un **repositorio público de Git** (GitHub, GitLab, Bitbucket).

---

## Instrucciones para Levantar y Probar la Aplicación (Ejemplo - ¡A completar por ti!)

1.  **Clonar el repositorio:**
    ```bash
    git clone [URL_DE_TU_REPOSITORIO]
    cd [NOMBRE_DEL_PROYECTO]
    ```
2.  **Configurar Java 11:** Asegúrate de que tu entorno tenga Java 11 configurado. Puedes verificarlo con `java -version`.
3.  **Construir el proyecto (ej. con Maven):**
    ```bash
    ./mvnw clean install
    ```
4.  **Ejecutar la aplicación:**
    ```bash
    ./mvnw spring-boot:run
    ```
    La API estará disponible en `http://localhost:8080`.

5.  **Ejemplos de `curl` para probar los *endpoints*:**

    * **Crear Persona:**
        ```bash
        curl -X POST -H "Content-Type: application/json" -d '{
            "nombre": "Ana",
            "apellido": "García",
            "fechaNacimiento": "1992-07-20",
            "email": "ana.garcia@example.com"
        }' http://localhost:8080/api/v1/personas
        ```

    * **Listar Personas:**
        ```bash
        curl http://localhost:8080/api/v1/personas
        ```

    * **Obtener Persona por ID (ej. ID 1):**
        ```bash
        curl http://localhost:8080/api/v1/personas/1
        ```

    * **Actualizar Persona (ej. ID 1):**
        ```bash
        curl -X PUT -H "Content-Type: application/json" -d '{
            "id": 1,
            "nombre": "Ana",
            "apellido": "García Actualizada",
            "fechaNacimiento": "1992-07-20",
            "email": "ana.garcia.nueva@example.com"
        }' http://localhost:8080/api/v1/personas/1
        ```

    * **Eliminar Persona (ej. ID 1):**
        ```bash
        curl -X DELETE http://localhost:8080/api/v1/personas/1
        ```

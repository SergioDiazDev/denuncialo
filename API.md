# API Documentación - Denuncialo

Este documento describe las rutas principales de la API y los datos que devuelven. Cada endpoint está documentado con su descripción, método HTTP, parámetros requeridos y el formato de la respuesta.

---

## Tabla de Contenidos

1. [Endpoints de Denuncias](#endpoints-de-denuncias)
    - [POST /denuncias](#post-denuncias)
    - [GET /denuncias](#get-denuncias)
    - [GET /denuncias/:zona](#get-denunciaszona)
    - ...

---

### Endpoints de Denuncias

#### POST /denuncias
- **Descripción**: Permite crear una nueva denuncia.
- **Método**: `POST`
- **Ruta**: `/denuncias`
- **Parámetros del Cuerpo** (formato JSON):
  - `ubicacion` (string): Coordenadas de la denuncia en formato "lat,lon".
  - `imagen_url` (string): URL de la imagen asociada.
  - `motivo` (string): Descripción de la denuncia.
  - ...
- **Respuesta**:
  - **Código 201** (Creado): Denuncia creada con éxito.
  - **Ejemplo de respuesta**:
    ```json
    {
      "success": true,
      "data": {
        "id": "unique-denuncia-id",
        "ubicacion": "40.4168,-3.7038",
        "imagen_url": "https://example.com/image.jpg",
        "motivo": "Descripción del motivo",
        "fecha_creacion": "2024-11-03T12:00:00Z",
        "estatus": "activa"
      }
    }
    ```
  - **Errores**:
    - **400**: Parámetros inválidos o faltantes.
    - **500**: Error en el servidor.

---

#### GET /denuncias
- **Descripción**: Obtiene todas las denuncias activas en el sistema.
- **Método**: `GET`
- **Ruta**: `/denuncias`
- **Respuesta**:
  - **Código 200** (OK): Lista de denuncias activas.
  - **Ejemplo de respuesta**:
    ```json
    {
      "success": true,
      "data": [
        {
          "id": "unique-denuncia-id",
          "ubicacion": "40.4168,-3.7038",
          "imagen_url": "https://example.com/image.jpg",
          "motivo": "Descripción del motivo",
          "fecha_creacion": "2024-11-03T12:00:00Z",
          "estatus": "activa"
        },
        {
          "id": "another-denuncia-id",
          "ubicacion": "37.7749,-122.4194",
          "imagen_url": "https://example.com/another_image.jpg",
          "motivo": "Otro motivo de denuncia",
          "fecha_creacion": "2024-11-02T08:30:00Z",
          "estatus": "activa"
        }
      ]
    }
    ```
  - **Errores**:
    - **500**: Error en el servidor.

---

#### GET /denuncias/:zona
- **Descripción**: Obtiene denuncias filtradas por una zona específica.
- **Método**: `GET`
- **Ruta**: `/denuncias/:zona`
- **Parámetros de la Ruta**:
  - `zona` (string): Nombre o identificador de la zona para filtrar.
- **Respuesta**:
  - **Código 200** (OK): Lista de denuncias filtradas por zona.
  - **Ejemplo de respuesta**:
    ```json
    {
      "success": true,
      "data": [
        {
          "id": "denuncia-id-en-zona",
          "ubicacion": "40.4168,-3.7038",
          "imagen_url": "https://example.com/image.jpg",
          "motivo": "Motivo específico en la zona",
          "fecha_creacion": "2024-11-03T14:00:00Z",
          "estatus": "activa"
        }
      ]
    }
    ```
  - **Errores**:
    - **404**: Zona no encontrada o sin denuncias.
    - **500**: Error en el servidor.

---

Este formato en `API.md` facilita la comprensión y el uso de la API a cualquier desarrollador. Si se necesitan más detalles, como autorizaciones o validaciones, se pueden añadir secciones extra para aclarar cada punto.

# Esquema de Base de Datos

## Tabla: `denuncias`

| **Campo**         | **Tipo de Dato**       | **Descripción**                                         |
|-------------------|------------------------|---------------------------------------------------------|
| `id`              | `SERIAL PRIMARY KEY`   | Identificador único de la denuncia.                     |
| `lat`             | `DECIMAL(9, 6)`        | Latitud de la ubicación de la denuncia.                 |
| `lon`             | `DECIMAL(9, 6)`        | Longitud de la ubicación de la denuncia.                |
| `motivo`          | `VARCHAR(255)`         | Motivo de la denuncia.                                  |
| `descripcion`     | `TEXT`                 | Descripción detallada de la denuncia (opcional).       |
| `etiqueta`        | `VARCHAR(255)`         | Etiqueta de la denuncia.                                  |
| `imagen_url`      | `VARCHAR(255)`         | URL de la imagen asociada (opcional).                   |
| `fecha_hora`      | `TIMESTAMP`            | Fecha y hora en que se realizó la denuncia (por defecto, la fecha actual). |
| `tipo_denuncia`   | `VARCHAR(50)`          | Tipo de denuncia (opcional).                            |
| `estado`          | `VARCHAR(50)`          | Estado de la denuncia (por defecto, "pendiente").      |

## Tabla: `usuarios`

| **Campo**         | **Tipo de Dato**       | **Descripción**                                         |
|-------------------|------------------------|---------------------------------------------------------|
| `id`              | `SERIAL PRIMARY KEY`   | Identificador único del usuario.                        |
| `nick`            | `VARCHAR(100) UNIQUE`  | Nombre del usuario.                                     |
| `pass_hash`       | `VARCHAR(255)`         | Contraseña del usuario (almacenada como hash).         |
| `huella`          | `VARCHAR(255)`         | Huella digital única del usuario (para validación).    |
| `admin`           | `BOOLEAN`              | Indica si el usuario es administrador (TRUE o FALSE).  |
| `fecha_registro`  | `TIMESTAMP`            | Fecha en que se registró el usuario (por defecto, la fecha actual). |

## Tabla: `denuncias_usuarios`

| **Campo**         | **Tipo de Dato**       | **Descripción**                                         |
|-------------------|------------------------|---------------------------------------------------------|
| `id`              | `SERIAL PRIMARY KEY`   | Identificador único de la relación.                     |
| `denuncia_id`     | `INT`                  | Referencia a `denuncias.id`, para asociar la denuncia con el usuario. |
| `usuario_id`      | `INT`                  | Referencia a `usuarios.id`, para asociar la denuncia con el usuario. |
| **Restricciones**  |                        | `UNIQUE(denuncia_id, usuario_id)` para evitar duplicados. |
| **FOREIGN KEY**    |                        | `FOREIGN KEY (denuncia_id) REFERENCES denuncias(id), FOREIGN KEY (usuario_id) REFERENCES usuarios(id)` |

## Tabla: `validaciones`

| **Campo**         | **Tipo de Dato**       | **Descripción**                                         |
|-------------------|------------------------|---------------------------------------------------------|
| `id`              | `SERIAL PRIMARY KEY`   | Identificador único de la validación.                  |
| `denuncia_id`     | `INT`                  | Referencia a `denuncias.id`, para asociar la validación con la denuncia. |
| `usuario_id`      | `INT`                  | Referencia a `usuarios.id`, para asociar la validación con el usuario que la realizó. |
| `fecha_validacion`| `TIMESTAMP`            | Fecha y hora en que se realizó la validación (por defecto, la fecha actual). |

### Restricciones

- **FOREIGN KEY**: 
  - `FOREIGN KEY (denuncia_id) REFERENCES denuncias(id)`
  - `FOREIGN KEY (usuario_id) REFERENCES usuarios(id)`

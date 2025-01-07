# Movies API

## Descripción ( ⚠️ Proyecto para portfolio del curso de midudev ⚠️ )
Esta es una API RESTful construida con **Express.js** que permite gestionar un catálogo de películas. Incluye operaciones CRUD (Crear, Leer, Actualizar, Eliminar) y utiliza validaciones para garantizar la integridad de los datos.

## Características principales
- **CORS configurado**: Permite orígenes específicos definidos en una lista blanca.
- **Rutas principales**: `/movies` y `/movies/:id` para gestionar películas.
- **Validaciones**: Utiliza esquemas definidos para validar la estructura de las películas antes de procesarlas.
- **UUID para identificación**: Los recursos se identifican con identificadores únicos generados con `crypto.randomUUID()`.
- **Middleware**: Incluye middlewares para JSON, CORS y deshabilitar el encabezado `X-Powered-By` por seguridad.

## Requisitos
- **Node.js** versión 18 o superior.
- Archivo `movies.json` que contenga una lista inicial de películas.

## Instalación
1. Clona este repositorio:
   ```bash
   git clone <url-del-repositorio>
   cd <nombre-del-repositorio>
   ```

2. Instala las dependencias:
   ```bash
   npm install
   ```

3. Asegúrate de tener un archivo `movies.json` en la raíz del proyecto con una estructura como esta:
   ```json
   [
     {
       "id": "1",
       "title": "Inception",
       "genre": ["Sci-Fi", "Action"],
       "year": 2010
     }
   ]
   ```

4. Inicia el servidor:
   ```bash
   npm start
   ```
   El servidor estará disponible en `http://localhost:1234`.

## Endpoints

### **GET /movies**
Obtiene la lista de todas las películas. 
Opcionalmente, puedes filtrar por género usando el parámetro de consulta `genre`.

- **Parámetros opcionales**:
  - `genre`: Filtra películas por género (insensible a mayúsculas).

#### Ejemplo de respuesta:
```json
[
  {
    "id": "1",
    "title": "Inception",
    "genre": ["Sci-Fi", "Action"],
    "year": 2010
  }
]
```

### **GET /movies/:id**
Obtiene una película por su identificador único.

- **Respuesta 200**: Devuelve la película.
- **Respuesta 404**: Película no encontrada.

#### Ejemplo de respuesta:
```json
{
  "id": "1",
  "title": "Inception",
  "genre": ["Sci-Fi", "Action"],
  "year": 2010
}
```

### **POST /movies**
Crea una nueva película.

- **Cuerpo requerido**:
  ```json
  {
    "title": "string",
    "genre": ["string"],
    "year": 2023
  }
  ```

- **Respuesta 201**: Película creada con éxito.
- **Respuesta 400**: Datos inválidos.

#### Ejemplo de respuesta:
```json
{
  "id": "2",
  "title": "Interstellar",
  "genre": ["Sci-Fi", "Drama"],
  "year": 2014
}
```

### **DELETE /movies/:id**
Elimina una película por su identificador único.

- **Respuesta 200**: Película eliminada.
- **Respuesta 404**: Película no encontrada.

#### Ejemplo de respuesta:
```json
{
  "message": "Movie deleted"
}
```

### **PATCH /movies/:id**
Actualiza parcialmente una película por su identificador único.

- **Cuerpo permitido**: Los campos que se desean actualizar.
  ```json
  {
    "title": "string",
    "genre": ["string"],
    "year": 2023
  }
  ```

- **Respuesta 200**: Película actualizada con éxito.
- **Respuesta 400**: Datos inválidos.
- **Respuesta 404**: Película no encontrada.

#### Ejemplo de respuesta:
```json
{
  "id": "2",
  "title": "Interstellar Updated",
  "genre": ["Sci-Fi", "Drama"],
  "year": 2014
}
```

## Configuración de CORS
El middleware CORS está configurado para aceptar solicitudes únicamente de los orígenes:
- `http://localhost:8080`
- `http://localhost:1234`

Si necesitas añadir más orígenes, puedes hacerlo en la constante `ACCEPTED_ORIGINS` dentro del archivo principal.

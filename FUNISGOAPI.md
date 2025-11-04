🎬 FunisGo API - Documentación Completa

📖 Descripción General

FunisGo API es una API RESTful robusta para gestión de contenido multimedia (películas, series, canales) con sistema de autenticación, límites de uso, y administración completa. Desarrollada con Flask y Firebase Firestore.

🚀 Características Principales

🔐 Autenticación y Seguridad

· Sistema de tokens JWT-like con renovación automática
· Rate limiting por IP y usuario
· Restricciones de dominio para tokens web
· Control de colecciones por token
· Validación de permisos granular

📊 Gestión de Usuarios y Planes

· Plan Free: Límites diarios y de sesión
· Plan Premium: Acceso completo e ilimitado
· Sistema de administración completo
· Notificaciones automáticas por email

🎭 Gestión de Contenido

· Películas, Series y Canales con estructura normalizada
· Sistema de streams con límites diarios
· Búsqueda avanzada con filtros por plan
· Endpoints genéricos para colecciones adicionales

🛠️ Operaciones CRUD

· Crear, leer, actualizar, eliminar contenido
· Validación de estructura de datos
· Metadatos automáticos (creación, actualización)
· Sistema de reportes para contenido

📋 Endpoints Principales

🔐 Autenticación

Método Endpoint Descripción
POST /api/auth/register Registro público (siempre plan Free)
POST /api/auth/login Login con token
GET /api/auth/verify Verificar token

👤 Usuario

Método Endpoint Descripción
GET /api/user/info Información del usuario actual
GET /api/plan-comparison Comparación de planes

🎬 Contenido

Método Endpoint Descripción
GET /api/peliculas Listar películas
GET /api/peliculas/{id} Obtener película específica
GET /api/series Listar series
GET /api/series/{id} Obtener serie específica
GET /api/canales Listar canales
GET /api/canales/{id} Obtener canal específico
GET /api/buscar?q={term} Buscar contenido
GET /api/stream/{id} Obtener URL de streaming
GET /api/contenido/recientes Contenido recientemente agregado
GET /api/contenido/animes Contenido de anime

➕ Creación y Edición (Admin/Premium)

Método Endpoint Descripción
POST /api/peliculas Crear película
PUT /api/peliculas/{id} Actualizar película
DELETE /api/peliculas/{id} Eliminar película
POST /api/series Crear serie
PUT /api/series/{id} Actualizar serie
DELETE /api/series/{id} Eliminar serie
POST /api/canales Crear canal
PUT /api/canales/{id} Actualizar canal
DELETE /api/canales/{id} Eliminar canal

📊 Administración (Solo Admin)

Método Endpoint Descripción
POST /api/admin/create-user Crear usuario
GET /api/admin/users Listar usuarios
POST /api/admin/update-limits Actualizar límites
POST /api/admin/change-plan Cambiar plan
POST /api/admin/reset-limits Resetear límites
POST /api/admin/regenerate-token Regenerar token
GET /api/admin/usage-statistics Estadísticas de uso
POST /api/generate-frontend-token Generar token para frontend

🐛 Sistema de Reportes

Método Endpoint Descripción
POST /api/reports Crear reporte
GET /api/reports Listar reportes (admin)
PUT /api/reports/{id} Actualizar reporte (admin)
GET /api/reports/statistics Estadísticas de reportes

🔧 Sistema y Salud

Método Endpoint Descripción
GET /health Health check para Render
GET /api/connection/status Estado de conexión Firebase
POST /api/connection/reconnect Reconexión forzada (admin)
GET /api/diagnostic Diagnóstico completo

🔐 Autenticación

Uso de Tokens

```http
Authorization: Bearer {token}
```

O mediante query parameter:

```http
GET /api/peliculas?token={token}
```

Tipos de Tokens

1. Tokens de Administrador: Acceso completo al sistema
2. Tokens de Usuario: Acceso según plan (Free/Premium)
3. Tokens para Frontend: Acceso restringido a colecciones específicas

📈 Límites y Planes

Plan Free

· 200 requests diarios
· 10 requests por sesión
· 10 streams diarios
· Búsqueda limitada (5 resultados)
· Acceso básico a metadata

Plan Premium

· 30,000 requests diarios
· 2,000 requests por sesión
· Streams ilimitados
· Búsqueda avanzada (50 resultados)
· Acceso completo a todas las características

🗃️ Estructura de Datos

Película

```json
{
  "id": "string",
  "title": "string",
  "poster": "string",
  "description": "string",
  "year": "string",
  "genre": "string",
  "rating": "string",
  "play_links": [
    {
      "server": "string",
      "url": "string"
    }
  ],
  "type": "string",
  "add": "string"
}
```

Serie

```json
{
  "id": "string",
  "title": "string",
  "poster": "string", 
  "description": "string",
  "year": "string",
  "genre": "string",
  "rating": "string",
  "total_seasons": "number",
  "status": "string",
  "seasons": [
    {
      "season_number": "number",
      "episode_count": "number",
      "year": "string",
      "episodes": [
        {
          "episode_number": "number",
          "title": "string",
          "duration": "string",
          "description": "string",
          "play_links": []
        }
      ]
    }
  ],
  "type": "string",
  "add": "string"
}
```

Canal

```json
{
  "id": "string",
  "name": "string",
  "logo": "string",
  "status": "string",
  "category": "string", 
  "country": "string",
  "stream_options": [
    {
      "option_name": "string",
      "stream_url": "string"
    }
  ]
}
```

🛠️ Configuración

Variables de Entorno Requeridas

```bash
# Firebase
FIREBASE_TYPE=service_account
FIREBASE_PROJECT_ID=your-project-id
FIREBASE_PRIVATE_KEY=your-private-key
FIREBASE_CLIENT_EMAIL=your-client-email

# Administración
ADMIN_EMAIL=admin@example.com
ADMIN_TOKEN=your-admin-token
```

Instalación y Ejecución

```bash
# Instalar dependencias
pip install flask flask-cors firebase-admin requests

# Configurar variables de entorno
export FIREBASE_PROJECT_ID="tu-proyecto"
export FIREBASE_PRIVATE_KEY="tu-clave-privada"
export ADMIN_TOKEN="token-admin-secreto"

# Ejecutar
python app.py
```

🔄 Endpoints Genéricos

La API incluye endpoints automáticos para colecciones adicionales:

· listas - Listas de contenido
· reports - Sistema de reportes
· sagas - Sagas y colecciones
· trending - Contenido popular

Cada colección tiene endpoints CRUD automáticos:

· GET /api/{coleccion} - Listar
· GET /api/{coleccion}/{id} - Obtener específico
· POST /api/{coleccion} - Crear
· PUT /api/{coleccion}/{id} - Actualizar
· DELETE /api/{coleccion}/{id} - Eliminar

📞 Ejemplos de Uso

Registro de Usuario

```javascript
const userData = {
  "username": "nuevo_usuario",
  "email": "usuario@ejemplo.com",
  "password": "contraseña_segura"
};

const response = await fetch('/api/auth/register', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(userData)
});

const result = await response.json();
console.log(result.user.token); // Token para futuras requests
```

Obtener Películas

```javascript
const response = await fetch('/api/peliculas', {
  headers: {
    'Authorization': 'Bearer TU_TOKEN'
  }
});

const data = await response.json();
console.log(data.data); // Array de películas
```

Buscar Contenido

```javascript
const response = await fetch('/api/buscar?q=avengers&limit=10', {
  headers: {
    'Authorization': 'Bearer TU_TOKEN'
  }
});
```

Reproducir Contenido

```javascript
// Para películas
const response = await fetch('/api/stream/movie-123', {
  headers: {
    'Authorization': 'Bearer TU_TOKEN'
  }
});

const streamData = await response.json();
// Usar streamData.streaming_url para reproducir

// Para series (especificar temporada y episodio)
const response = await fetch('/api/stream/serie-456?season=1&episode=2', {
  headers: {
    'Authorization': 'Bearer TU_TOKEN'
  }
});
```

Crear Reporte

```javascript
const report = {
  "contentId": "movie-123",
  "contentType": "pelicula",
  "contentTitle": "Avengers Endgame", 
  "reportType": "general",
  "reason": "broken_link",
  "comment": "El enlace de streaming no funciona",
  "userEmail": "usuario@ejemplo.com"
};

const response = await fetch('/api/reports', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer TU_TOKEN',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(report)
});
```

Crear Película (Admin/Premium)

```javascript
const movieData = {
  "title": "Nueva Película",
  "image_url": "https://ejemplo.com/poster.jpg",
  "sinopsis": "Descripción de la película",
  "details": {
    "year": "2024",
    "genres": ["Acción", "Aventura"],
    "rating": "8.5",
    "actors": ["Actor 1", "Actor 2"],
    "duration": "120 min",
    "director": "Director Ejemplo"
  },
  "play_links": [
    {
      "server": "Server 1",
      "url": "https://ejemplo.com/stream"
    }
  ],
  "type": "",
  "add": "yes"
};

const response = await fetch('/api/peliculas', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer TU_TOKEN',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(movieData)
});
```

🐛 Troubleshooting

Error de Conexión Firebase

```bash
# Verificar estado
GET /api/connection/status

# Forzar reconexión (admin)
POST /api/connection/reconnect
```

Límites Excedidos

· Los usuarios Free reciben notificaciones automáticas
· Los límites se reinician automáticamente cada 24 horas
· Contactar administrador para aumentar límites

Tokens Inválidos

· Verificar formato: Authorization: Bearer {token}
· Regenerar token desde panel de administración
· Verificar restricciones de dominio (para tokens web)

Códigos de Estado HTTP

Código Significado Acción
200 ✅ Success Todo OK
400 ❌ Bad Request Revisar datos enviados
401 🔒 Unauthorized Token inválido o faltante
403 🚫 Forbidden Sin permisos para la operación
404 🔍 Not Found Recurso no encontrado
429 ⚠️ Too Many Requests Límites excedidos
500 💥 Server Error Error interno del servidor

🎯 Características Avanzadas

Sistema de Notificaciones

· Notificaciones automáticas por email al alcanzar límites
· Soporte para webhook.email y Formspree
· Plantillas HTML personalizadas

Control de Acceso por Dominio

```javascript
// Al crear token para frontend
const frontendTokenData = {
  "plan_type": "free",
  "allowed_domains": ["https://midominio.com", "https://app.midominio.com"],
  "allowed_collections": ["peliculas", "series"],
  "can_create_content": false,
  "can_edit_content": false,
  "can_delete_content": false
};
```

Validación de Estructura

La API valida automáticamente la estructura de:

· Películas (campos obligatorios, play_links, details)
· Series (seasons, episodes, estructura anidada)
· Canales (stream_options, campos requeridos)

Normalización de Datos

· IDs automáticos desde títulos
· Estructura consistente across endpoints
· Filtrado de campos vacíos o nulos

📊 Monitoreo y Métricas

Endpoints de Diagnóstico

· /health - Health check para servicios de deploy
· /api/diagnostic - Diagnóstico completo del sistema
· /api/connection/status - Estado de Firebase

Estadísticas de Uso

· Requests diarios y por sesión
· Streams reproducidos
· Usuarios activos por plan
· Métricas de rendimiento

🔒 Seguridad

Características Implementadas

· Rate limiting por IP y usuario
· Validación de dominios para tokens web
· Sanitización de inputs
· Headers de seguridad HTTP
· Validación de estructura de datos
· Control de acceso por colección

Best Practices

· Usar siempre HTTPS en producción
· Rotar tokens regularmente
· Validar dominios en tokens de frontend
· Monitorear logs de acceso
· Revisar reportes de usuarios

📄 Licencia

Este proyecto está bajo licencia MIT.

🤝 Contribuciones

Las contribuciones son bienvenidas. Por favor:

1. Fork el proyecto
2. Crea una rama para tu feature
3. Commit tus cambios
4. Push a la rama
5. Abre un Pull Request

📞 Soporte

Para soporte técnico:

· Revisar documentación en /api/diagnostic
· Verificar logs de la aplicación
· Contactar al administrador del sistema
· Usar el sistema de reportes para problemas con contenido

---

API Name: FunisGo API
Versión: 2.0.0
Framework: Flask + Firebase Firestore
Última Actualización: ${new Date().toLocaleDateString()}

Para consultas sobre administración o acceso premium, contacta con el administrador del sistema.
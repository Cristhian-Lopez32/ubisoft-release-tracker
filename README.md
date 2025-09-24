**README — Mi Web (SPA React / Vite)**
Este documento explica en detalle cómo funciona la web (SPA) que migró del proyecto anterior hacia una version en React + Vite, donde se incluye,
cómo instalarlo localmente y cómo probar las funciones principales.
Resumen del proyecto

Esta aplicación es una Single Page Application (SPA) construida con React, con una plantilla base generada con vite
Navegación con React Router (/, /login, /register, /events).
Formularios validados:

Registro / Login (persisten usuarios en localStorage).

Buscar juegos (valida mínimo 2 caracteres) que llama a la API externa RAWG.

Crear evento (modal) — solamente para usuarios autenticados — guardado en localStorage.

Uso de hooks (useState, useEffect, useContext) y AuthContext para el estado de sesión.

Paginación (botón Cargar más), select para filtrar por tiempo: Próximos / Recientes / Todos.

Cuenta regresiva (countdown) por tarjeta de juego (actualiza cada segundo).

**Requisitos previos**

Node.js (v16+) y npm instalados.

Editor (VS Code recomendado).

**Instalación y ejecución**

1. Clonar / colocar proyecto en una carpeta:

cd <carpeta-del-proyecto>


2. Instalar dependencias:

npm install


3. Crear archivo de entorno (.env) en la raíz (opcional para pruebas con RAWG):

VITE_RAWG_KEY=tu_rawg_key_aqui


4. Levantar servidor de desarrollo:

npm run dev
Vite normalmente expone la app en http://localhost:5173.

**Funciones principales y flujo de datos
Registro / Login**

**Register.jsx:**

Verifica campos (no vacíos), password === password2.

Rechaza username/email duplicado (mira app_users_v1).

Crea usuario { id, username, email, passwordHash, createdAt }.

Guarda usuario y marca sesión (app_current_user_v1).

**Login.jsx:**

Comprueba credenciales con localStorage.

Buscar juegos (formulario validado + API RAWG)

Usuario escribe término (≥2 chars) → submit → searchGames(query) → fetch RAWG.

Resultados se muestran como GameCard (countdown incluido).

Si input vacío, el listado usa el filtro timeRange y llamadas a fetchUpcomingRawg.

Paginación: page + botón Cargar más -> consulta siguiente página y concatena resultados.

**Eventos**
Solo usuarios autenticados (ruta protegida).

Crear evento: modal con title, datetime, description → validación mínima → guarda en app_events_v1.

Listado de eventos del usuario: filtra por ownerId.

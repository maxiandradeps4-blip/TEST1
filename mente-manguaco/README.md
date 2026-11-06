# Mente Manguaco

Juego web multijugador de respuestas simultáneas. Funciona como sitio estático en GitHub Pages; Firebase Realtime Database sincroniza las salas entre jugadores.

## Reglas implementadas

- Una persona crea una sala y comparte el código de cinco caracteres.
- Cada ronda muestra una pregunta para todos. Cada jugador envía una respuesta privada; el anfitrión revela cuando quiera.
- Las respuestas iguales que forman el grupo más grande dan una vaca común a cada persona de ese grupo. Si hay empate entre respuestas más repetidas, ambos grupos reciben vaca.
- Una respuesta que nadie más dio entrega una vaca rosada. Las respuestas que coinciden con otras, pero no quedan entre las más repetidas, no puntúan.
- Con 3 vacas rosadas quedas fuera. Gana quien llegue primero a 5 vacas comunes y tenga menos de 3 rosadas.
- Máximo 12 jugadores por sala. La sala se mantiene mientras exista en Firebase.

## Configurar Firebase (una vez)

1. En [Firebase Console](https://console.firebase.google.com/), crea un proyecto.
2. En **Authentication > Sign-in method**, activa **Anonymous**.
3. En **Realtime Database**, crea una base de datos. Copia su URL (por ejemplo `https://mi-proyecto-default-rtdb.firebaseio.com`).
4. En la configuración del proyecto, crea una aplicación web y copia sus valores de configuración.
5. En `index.html`, reemplaza `PEGA_API_KEY`, `PEGA_PROJECT_ID` y `PEGA_APP_ID` por los valores reales. En `databaseURL`, pega la URL exacta de tu Realtime Database.
6. En **Realtime Database > Rules**, configura estas reglas para una primera versión jugable:

```json
{
  "rules": {
    "rooms": {
      "$room": {
        ".read": "auth != null",
        ".write": "auth != null"
      }
    }
  }
}
```

Las reglas permiten a cualquier usuario autenticado anónimamente leer y modificar datos de cualquier sala. Son simples para una partida entre amigos, pero no validan las acciones desde el servidor; no uses esto para manejar datos sensibles ni para partidas competitivas.

## Publicar con GitHub Pages

1. Crea un repositorio en GitHub y sube `index.html`, la carpeta `assets/` (incluye la gráfica de portada) y este README si quieres. No cambies la ubicación de `assets/mente-manguaco-portada.jpg`, porque la página la carga desde ahí.
2. Abre **Settings > Pages**.
3. En **Build and deployment**, selecciona **Deploy from a branch**, elige `main` y `/ (root)`, y guarda.
4. GitHub te dará una dirección pública. Comparte esa dirección y el código de sala con tus amigos.

Para probar en local, sirve la carpeta con cualquier servidor estático (por ejemplo `python3 -m http.server 8000`) y abre `http://localhost:8000`. Firebase Authentication no funciona de forma fiable abriendo el HTML con doble clic (`file://`).

## Personalizar preguntas

En `index.html`, edita el arreglo `questions` dentro del bloque `<script type="module">`.

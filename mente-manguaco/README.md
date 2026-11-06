# Mente Manguaco

Juego web multijugador de respuestas simultáneas. Funciona como sitio estático en GitHub Pages; Firebase Realtime Database sincroniza las salas entre jugadores.

## Reglas implementadas

- Una persona crea una sala y comparte el código de cinco caracteres.
- Cada ronda muestra una pregunta para todos. Cada jugador envía una respuesta privada; el anfitrión revela cuando quiera.
- Las respuestas iguales que forman el grupo más grande dan una vaca común a cada persona de ese grupo. Si hay empate entre respuestas más repetidas, ambos grupos reciben vaca.
- Una respuesta que nadie más dio entrega una vaca rosada. Las respuestas que coinciden con otras, pero no quedan entre las más repetidas, no puntúan.
- Con 3 vacas rosadas quedas fuera. Gana quien llegue primero a 5 vacas comunes y tenga menos de 3 rosadas.
- Máximo 12 jugadores por sala. La sala se mantiene mientras exista en Firebase.

## Conexión multijugador

El juego incluye el cliente PeerJS dentro de `assets/peerjs.min.js`, así no depende de un CDN externo para cargarlo. No requiere claves de Firebase ni un backend propio. Cada sala se identifica con un código aleatorio de cinco caracteres; el anfitrión mantiene el estado y sincroniza las respuestas, el marcador y las rondas.

PeerJS usa su servidor público de señalización. La conexión directa puede depender de las redes y cortafuegos de cada jugador; si una red bloquea WebRTC, prueben desde otra conexión o navegador. La licencia MIT del cliente está incluida en `PEERJS-LICENSE.txt`.

## Publicar con GitHub Pages

1. Crea un repositorio en GitHub y sube `index.html`, la carpeta `assets/` (incluye la gráfica de portada) y este README si quieres. No cambies la ubicación de `assets/mente-manguaco-portada.jpg`, porque la página la carga desde ahí.
2. Abre **Settings > Pages**.
3. En **Build and deployment**, selecciona **Deploy from a branch**, elige `main` y `/ (root)`, y guarda.
4. GitHub te dará una dirección pública. Comparte esa dirección y el código de sala con tus amigos.

Para probar en local, sirve la carpeta con cualquier servidor estático (por ejemplo `python3 -m http.server 8000`) y abre `http://localhost:8000`.

## Personalizar preguntas

En `index.html`, edita el arreglo `questions` dentro del bloque `<script type="module">`.

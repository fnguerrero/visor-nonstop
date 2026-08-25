# TODO — Plataformero

Estados: `[ ]` pendiente · `[x]` hecho y verificado · `[!]` bloqueado (con motivo)

**Todo completo.** 55/55 tests en `tests.html`, 10/10 niveles en `tools/validar.js`.

## Base

- [x] Andamiaje: `index.html`, `css/style.css`, canvas 480x272 escalado, orden de `<script>`
- [x] `js/input.js`: teclado, mapeo de teclas, estado pressed/justPressed
- [x] `js/engine.js`: game loop con delta time fijo, FPS, máquina de estados
- [x] `js/tiles.js`: catálogo de tiles, parser de tilemap de strings, dibujo del mundo
- [x] `js/physics.js`: AABB, resolución de colisión por eje, consulta de tiles sólidos

## Jugador

- [x] `js/player.js`: movimiento horizontal con aceleración/fricción y sprint
- [x] Salto de altura variable + gravedad + coyote time + jump buffer
- [x] Estados del jugador: chico/grande, invencibilidad, daño, muerte y respawn
- [x] Dibujo del jugador por código (con animación de correr y salto)

## Mundo

- [x] `js/camera.js`: scroll horizontal con lookahead y clamp a los bordes del nivel
- [x] `js/world.js`: carga del nivel, dibujo del mundo y fondo por tema
- [x] Bloques interactivos: `?` con item, ladrillo rompible, bloque sólido
- [x] Plataformas móviles y plataformas que caen
- [x] Peligros: pinchos, lava, agua, caída al vacío

## Entidades

- [x] `js/entities.js`: base de entidad, spawn desde tilemap, update/draw/pool
- [x] Enemigo 1 — caminante (patrulla, no se cae de los bordes, se mata pisándolo)
- [x] Enemigo 2 — saltarín (salta hacia el jugador si lo tiene cerca)
- [x] Enemigo 3 — volador (patrulla horizontal + oscilación vertical)
- [x] Coleccionables: monedas y vida extra
- [x] Power-ups: hongo (crecer) y estrella (invencible 9 seg)
- [x] Meta: bandera de fin de nivel

## Niveles

- [x] `js/levels.js`: estructura de nivel y los 10 tilemaps
- [x] Niveles 1-3 (básicos: correr, saltar, primer enemigo, monedas)
- [x] Niveles 4-7 (combinan: plataformas móviles, pinchos, power-ups, voladores)
- [x] Niveles 8-10 (precisión: saltos justos, enemigos combinados, nivel final)
- [x] `js/validator.js`: validador de niveles (alcanzabilidad por BFS, tiles, spawn, meta)

## UI y sistemas

- [x] `js/hud.js`: vidas, monedas, puntaje, tiempo, nivel actual
- [x] Pantallas: menú, selección de nivel, pausa, muerte, nivel completado, game over, final
- [x] `js/save.js`: progreso en localStorage (nivel desbloqueado, mejor puntaje)
- [x] `js/audio.js`: efectos sintetizados con WebAudio (salto, moneda, daño, power-up, meta)

## Verificación final

- [x] Correr el validador sobre los 10 niveles y que pase — 10/10
- [x] Probar en navegador: 0 errores de consola, menú y partida funcionando
- [x] Batería automatizada `tests.html` — 55/55
- [x] Verificar cada criterio de aceptación de SPEC.md uno por uno — 13/13
- [x] Escribir `README.md` y `.nonstop/INFORME.md`

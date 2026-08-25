# SPEC — Plataformero (tipo Mario, 10 niveles)

## Objetivo

Un juego de plataformas 2D estilo Mario, jugable en el navegador, con 10 niveles de
dificultad progresiva. HTML + JavaScript puro, sin dependencias ni assets externos:
se abre el `index.html` y anda. Gráficos y sonido generados por código.

## Alcance

**Entra:**
- Motor propio: game loop con delta time, física AABB, cámara con scroll horizontal.
- Jugador: correr, sprint, salto de altura variable, coyote time, jump buffer, muerte y respawn.
- 10 niveles con mecánicas introducidas de forma progresiva.
- Enemigos (3 tipos), peligros, coleccionables, power-ups, bloques interactivos.
- HUD, menú, pausa, selección de niveles, game over, pantalla final.
- Progreso guardado en `localStorage`.
- Sonido sintetizado con WebAudio (sin archivos de audio).
- Validador automático de niveles (chequea que cada nivel sea completable).

**NO entra:**
- Scroll vertical / niveles verticales. Todos los niveles son horizontales.
- Multijugador, online, leaderboards.
- Sprites o audio en archivos externos (todo dibujado/sintetizado por código).
- Soporte mobile / touch. Teclado únicamente.
- Editor de niveles.

## Stack y decisiones

- **HTML + Canvas 2D + JS vanilla.** Cero dependencias, cero build step.
- **Scripts clásicos** (`<script src>`), NO módulos ES6. Motivo: los módulos ES6 fallan
  con `file://` por CORS; con scripts clásicos el juego funciona haciendo doble click en
  `index.html`, sin servidor.
- **Namespace global único** `G` para compartir estado entre archivos.
- **Niveles como tilemaps de strings** — un array de líneas por nivel, legible y editable
  a mano.
- **Gráficos procedurales**: todo dibujado con primitivas de canvas.
- **Resolución interna fija** 480x270, escalada con `image-rendering: pixelated`.
  Mantiene el look pixel-art y hace la física independiente del tamaño de ventana.

## Supuestos

Ambigüedades resueltas por criterio propio (esta sección crece durante el trabajo):

1. **"Tipo Mario" = plataformero clásico 2D**, scroll lateral, pisar enemigos, monedas,
   bloques `?`, bandera al final. No es un clon exacto ni usa assets de Nintendo.
2. **Sin assets propietarios.** Todo original y generado por código, para que no haya
   problema de derechos ni archivos binarios en el repo.
3. **Dificultad progresiva**: niveles 1-3 introducen lo básico, 4-7 combinan mecánicas,
   8-10 exigen precisión. Cada nivel nuevo introduce como mucho una mecánica nueva.
4. **Vidas**: 3 al empezar, se pierde una al morir, game over al llegar a 0, se vuelve al
   menú conservando el progreso de niveles desbloqueados.
5. **Controles**: flechas / WASD para mover, Space / W / ↑ para saltar, Shift para correr,
   P o Esc para pausa. Se documentan en pantalla.
6. **Idioma**: todos los textos en pantalla en español.
7. **Navegador objetivo**: Chrome/Firefox de escritorio, actual. Sin polyfills.

## Criterios de aceptación

Condiciones verificables. Todas tienen que pasar para dar el trabajo por terminado.

1. `index.html` abre sin errores en la consola del navegador (0 errores).
2. El juego arranca en el menú y se puede empezar a jugar con el teclado.
3. Existen exactamente **10 niveles** definidos y todos cargan sin error.
4. El **validador de niveles pasa en los 10**: spawn válido, meta presente, sin tiles
   desconocidos, sin huecos más anchos que el salto máximo del jugador, sin muros más
   altos que la altura de salto.
5. El jugador puede **morir y reaparecer** (por enemigo, por pincho y por caer al vacío).
6. Pisar un enemigo lo elimina; tocarlo de costado daña al jugador.
7. Las **monedas se recolectan** y el contador del HUD sube.
8. Los **power-ups funcionan**: hongo agranda al jugador, estrella da invencibilidad temporal.
9. Tocar la **bandera completa el nivel** y desbloquea el siguiente.
10. El **progreso persiste** en `localStorage` entre recargas.
11. Completar el nivel 10 muestra la **pantalla de final del juego**.
12. La **pausa** detiene la simulación y se puede reanudar.
13. El juego corre a ~60 FPS estables sin fugas de memoria evidentes.

## Presupuesto

Máximo **40 iteraciones**. Si se alcanza, frenar y reportar estado sin borrar nada.

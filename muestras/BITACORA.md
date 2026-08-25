# Bitácora — Plataformero

Una línea por iteración: `#N — qué se hizo — cómo se verificó`

---

#0 — Bootstrap: carpeta, SPEC.md, TODO.md, settings.json de permisos — verificado con `ls`
#1 — Andamiaje: index.html, style.css, core.js (constantes y física), input.js — `node --check` OK
#2 — audio.js (WebAudio sintetizado) y save.js (localStorage con fallback) — `node --check` OK
#3 — tiles.js (catálogo + dibujo) y physics.js (AABB por eje, one-way, peligros) — `node --check` OK
#4 — Ajuste de salto a 330/800 (sube 4,25 tiles, cubre ~7 corriendo) para poder diseñar niveles con números redondos — recalculado a mano
#5 — levels.js: los 10 niveles con DSL de coordenadas en vez de strings de 150 chars — `node tools/validar.js` 10/10
#6 — validator.js: BFS sobre grafo de apoyos con las reglas de salto reales; tools/validar.js para correrlo sin navegador — 10/10 válidos
#7 — entities.js: 3 enemigos, monedas, hongo, estrella, vida, 3 tipos de plataforma, meta — `node --check` OK
#8 — player.js: aceleración, sprint, salto variable, coyote time, jump buffer, chico/grande, daño, muerte — `node --check` OK
#9 — camera.js (lookahead) y world.js (mapa mutable, colisiones, partículas, fondos por tema) — `node --check` OK
#10 — hud.js y screens.js: menú, selección de nivel, pausa, muerte, nivel completado, game over, final — `node --check` OK
#11 — engine.js (loop de paso fijo 1/120 con acumulador, máquina de estados, ganchos de debug) y main.js — `node --check` OK en los 17 archivos
#12 — Servidor local + primera carga en el navegador — 0 errores de consola, estado=menu, 10/10 niveles válidos
#13 — Primera tanda de tests por consola: movimiento, salto variable, monedas, muerte — 8/10; falla el pisotón
#14 — El pisotón fallaba por el test, no por el juego: avanzaba 1/120 s y los cuerpos nunca llegaban a solaparse. Recalibrado a 0,08 s — PASA
#15 — Faltaban estrellas en los niveles (el criterio 8 las pedía): agregadas en 6, 9 y 10 — revalidado 10/10
#16 — Tests de peligros, vidas y game over — 11/11 PASA
#17 — Tests de bloques, power-ups y plataformas móviles — 16/16 PASA
#18 — Tests de pausa, meta, progreso y recorrido de los 10 niveles encadenados — 14/14 PASA
#19 — Tests de rendimiento: 0,30 ms/frame en el nivel 10, sin acumulación de entidades ni partículas — PASA
#20 — Batería movida de la consola a tests.html + tools/tests.js, reproducible — 54/55
#21 — La falla 55 era del test: usaba localStorage.removeItem, que limpia el disco pero no el estado ya cargado en G.save. Cambiado a G.save.borrar() — 55/55
#22 — Verificado que no hay módulos ES6, fetch ni assets externos: el juego anda con doble click en file:// — grep sin resultados
#23 — Verificado el render leyendo píxeles del canvas (menú, selección, nivel 1, nivel 6, final) — las 5 pantallas dibujan contenido
#24 — Cierre: README.md con instrucciones y guía para editar niveles, INFORME.md — 13/13 criterios de aceptación

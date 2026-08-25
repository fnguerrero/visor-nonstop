# Visor /nonstop

Mira de un vistazo cómo va un trabajo largo de `/nonstop`, sin abrir tres archivos a mano.

## Uso

Doble click en **`index.html`**, y arrastrá adentro los `.md` de la carpeta `.nonstop/`
del proyecto que quieras mirar (SPEC, TODO, BITACORA). También podés hacer click para
elegirlos.

Muestra:

- **Porcentaje y barra de progreso**, con los bloqueados y los en curso en su propio color.
- **Contadores** por estado: hechos, en curso, pendientes, bloqueados.
- **Ítems agrupados por sección**, con el `verif:` de cada uno en gris.
- **Iteraciones usadas sobre el presupuesto**, sacadas de la bitácora y la spec.
- **Las últimas 8 entradas del log.**

No hace falta cargar los tres: con el TODO solo ya muestra el progreso, y avisa qué falta.
Un archivo que no sea de `.nonstop/` se ignora con un aviso, sin romper nada.

## Tests

```
http://localhost:PUERTO/index.html?test=1
```

Corre 31 tests sobre los `.md` reales que están en `muestras/` (una copia de los del
proyecto Plataformero). **La batería necesita servidor**: usa `fetch`, y con `file://`
el navegador lo bloquea. El visor en sí no usa `fetch`, así que funciona con doble click.

## Formato que entiende

El que genera la skill `/nonstop`:

- **TODO**: `- [x] texto · verif: cómo se verificó`, agrupado por `## Sección`.
  Estados: `[ ]` pendiente, `[~]` en curso, `[x]` hecho, `[!]` bloqueado.
- **SPEC**: el `# Título`, la sección `## Objetivo` y un `**N**` de presupuesto.
- **BITACORA**: líneas `#N — texto`.

Si los archivos vienen renombrados, los detecta igual por su contenido.

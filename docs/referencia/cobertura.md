# Cobertura del README inicial

La reorganización conserva el contenido completo en la
[referencia inicial](README-inicial.md). Solo se ajustan sus rutas de imagen;
la [comprobación de procedencia](procedencia.json) identifica esa adaptación.
La presentación principal se redacta como documentación del proyecto.

La [matriz de requisitos e iteraciones](../../bombardment-player/doc/cobertura-enunciado.md)
completa este mapa con 32 puntos de revisión del enunciado y las comprobaciones
previstas para cada uno.

| Apartado inicial | Ubicación en la documentación actual |
| --- | --- |
| Introducción, objetivo y pareja | README principal: presentación, contrato y equipo. |
| Reglas, autoría y descripción original del juego | README principal: el juego. |
| Estructura y módulo independiente | README principal: organización; guía técnica: compilación. |
| Puesta en marcha, JDK, Maven y NetBeans | README principal y guía técnica: comandos de trabajo. |
| Scripts, configuración, `BUILD`, interfaz y aislamiento | README principal: ejecución; guía técnica: interfaz y lanzadores. |
| Clase, paquete, `player.class`, auxiliares y nombre visible | README principal: contrato; normativa: PF05–PF08. |
| `IPlayer`, `timeout()` y gracia por arranque frío | README principal: contrato; normativa: contrato de tiempo. |
| Hilos, memoria, archivos, red y salida de depuración | README principal: contrato; normativa: PF09–PF13. |
| `GameStatus`: todas las firmas y semántica | Guía técnica: API de `GameStatus`. |
| Ejemplo de matriz, explosión, coordenadas y FEN | Guía técnica: ejemplo de coordenadas; referencia íntegra conserva también el dibujo textual. |
| Herencia, `setCell` y `forceLoser` | README principal y guía técnica: modelo y API. |
| Challenges, argumentos y especificaciones de jugadores | README principal: challenges; guía técnica: ejecución y jugadores. |
| HTML, CSV, Elo, profundidad, tiempos e incidencias | README principal y guía técnica: experimentación. |
| Aperturas y coste orientativo | README principal y guía técnica: aperturas. |
| Validación B, sobreajuste e incertidumbre | README principal y normativa: desarrollo y validación. |
| Fórmula de puntuación e interpolación, con ejemplo | README principal y normativa: evaluación. |
| Tablas de nivel 1 y nivel 2 | README principal y normativa: evaluación. |
| Memoria, imágenes y reparto de los tres puntos | README principal y normativa; estructura en `memoria.md`. |
| Torneo y bonus | README principal y normativa: evaluación. |
| Registro por fechas, tags, repositorio privado y evidencias | README principal y `doc/registre.md`; normativa: PF14–PF16. |
| Uso de IA, declaración y ejercicios de validación | README principal y normativa; declaración iniciada en `memoria.md`. |
| Entrega, estructura del ZIP, ID e inscripción | README principal y normativa: entrega y equipo. |
| Comandos de ZIP en Linux/macOS y Windows, limpieza y extracción | README principal y guía técnica: empaquetado. |

## Aclaraciones verificadas

La referencia inicial contiene una afirmación de disjunción entre conjuntos
rápidos que contradice `exemple.properties`. La
[comparación de los FEN actuales](../../bombardment-player/doc/evidencias/aperturas.json)
confirma que los conjuntos rápidos están anidados. Se conserva el texto de
partida en el archivo de referencia y se usa el resultado comprobado en la
documentación de trabajo.

Los ejemplos de constructores con parámetros representan posibilidades del
cargador. El jugador actual solo implementa constructor vacío y con nombre
`String`; la guía lo señala para evitar comandos de variantes inexistentes.

Los lanzadores `.sh` requieren Bash. Sus invocaciones se conservan como
`bash scripts/ui.sh` y `bash scripts/challenge.sh` en el README y la guía.
La configuración de benchmark fija 200 ms; el banco utiliza 1000 ms si se
omite `timeMs`, por lo que ese parámetro debe mantenerse explícito.

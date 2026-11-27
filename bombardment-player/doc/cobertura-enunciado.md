# Cobertura del enunciado

Revisión documental del 2026-11-27 sobre el contenido completo de
`7bb12c2:README.md`, conservado en la [referencia inicial](../../docs/referencia/README-inicial.md).
Las cabeceras y opciones de los scripts, `Challenge`, `EngineOptions` y las
configuraciones de benchmark se han contrastado mediante lectura de sus archivos.

**Resultado:** los requisitos están recogidos en el plan y la normativa.
Las tareas de implementación, los experimentos y los trámites que siguen
pendientes no se consideran realizados por aparecer en esta tabla.
Esta revisión no ha ejecutado nuevas compilaciones ni challenges.

## Relación de requisitos e iteraciones

Las fuentes de la segunda columna corresponden a los apartados de la
referencia inicial. Las comprobaciones se realizarán al cerrar las iteraciones,
salvo las revisiones documentales ya recogidas en el diario.

| ID | Apartado de origen | Contenido que debe conservarse | Iteraciones | Comprobación prevista |
| --- | --- | --- | --- | --- |
| CE01 | Introducció | Minimax, poda alfa-beta y profundización iterativa limitada por tiempo. | I02–I04 | Referencia correcta, equivalencia con poda e interrupción segura. |
| CE02 | Introducció | Heurística propia y optimizaciones ajustadas al juego. | I05–I09 | Hipótesis, componentes, pesos y comparación controlada. |
| CE03 | Introducció | Transposiciones, Zobrist y variantes de búsqueda como posibilidades, no obligaciones. | I06–I08 | Decisión documentada de incorporar o descartar cada candidata. |
| CE04 | Introducció / Lliurament | Trabajo en pareja, inscripción, NIF en el registro e ID para el nombre del ZIP. | I00, I11 | Datos confirmados en el registro del proyecto final. |
| CE05 | Registre d'experiments | GitHub privado con la cuenta de revisión como colaboradora. | I00, I11 | Visibilidad y acceso comprobados. |
| CE06 | El vostre jugador | Clase `MyPlayer`, paquete y `player.class` conservados; auxiliares y nombre visible personalizables. | I01, I11 | Revisar punto de entrada y cargar el JAR. |
| CE07 | Estructura / Posada en marxa | Módulo independiente, API instalada, JDK 17 o posterior, Maven y uso desde NetBeans. | I00–I01, I11 | Entorno compatible y compilación fuera del agregador. |
| CE08 | Contracte de temps | `timeout()` desde otro hilo; devolución inmediata de última iteración completa; gracia de 100 ms y 1 s en las tres primeras jugadas del proceso. | I04, I09 | Reserva legal, interrupciones y pruebas en frío/caliente. |
| CE09 | Normes | Búsqueda monohilo, `-XX:ActiveProcessorCount=1` y `-Xmx1g`. | I04, I07, I09, I11 | Revisar concurrencia y memoria con opciones reales de JVM. |
| CE10 | Normes | Sin archivos, red, `System.exit` ni cálculo durante el turno rival; salida moderada a logs. | I04, I09, I11 | Revisión del jugador y sus auxiliares. |
| CE11 | Contracte de temps / Challenges | Respuesta tardía, `null`, ilegalidad, excepción o muerte del proceso causan derrota. | I01, I04, I09 | Legalidad y cero incidencias en las pruebas realizadas. |
| CE12 | El joc / GameStatus | Reglas, dos colores, coordenadas, constructores, consultas, jugadas, FEN, copias y condiciones terminales. | I01–I02 | Casos calculables, ambos colores y estado de entrada conservado. |
| CE13 | GameStatus / Herència | `setCell()` con llamada a `super`, inicialización de hash fuera de constructores; `forceLoser()` reservado al motor. | I01, I07, I11 | Revisión y equivalencia del hash, si se utiliza herencia. |
| CE14 | Posada en marxa / Challenges | Comandos, configuración de los lanzadores, `BUILD`, `CONFIG`, controles de UI y aislamiento. | I00–I01 | README y guía contrastados con los scripts. |
| CE15 | Banc de proves | Challenges `.properties`, `playerA`/`playerB`, argumentos de constructor, etiquetas, JAR y dos colores por apertura. | I04–I09 | Configuración efectiva y versiones reales comparadas. |
| CE16 | Banc de proves | HTML/CSV, puntuación, error, Elo, profundidad, logs, tiempos máximos e incidencias. | I04–I10 | Revisar informes, cifras y posibles derrotas técnicas. |
| CE17 | Banc de proves | Conjuntos rápidos de 20/50/100 partidas y benchmarks de 200; coste orientativo e independencia de aperturas. | I05–I09 | Usar los FEN reales y no contar solapamientos como muestras nuevas. |
| CE18 | Validació contra el sobreajustament | A para benchmark, B reservado para validación, sin ajustar con B; incertidumbre y comparación con más de un conjunto. | I05, I09–I10 | Puntuación ± error y discusión de la validación. |
| CE19 | Avaluació | Puntuación `(V + E/2)/N`, derrotas por incidencias e interpolación lineal por tramos. | I09–I10 | Recalcular a partir del CSV y cotejar el informe. |
| CE20 | Resultats contra profe1 | 5 puntos; 200 partidas a 200 ms; máximo desde 75 % y posibilidad de cambiar aperturas. | I05, I09–I10 | Benchmark completo y validación fuera del ajuste. |
| CE21 | Resultats contra profe2 | 2 puntos; 200 partidas a 200 ms; máximo desde 70 %; rival y aperturas no distribuidos. | I09–I10 | Dejar constancia de la limitación; incorporar solo resultados publicados. |
| CE22 | Documentació | 1,25 puntos por mejoras, con challenges entre versiones con/sin cada optimización. | I03–I10 | Comparativas controladas y explicación detallada. |
| CE23 | Documentació | 1,25 puntos por heurística, ajuste de parámetros y aportación de cada componente. | I05, I09–I10 | Comparativas de componentes y discusión del equipo. |
| CE24 | Documentació | 0,5 puntos por resumen de resultados. | I09–I10 | Resumen coherente con las evidencias. |
| CE25 | Documentació | Documentación de entrega en `doc/`; `memoria.md` en Markdown y tablas/gráficas como imágenes de `doc/img/` con rutas relativas. | I00, I10–I11 | Contenido, recursos y enlaces del paquete. |
| CE26 | Registre d'experiments | Diario por fechas reales con evolución, pruebas y resultados; su ausencia o incoherencia puede invalidar la entrega. | Todas | Entrada por trabajo real, sin resultados estimados. |
| CE27 | Registre d'experiments | Cada etapa corresponde a un tag de GitHub cuyo checkout contiene el código probado. | Todas, I11 | Commit/tag reales y recuperación de la versión. |
| CE28 | Registre d'experiments | HTML y CSV de cada challenge citado en `experiments/`, incluidos en el commit del tag; cifras derivadas de esos datos. | I04–I11 | Archivos presentes y correspondencia con diario y memoria. |
| CE29 | Ús de la IA | Tres categorías de uso, límites al encargo de código/análisis y declaración final con herramientas, usos y peticiones, incluso si no hubo IA. | Todas, I10 | Uso real declarado y revisión del equipo. |
| CE30 | Ús de la IA / Validació | Comprensión profunda y capacidad de ampliar el código en la prueba final. | Todas, I10 | Ambos integrantes explican y modifican el jugador. |
| CE31 | Torneig | Torneo tras la entrega; bonus de +1, +0,5 y +0,25 para primero, segundo y tercero/cuarto. | I09–I11 | Jugador compatible; bonus separado de la nota sobre diez. |
| CE32 | Lliurament | Un integrante entrega un ZIP con raíz `bombardment-player/`, fuentes, POM, documentación y experimentos, sin `target/`; extraer fuera y ejecutar `mvn package`. | I11 | Inspección del archivo, reproducción y confirmación del envío. |

La [normativa](normativa-y-restricciones.md) conserva las tablas completas de
puntuación y sus límites; el [plan](iteraciones.md) desarrolla las tareas de
cada iteración. La cobertura documental no equivale a certificar la nota.

## Comandos y documentación técnica conservados

El README principal mantiene los comandos operativos; la guía amplía las
firmas de API y las invocaciones directas del banco. La referencia inicial
conserva también los ejemplos completos.

| Elemento del README inicial | Conservación y aclaración actual |
| --- | --- |
| `mvn install` | Comando inicial del README; `mvn clean install` para reconstruir desde cero. |
| `scripts/ui.sh` / `scripts\ui.bat` | README: `bash scripts/ui.sh` y `.\scripts\ui.bat`. Bash respeta el intérprete declarado. |
| `scripts/challenge.sh` / `scripts\challenge.bat` | README: `bash scripts/challenge.sh` y `.\scripts\challenge.bat`. |
| `BUILD=0`, variable `CONFIG` y configuración sin argumentos de los scripts | README y guía técnica, con el `.properties` inicial y `playerA`/`playerB`. |
| `mvn package` para un jugador JAR | README: tabla de jugadores y reproducción de entrega; guía: módulo independiente. |
| `cd bombardment-player && mvn clean && cd ..` | Mismo comando en el README, para preparar el empaquetado. |
| `zip -r G_E76.zip bombardment-player -x "*/.git/*" "*/target/*"` | Misma invocación en el README; ID ilustrativo que se sustituye por el real. |
| `tar -a -c -f G_E76.zip --exclude=.git --exclude=target bombardment-player` | Misma invocación en el README, identificada para `cmd` de Windows. |
| `git checkout` del tag probado | README: relación tag/checkout; diario y guía: protocolo para recuperar la versión. |
| Firmas de `IPlayer`, constructores, consultas y jugadas de `GameStatus` | README: contrato y resumen; guía: inventario completo y semántica. |
| Tablero de ejemplo, `getPos`, `explosionBalance`, dibujo y FEN | Guía: ejemplo y FEN; referencia inicial: ejemplo completo, incluido el dibujo textual. |
| Jugadores, argumentos y etiquetas de variantes | README y guía, diferenciando firmas de ejemplo de los constructores existentes. |

## Aclaraciones resultantes de la revisión

- Los scripts `.sh` declaran Bash y usan `set -euo pipefail`; se documentan
  con `bash`, evitando asumir que el comando `sh` selecciona ese intérprete.
- Los benchmarks fijan `timeMs=200`. Si se omite la clave en una copia,
  `Challenge` usa 1000 ms por defecto; la configuración efectiva debe comprobarse.
- Los conjuntos rápidos están anidados. La
  [comprobación de aperturas](evidencias/aperturas.json) prevalece sobre la
  afirmación de disjunción del texto inicial, que se conserva como referencia.
- `volatile boolean` es el patrón recomendado de señalización. El requisito
  es cumplir el contrato de interrupción; la memoria justificará la solución usada.
- Las 13 pruebas de infraestructura registradas corresponden a la revisión
  inicial. Esta auditoría es documental y no añade resultados de juego.
- Los materiales de Multi-Snake y htop se mantienen separados. Sus reglas
  no añaden límites, algoritmos ni formatos de ZIP al proyecto final.

El [mapa de conservación](../../docs/referencia/cobertura.md) identifica dónde
se encuentra cada apartado original. El informe de esta auditoría está en
[las evidencias](evidencias/auditoria-enunciado.json).

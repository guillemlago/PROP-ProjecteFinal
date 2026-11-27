# Normativa y restricciones

Este documento centraliza las condiciones encontradas al revisar el proyecto
y los materiales de consulta. Cada apartado indica su ámbito y su fuente.
Las condiciones de otras actividades no cambian las de Bombardment.

## Fuentes y alcance

| Referencia | Contenido | Alcance |
| --- | --- | --- |
| [Referencia inicial completa](../../docs/referencia/README-inicial.md) | Requisitos, evaluación, registro, IA y entrega; copia íntegra de `7bb12c2:README.md`. | Proyecto final Bombardment. |
| [Contrato `IPlayer`](../../bombardment-api/src/main/java/edu/upc/epsevg/prop/bombardment/IPlayer.java) y [`PlayerMove`](../../bombardment-api/src/main/java/edu/upc/epsevg/prop/bombardment/PlayerMove.java) | Interfaz y significado de las métricas. | Integración del jugador. |
| [Opciones del motor](../../bombardment-api/src/main/java/edu/upc/epsevg/prop/bombardment/engine/EngineOptions.java) y [ejecución aislada](../../bombardment-api/src/main/java/edu/upc/epsevg/prop/bombardment/engine/IsolatedPlayer.java) | Tiempo, memoria y proceso. | Ejecución de partidas. |
| [Benchmark principal](../../challenges/benchmark-1-profe1.properties) y [validación](../../challenges/benchmark-validacio-1-profe1.properties) | Parámetros y aperturas. | Evaluación y validación local. |
| [Actividad 1](../../docs/asignatura/actividad-1-multi-snake.md) | Reglas y entrega de Multi-Snake, páginas 3–9. | Actividad anterior. |
| [HKT2](../../docs/asignatura/hkt2-instalacion-aplicaciones.md) | Instalación y modificación de htop. | Documento externo a Bombardment. |

Las referencias externas al módulo se consultan desde el repositorio completo.
Las condiciones necesarias para preparar la entrega se reproducen aquí.
La [matriz de cobertura](cobertura-enunciado.md) asigna cada apartado del
enunciado a las iteraciones y a sus comprobaciones.

## Proyecto final: condiciones obligatorias

| ID | Condición | Comprobación prevista |
| --- | --- | --- |
| PF01 | Trabajo en pareja e inscripción en el registro de equipos, con los NIF requeridos en ese registro. | I00 e I11: datos e ID del proyecto final confirmados. |
| PF02 | Repositorio GitHub privado y acceso como colaborador para la cuenta que revisa el proyecto. | I00 e I11: visibilidad, acceso y tags comprobados. |
| PF03 | Búsqueda minimax con poda alfa-beta y profundización iterativa limitada por tiempo. | I02–I04: corrección y partidas aisladas. |
| PF04 | Heurística propia, documentada y justificada experimentalmente. | I05, I09 e I10: componentes, pesos y comparativas. |
| PF05 | Mantener `MyPlayer`, el paquete `edu.upc.epsevg.prop.bombardment.player` y `player.class`. | I11: compilación y carga por el motor. |
| PF06 | Se permiten clases auxiliares y cambiar el nombre visible devuelto por `getName()`. | Revisar que se conserva el punto de entrada. |
| PF07 | El módulo `bombardment-player` debe compilar de forma independiente; depende de la API instalada. | I11: extraer el ZIP fuera del proyecto y ejecutar `mvn package`. |
| PF08 | JDK 17 o posterior y Maven; el proyecto utiliza nivel de compilación Java 17. | I01 e I11: `java -version` y `mvn -version`. |
| PF09 | Una sola hebra de búsqueda; proceso con `-XX:ActiveProcessorCount=1`. | I04–I09: revisión y ejecución aislada. |
| PF10 | Memoria del proceso del jugador limitada mediante `-Xmx1g`. | I07–I09: tabla acotada y ausencia de errores de memoria. |
| PF11 | El jugador no accede a ficheros ni red, no llama a `System.exit` y no calcula durante el turno rival. | Revisión del jugador y sus auxiliares. |
| PF12 | Evitar exceso de salida por consola: se redirige a logs y consume tiempo. | I04–I09: comparar sin depuración intensiva. |
| PF13 | `move()` devuelve una jugada legal y no nula; excepciones o muerte del proceso suponen derrota. | Pruebas y cero incidencias en challenges. |
| PF14 | Mantener `doc/registre.md` con fechas reales, evolución, pruebas y resultados. | Actualizar cada sesión y cerrar etapas con su tag. |
| PF15 | Cada etapa del registro debe corresponder a un tag de GitHub con el código probado. | Verificar checkout, commit y evidencias de cada etapa cerrada. |
| PF16 | Conservar HTML y CSV de cada challenge citado en `bombardment-player/experiments/`, en la versión del tag. | Comprobar archivos y correspondencia de cifras. |
| PF17 | Toda la documentación de entrega en `doc/`; memoria Markdown en `doc/memoria.md`, tablas y gráficas como imágenes de `doc/img/`, con enlaces relativos. | I10: lectura completa y revisión de enlaces. |
| PF18 | Declaración final de uso de IA, también si no se utilizó. | I10: completar con herramientas y usos reales. |
| PF19 | Entregar un único `[ID_EQUIP].zip`, con raíz `bombardment-player/`, sin `target/`. | I11: inspeccionar contenido y reproducir compilación. |
| PF20 | Solo un integrante realiza la entrega. | I11: responsable y envío confirmados. |

La ausencia de un registro histórico coherente puede invalidar la entrega.
Incumplir las restricciones del jugador puede provocar la terminación de su
proceso o que la entrega se considere no válida.
Las fechas de PF14 son fechas de actividad real; no fijan un calendario de trabajo.

## Contrato de tiempo

- Presupuesto de evaluación: **200 ms por movimiento**.
- Al agotarse, el motor llama a `timeout()` desde otro hilo. `move()` debe
  devolver inmediatamente la jugada de la última profundidad completada.
- El margen ordinario de gracia es **100 ms**. Las **tres primeras llamadas
  a movimiento de cada proceso** tienen **1 s** de gracia por el arranque frío.
- Superar el margen causa la terminación del proceso y la derrota.
- La señal recomendada es un `volatile boolean`, consultado en cada nodo.
- Una iteración parcial no sustituye la última solución completa. Si ninguna
  terminó, debe existir una jugada legal de reserva.
- `PlayerMove.maxDepthReached` expresa la profundidad de la última iteración
  completada; los nodos deben seguir una convención coherente.

La gracia permite devolver el resultado; no amplía el presupuesto de búsqueda.
No basta con que funcione en la interfaz sin aislamiento: los challenges y el
torneo ejecutan a cada jugador en su propia JVM.

## Reglas del modelo que condicionan la implementación

- Tablero cuadrado; configuración principal de 8 × 8 y dos filas iniciales.
- `x` es columna, `y` fila; `board[y][x]`. La fila cero es la de las blancas.
- `PLAYER1 = 1`, `PLAYER2 = -1`, casilla vacía `0`; comienzan las blancas.
- Un paso avanza una fila a una casilla vacía, recto o en diagonal; no captura.
- Una explosión elimina la piedra y los ocho vecinos, de cualquier color.
- Se gana al llegar a la meta o eliminar todas las piedras rivales conservando
  alguna propia. Si la explosión vacía todo el tablero, son tablas.
- Las partidas terminan: las jugadas avanzan o eliminan piedras, sin ciclos.
  Pueden existir transposiciones entre órdenes de movimientos distintos.
- `getMoves()` genera primero pasos y después explosiones; no es una ordenación
  diseñada para mejorar alfa-beta.
- `movePiece()` valida la legalidad y cambia el turno; trabajar sobre copias
  para conservar el estado de entrada.
- Al sobreescribir `setCell()` para mantener un hash, llamar a `super.setCell()`;
  los constructores no pasan por este método y necesitan inicialización propia.
- `forceLoser()` está reservado al motor y no se llama desde el jugador.

## Benchmarks y puntuación

Los dos `.properties` de referencia fijan tamaño, tiempo, gracia y paralelismo.
El banco y el motor completan los demás valores por defecto. La configuración
efectiva a verificar es:

| Parámetro | Valor | Procedencia |
| --- | --- | --- |
| `size` | `8` | Ambos archivos de benchmark. |
| `rows` | `2` | Valor por defecto de `Challenge`. |
| `timeMs` | `200` | Ambos archivos de benchmark. |
| `graceMs` | `100` | Ambos archivos; la gracia fría se aplica en el motor. |
| `isolated` | `true` | Valor por defecto de `Challenge`. |
| `jvmArgs` | `-Xmx1g -XX:ActiveProcessorCount=1` | Valor por defecto de `EngineOptions`. |
| `parallel` | `1` | Ambos archivos de benchmark. |

Fuente adicional: [`Challenge`](../../bombardment-bench/src/main/java/edu/upc/epsevg/prop/bombardment/bench/Challenge.java).
No omitir `timeMs=200` en las copias: el valor por defecto del banco sin esa
clave es **1000 ms**, que no corresponde al presupuesto de evaluación.

La puntuación porcentual es `100 × (victorias + tablas / 2) / partidas`.
Una derrota por tiempo, jugada ilegal, excepción o proceso terminado cuenta
como derrota. Los puntos de cada tramo se interpolan linealmente:

`puntos = a + (P - P0) × (b - a) / (P1 - P0)`.

### Referencia de nivel 1 · 5 puntos

200 partidas, 100 aperturas jugadas con los dos colores y 200 ms por jugada.
El alias técnico del rival es `profe1`.

| Puntuación | Puntos |
| --- | --- |
| Jugador no funcional | 0 |
| 0 % a 10 % | 0 a 1 |
| 10 % a 30 % | 1 a 2,5 |
| 30 % a 75 % | 2,5 a 5 |
| Al menos 75 % | 5 |

Ejemplo conservado: 80 victorias, 10 tablas y 110 derrotas en 200 partidas
dan 42,5 %, equivalentes a unos 3,19 puntos de este bloque.

Las aperturas de evaluación pueden sustituirse por otras del mismo tamaño.
La versión final debe generalizar más allá del conjunto `benchmark-A`.

### Referencia de nivel 2 · 2 puntos

200 partidas a 200 ms con un rival de mayor nivel y un conjunto de aperturas
no distribuido. Su identificador es `profe2`. El rival tampoco se distribuye;
sus resultados se publican junto con el torneo.

| Puntuación | Puntos |
| --- | --- |
| Menos de 5 % | 0 |
| 5 % a 30 % | 0 a 1,5 |
| 30 % a 70 % | 1,5 a 2 |
| Al menos 70 % | 2 |

No se pueden certificar localmente estos dos puntos.

### Documentación · 3 puntos

| Contenido | Puntos | Evidencia necesaria |
| --- | --- | --- |
| Mejoras y optimizaciones | 1,25 | Explicación y challenges entre variantes con/sin cada mejora. |
| Heurística | 1,25 | Diseño, ajuste de parámetros y valor de cada componente. |
| Resumen de resultados | 0,5 | Cifras coherentes con los experimentos archivados. |

La declaración de IA y el registro histórico son obligatorios además de los
contenidos puntuables. La prueba final puede incluir teoría y ampliaciones
del código; se necesita comprender y poder modificar el jugador entregado.

### Torneo · bonus adicional

Ganador: +1; finalista: +0,5; tercer y cuarto puesto: +0,25.
Este bonus está fuera de los diez puntos anteriores y se disputa tras la entrega.

## Desarrollo, validación y sobreajuste

- `prova-10`, `prova-25` y `prova-50` se usan en desarrollo: 20, 50 y 100 partidas.
- `benchmark-A` contiene 100 aperturas; sus dos colores dan 200 partidas.
- `benchmark-B` contiene otras 100 aperturas y se reserva para validar.
- B no cuenta para la puntuación local del benchmark principal. No ajustar
  los pesos mirándolo: al usarlo para ajustar deja de ser validación independiente.
- En torno al 50 % de puntuación y con 200 partidas, el error estándar puede
  rondar 3,5 puntos porcentuales. Diferencias de 2 o 3 puntos no bastan para
  atribuir una mejora; informar del error calculado por el banco.
- Una caída en B superior a dos errores estándar es una señal de posible
  sobreajuste que debe investigarse, no una demostración automática.
- El paralelismo de partidas del banco no equivale a permitir varios hilos
  de búsqueda. Se recomienda `parallel=1` para comparar; no superar la mitad
  de los núcleos físicos al paralelizar partidas.

**Discrepancia comprobada:** la referencia inicial describe los conjuntos
rápidos como disjuntos, mientras que un comentario de `exemple.properties`
afirma que comparten aperturas. Los FEN actuales confirman el solapamiento:
`prova-10` está contenido en `prova-25`, y este en `prova-50`. A y B son disjuntos
entre sí y respecto a los rápidos. Véase la [comprobación archivada](evidencias/aperturas.json).
No contar las mismas aperturas como observaciones independientes nuevas.

## Uso de IA

| Categoría | Usos |
| --- | --- |
| Apoyo libre | Dudas de Java y algoritmos, ayuda de depuración, automatización de pruebas, gráficas y tablas de CSV, revisión de redacción. |
| Permitido con declaración | Autocompletado, sugerencias de fragmentos pequeños y refactorizaciones. |
| Fuera del alcance permitido | Encargar el jugador completo, toda la búsqueda o toda la heurística; encargar el análisis y las conclusiones de la memoria. |

El equipo escribe su código y su análisis. La declaración final identifica
herramientas, usos y ejemplos de peticiones; el uso que requiere declaración
sin declararlo constituye una falta. El trabajo actual se limita a preparar
documentación y planificación. La memoria ya registra ese uso de apoyo.

## Formato y comprobación de la entrega

```text
[ID_EQUIP].zip
└── bombardment-player/
    ├── pom.xml
    ├── src/
    ├── doc/
    │   ├── memoria.md
    │   ├── registre.md
    │   └── img/            Imágenes utilizadas, cuando se generen
    └── experiments/        HTML y CSV de los challenges citados
```

La carpeta del módulo debe aparecer al abrir el ZIP. No se entregan los
otros módulos ni `target/`. El nombre del ZIP usa el ID asignado al equipo
en el registro del proyecto final. Solo un integrante lo envía. Antes de
entregar, extraerlo en una carpeta nueva fuera del proyecto y compilarlo con
`mvn package`, con la API instalada previamente.

## Condiciones de actividades anteriores: Multi-Snake

Estas condiciones se conservan como referencia histórica y **no se aplican
al jugador de Bombardment**. Fuente: [Actividad 1](../../docs/asignatura/actividad-1-multi-snake.md).

| Ámbito | Condición encontrada | Página |
| --- | --- | --- |
| PDDL | `domain.pddl` y `problem.pddl` para A; probar con LAMA-first e incluir plan y longitud. | 3 |
| Módulos | No modificar `ac1-model`; trabajar en `ac1-cerca`. Los cambios de `ac1-app` son locales y no se entregan. | 4 |
| Ejecución | Misma máquina y condiciones, `-Xmx2g`, máximo 120 s por búsqueda. | 4 |
| Estado | `equals()` y `hashCode()` incluyen posiciones y rastro; completar `distancesFrom()`. | 4 |
| Algoritmos | BFS, DFS, IDS y A*, con las dos heurísticas descritas en el documento. | 4–5 |
| DFS | Profundidad máxima 50: no expandir nodos por encima de 50. | 5 |
| Ciclos | `usarLNT=false`: revisar ancestros; `true`: LNT con estado completo. | 5 |
| Métricas | Solución, nodos explorados y cortados, picos LNO/LNT/suma, tiempo; acumular nodos de IDS entre iteraciones. | 5 y 7 |
| Heurísticas | Manhattan y distancias BFS con muros, rastros y agentes; descartar salidas inaccesibles. | 5 |
| Estudio | Markdown con las trece preguntas justificadas; reto E/F documentado si se desarrolla. | 6–7 |
| Entrega | ZIP con `pddl/`, `ac1-cerca/` limpio, `documentacio/` y `Readme.md` en primer nivel, sin carpeta raíz común. | 8 |
| Identidad | Registro obligatorio, nombre del ZIP por ID, enlace GitHub, nombres y NIF en el Readme de esa entrega. | 8 |
| Compilación | El proyecto debe compilar; si no compila, calificación cero de esa actividad. | 8 |
| Historial | GitHub con al menos un commit por sesión de trabajo y acceso de revisión. | 9 |
| Asistencia | Laboratorios de Actividad 1 obligatorios; penalización proporcional de hasta el 30 %. | 9 |

La composición de aquel ZIP es distinta de la del proyecto final. No mezclar
sus límites de 2 GB y 120 s con los de 1 GB y 200 ms de Bombardment.

## Material externo: instalación de htop

Fuente: [HKT2](../../docs/asignatura/hkt2-instalacion-aplicaciones.md), páginas 1–2.
No se ha encontrado relación de este ejercicio con Bombardment.

- Compilar e instalar htop desde sus fuentes en Debian y NixOS.
- En Debian, instalar en `/usr/local/games` y permitir su ejecución desde cualquier ubicación.
- Desinstalar y reinstalar cambiando `Load average:` por `Càrrega mitjana:`.
- En NixOS, estudiar estructura de directorios, entorno de compilación,
  dependencias, fuentes, `ldd`, recolección de basura y `overrideAttrs`.
- Entregar especificaciones, reparto de tareas, algoritmo de pasos,
  implementación con comandos/configuraciones/capturas, explicación individual
  y anexo de prompts de IA por integrante.

## Criterios internos acordados para este proyecto

Estas decisiones organizan nuestro trabajo; no se presentan como requisitos
adicionales de evaluación:

- Plan sin calendario; avances medidos por los criterios de cada iteración.
- Durante esta preparación se editan documentación y planificación.
- Código futuro acorde con el nivel trabajado: Java, métodos claros,
  estructuras conocidas y cada optimización explicada y medida.
- Conservar primero una referencia sencilla de corrección antes de optimizar.
- No afirmar resultados, tags ni experimentos inexistentes.
- Ninguna incidencia técnica se compensa con una puntuación de juego alta.
- Mantener las atribuciones de los materiales conservados.
- Cerrar las conclusiones a partir de datos reales y de la revisión de ambos integrantes.

Las tablas de transposiciones, Zobrist, killer moves, historial, extensiones
tácticas y variantes de ventana son posibilidades de optimización; no se
añaden como obligaciones del enunciado. Su estudio y selección pertenecen
al plan de trabajo y deben justificarse por su corrección y sus resultados.

## Cómo incorporar nuevas restricciones

Añadir cada nueva condición con su fuente exacta y apartado o página, su
ámbito, la comprobación prevista y la iteración afectada. Si una recomendación
se adopta como decisión interna, registrarla como tal. Si las fuentes discrepan,
anotar la discrepancia y la comprobación pendiente antes de asumir una regla.

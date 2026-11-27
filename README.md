<div align="center">

<img src="docs/img/coet.png" alt="Bombardment" width="96">

# Bombardment

Jugador automático de estrategia · Proyecto final de PROP

Java 17 · Minimax · Poda alfa-beta · Profundización iterativa

</div>

El proyecto desarrolla un jugador de **Bombardment** capaz de decidir con un
presupuesto de 200 ms por movimiento. El trabajo combina búsqueda adversaria,
una heurística específica del juego y experimentos reproducibles para medir
el efecto de cada mejora.

**Estado actual:** preparación documental completada y compilación inicial
verificada. `MyPlayer` todavía escoge una jugada aleatoria; la búsqueda y la
heurística propia están pendientes. Las técnicas de la cabecera describen el
objetivo del desarrollo.

## Documentación

- [Plan por iteraciones, sin fechas](bombardment-player/doc/iteraciones.md): tareas, dependencias y criterios de cierre.
- [Diario de trabajo y experimentos](bombardment-player/doc/registre.md): actividad real y evidencias de cada etapa.
- [Normativa y restricciones](bombardment-player/doc/normativa-y-restricciones.md): contrato técnico, evaluación y entrega.
- [Guía técnica](bombardment-player/doc/guia-tecnica.md): API, ejecución y método de experimentación.
- [Memoria](bombardment-player/doc/memoria.md): estructura preparada para documentar las mejoras y los resultados.
- [Material de la asignatura en Markdown](docs/asignatura/README.md): nueve documentos con sus páginas visuales.
- [Referencia inicial íntegra](docs/referencia/README-inicial.md): comandos, ejemplos y requisitos conservados para consulta.
- [Cobertura del enunciado](bombardment-player/doc/cobertura-enunciado.md): relación de requisitos, iteraciones y comprobaciones.

## El juego

Cada jugador empieza con dos filas de piedras en un tablero de 8 × 8.
Las blancas comienzan. En cada turno se realiza una de estas acciones:

- **Avanzar:** mover una piedra una fila hacia la meta, recto o en diagonal,
  a una casilla vacía. El desplazamiento no captura.
- **Explotar:** eliminar la piedra seleccionada y todas las piedras de los
  ocho vecinos, de ambos colores.

Se gana al alcanzar la última fila del rival o al ser el único jugador con
piedras. Una explosión que vacía el tablero produce tablas. El juego fue
creado por Chris Huntoon en 2003.

Toda partida termina: cada jugada avanza una piedra o elimina piedras y las
posiciones no se repiten a lo largo de una partida.

La [descripción original del juego](https://jpneto.github.io/world_abstract_games/bombardment.htm)
se conserva como referencia de sus reglas.

![Interfaz de Bombardment](docs/img/ui.png)

## Organización del repositorio

```text
PROP-ProjecteFinal/
├── pom.xml                   Agregador de los módulos Maven
├── bombardment-player/       Jugador y contenido de la entrega
│   ├── src/main/java/        Implementación del jugador
│   ├── doc/                  Plan, diario, normativa y memoria
│   └── experiments/          Evidencias de los experimentos citados
├── bombardment-api/          Modelo, interfaces y motor de partidas
├── bombardment-bench/        Ejecución de challenges e informes
├── bombardment-ui/           Interfaz gráfica
├── challenges/              Configuraciones de las comparaciones
├── openings/                Conjuntos de posiciones iniciales
├── docs/asignatura/          Documentos de consulta en Markdown
├── docs/referencia/          Referencia inicial y mapa de conservación
├── scripts/                 Lanzadores de la interfaz y los challenges
└── lib/repo/                Dependencia del rival de referencia
```

El desarrollo del jugador se concentra en `bombardment-player`. Este módulo
Maven es independiente, no hereda del agregador y su dependencia de ejecución
es `bombardment-api`. El punto de entrada está en
[`MyPlayer.java`](bombardment-player/src/main/java/edu/upc/epsevg/prop/bombardment/player/MyPlayer.java).
Se conservan la clase
`edu.upc.epsevg.prop.bombardment.player.MyPlayer` y la propiedad `player.class`
para mantener la compatibilidad con el motor.

## Compilar y ejecutar

Se necesitan **JDK 17 o superior** y **Maven**. Comprobar que `java -version`
y `mvn -version` usan el JDK adecuado; Java 8 no sirve para este proyecto.
Desde la raíz del repositorio:

```powershell
java -version
mvn -version
mvn install
.\scripts\ui.bat
```

Para reconstruir desde cero, usar `mvn clean install`. Los lanzadores tienen una sección
de configuración para elegir jugadores y tiempo. La interfaz permite jugar
como `human`, observar al jugador y depurar la búsqueda.

Para un challenge rápido en Windows:

```powershell
.\scripts\challenge.bat
```

En Linux o macOS, los lanzadores requieren **Bash**, como indican sus cabeceras:

```sh
bash scripts/ui.sh
bash scripts/challenge.sh
```

Invocarlos con `bash` respeta sus opciones y sintaxis; usar `sh` puede fallar
en sistemas donde corresponde a otro intérprete.

El lanzador utiliza `challenges/exemple.properties`. El benchmark principal
y su validación están en `challenges/benchmark-1-profe1.properties` y
`challenges/benchmark-validacio-1-profe1.properties`. La
[guía técnica](bombardment-player/doc/guia-tecnica.md) explica cómo ejecutarlos
sin modificar las configuraciones de referencia.

También se pueden lanzar directamente los tres conjuntos después de compilar:

```powershell
java -cp 'bombardment-bench\target\classes;bombardment-bench\target\lib\*' edu.upc.epsevg.prop.bombardment.bench.Challenge challenges/exemple.properties
java -cp 'bombardment-bench\target\classes;bombardment-bench\target\lib\*' edu.upc.epsevg.prop.bombardment.bench.Challenge challenges/benchmark-1-profe1.properties
java -cp 'bombardment-bench\target\classes;bombardment-bench\target\lib\*' edu.upc.epsevg.prop.bombardment.bench.Challenge challenges/benchmark-validacio-1-profe1.properties
```

Los scripts tienen `BUILD=1` por defecto y recompilan antes de ejecutar;
`BUILD=0` lo evita. No reciben argumentos: sus opciones se editan en la
sección de configuración. Para ejecutar pruebas usar `mvn test`: la
recompilación de los lanzadores las omite.

La variable `CONFIG` de `scripts/challenge.sh` y `scripts/challenge.bat`
selecciona el `.properties`. Dentro de él, `playerA` y `playerB` seleccionan
los rivales. Cambiar las configuraciones de desarrollo en copias propias.

En NetBeans, abrir la raíz como proyecto Maven y compilar el agregador;
ejecutar `bombardment-ui` para la interfaz o `bench.Challenge` para el banco.
En la UI, un clic selecciona la piedra; otro clic en ella o un clic derecho
la hace explotar. Los destinos y la zona de explosión se muestran al seleccionar
y apuntar. Los desplegables de jugadores son editables. Sin aislamiento se
puede depurar en la misma JVM; con aislamiento se reproduce el modo de los challenges.

## Contrato del jugador

La clase de entrada es `edu.upc.epsevg.prop.bombardment.player.MyPlayer` y
se conserva junto con `player.class`. Se pueden crear auxiliares y cambiar
el nombre visible en `getName()`. El contrato de `IPlayer` es:

```java
PlayerMove move(GameStatus s);
void timeout();
String getName();
```

La búsqueda prevista usa minimax, poda alfa-beta, profundización iterativa
y una heurística propia justificada con experimentos. `timeout()` llega
desde otro hilo: hay que devolver inmediatamente la mejor jugada de la
última profundidad completada. El patrón recomendado utiliza una señal
`volatile` que la búsqueda consulta en cada nodo.
Una jugada legal de reserva cubre el caso en que ninguna iteración termine.

- **Tiempo:** 200 ms por movimiento; gracia de 100 ms tras `timeout()`.
  Las tres primeras llamadas del proceso disponen de 1 s de gracia por arranque frío.
- **Recursos:** una hebra de búsqueda, `-XX:ActiveProcessorCount=1` y `-Xmx1g`.
- **Ejecución:** sin acceso a ficheros o red, sin `System.exit` y sin calcular
  durante el turno rival. La salida de depuración va a logs y debe ser moderada.
- **Incidencias:** respuesta tardía, excepción, `null`, movimiento ilegal o
  muerte del proceso causan derrota; el motor termina los procesos bloqueados.

`PlayerMove` informa de la jugada, los nodos y la profundidad **completada**.
La gracia sirve para terminar, no para extender el presupuesto de búsqueda.

## Modelo y API

`GameStatus` utiliza `x` para columna e `y` para fila, con `board[y][x]` y la
fila 0 abajo, del lado blanco. Las casillas contienen `1` (PLAYER1), `-1`
(PLAYER2) o `0`. `c2-d3` representa un paso y `e5*` una explosión.

La API incluye constructores para tablero inicial, filas configurables,
matriz y turno, copia y lectura FEN. Se consulta mediante `getSize`,
`isInside`, `getPos`, `getCurrentPlayer`, `isGameOver`, `getWinner`, `isDraw`,
`getStoneCount`, `getStones`, `getGoalRow`, `getLastMove` y `getPlies`.
`toFen`, `equals`, `hashCode` y `toString` permiten representar y comparar estados.

`getMoves()` devuelve una lista nueva de movimientos legales, primero pasos
y después explosiones, sin orden pensado para alfa-beta. `isLegal()` comprueba
una jugada; `movePiece()` la aplica y cambia el turno, o lanza una excepción
si es ilegal. `explosionBalance()` calcula rivales eliminados menos propias,
incluida la piedra que explota.

Para mantener un hash por herencia, `setCell()` permite interceptar cambios
llamando a `super.setCell()`; los constructores no lo invocan. `forceLoser()`
está reservado al motor. La [guía técnica](bombardment-player/doc/guia-tecnica.md#api-de-gamestatus)
conserva **todas las firmas, el ejemplo de tablero, FEN y coordenadas**.

## Challenges y validación

Cada apertura se juega dos veces intercambiando colores. Copiar
`challenges/exemple.properties` para crear comparaciones y conservar las
configuraciones de referencia. Las rutas del `.properties` son relativas
a su propia carpeta.

| Especificación | Jugador |
| --- | --- |
| `random` | Aleatorio. |
| `profe1` | Referencia de nivel 1. |
| `edu.upc.epsevg.prop.bombardment.player.MyPlayer` | Clase del jugador. |
| `edu.upc.epsevg.prop.bombardment.player.MyPlayer(4,true)` | Constructor configurable, si se implementa esa firma. |
| `v2=edu.upc.epsevg.prop.bombardment.player.MyPlayer(2)` | Etiqueta para comparar variantes, si existe ese constructor. |
| `jar:ruta/jugador.jar` | Jugador empaquetado con `mvn package`. |

El cargador acepta argumentos `String`, `int`, `long`, `double` y `boolean`.
Actualmente solo existen los constructores vacío y con nombre `String`.
En la interfaz se añade `human` para juego manual.

`profe1` es una referencia de nivel medio con heurística sencilla. Los
argumentos y etiquetas permiten comparar versiones propias; las etiquetas
por sí solas no cambian la implementación del jugador.

| Aperturas | Partidas | Uso |
| --- | --- | --- |
| `prova-10` | 20 | Prueba rápida; unos 3 minutos a 200 ms. |
| `prova-25` | 50 | Desarrollo; unos 8 minutos. |
| `prova-50` | 100 | Comparación ampliada; unos 15 minutos. |
| `benchmark-A` | 200 | Benchmark principal; alrededor de una hora. |
| `benchmark-B` | 200 | Validación reservada con otras aperturas. |

Estos costes son orientativos. Los conjuntos rápidos están anidados:
`prova-10` está contenido en `prova-25`, y este en `prova-50`. A y B son
disjuntos entre sí y respecto a los rápidos; la
[comprobación](bombardment-player/doc/evidencias/aperturas.json) aclara una
discrepancia de la referencia inicial.

Los informes HTML y CSV se generan en `results/`; los logs, en `results/logs/`.
Se informa de puntuación, error estándar, Elo, profundidad e incidencias;
el CSV conserva además FEN y jugadas. Revisar siempre las incidencias y los
máximos de respuesta, especialmente si se acercan a 200 + 100 ms.
`parallel=1` facilita comparaciones fiables; al paralelizar partidas no
superar la mitad de los núcleos físicos.

Reservar B para validar, sin ajustar los pesos con él. Una caída superior a
dos errores estándar respecto a A puede indicar sobreajuste. Con 200 partidas
y una puntuación próxima al 50 %, el error estándar ronda 3,5 puntos; una
mejora aparente de 2 o 3 puntos requiere más evidencia.

## Evaluación

La puntuación es `100 × (victorias + tablas / 2) / partidas`. Las incidencias
cuentan como derrotas. Dentro de cada tramo los puntos se interpolan linealmente:
`a + (P - P0) × (b - a) / (P1 - P0)`.

| Nivel 1 · `profe1` | Puntos sobre 5 |
| --- | --- |
| No funcional | 0 |
| 0–10 % | 0–1 |
| 10–30 % | 1–2,5 |
| 30–75 % | 2,5–5 |
| Al menos 75 % | 5 |

200 partidas con 100 aperturas a dos colores y 200 ms por movimiento.
Las aperturas de evaluación pueden cambiar por otras de la misma dimensión.
Por ejemplo, 80 victorias y 10 tablas entre 200 partidas producen 42,5 %,
equivalentes a unos 3,19 puntos de este bloque.

| Nivel 2 · `profe2` | Puntos sobre 2 |
| --- | --- |
| Menos de 5 % | 0 |
| 5–30 % | 0–1,5 |
| 30–70 % | 1,5–2 |
| Al menos 70 % | 2 |

Otras 200 partidas a 200 ms con rival y aperturas no distribuidos. Los
resultados de este bloque se publican junto al torneo.

La documentación aporta **3 puntos**: 1,25 por mejoras y optimizaciones con
comparativas con/sin cada una; 1,25 por heurística, ajuste y aportación de
componentes; 0,5 por resumen de resultados. La memoria se escribe en
`bombardment-player/doc/memoria.md`; las tablas y gráficas se incorporan como
imágenes de `doc/img/`, con enlaces relativos, por ejemplo
`![Profundidad por versión](img/profundidad.png)`.

El torneo posterior a la entrega añade bonus: ganador +1, finalista +0,5,
tercero y cuarto +0,25. El bonus está fuera de los diez puntos anteriores.

## Forma de trabajo

El [plan](bombardment-player/doc/iteraciones.md) avanza desde minimax a
profundidad fija hasta un jugador con control de tiempo, heurística medida
y optimizaciones justificadas. Cada iteración se cierra al superar sus
pruebas y dejar sus evidencias en el diario. El calendario permanece abierto.

El objetivo es optar a la máxima calificación mediante corrección,
rendimiento y una memoria defendible. Los umbrales de puntuación y las
limitaciones de la validación están recogidos en la normativa.

## Entrega

La entrega contiene únicamente la carpeta `bombardment-player`, con sus
fuentes, `pom.xml`, `doc/` y `experiments/`, sin `target/`. La última iteración
incluye la comprobación del ZIP y la compilación del módulo extraído fuera
del repositorio, con la API instalada previamente.

Ejemplo con el ID ilustrativo `G_E76`, que debe sustituirse por el real.
Desde la raíz, Linux o macOS:

```sh
cd bombardment-player && mvn clean && cd ..
zip -r G_E76.zip bombardment-player -x "*/.git/*" "*/target/*"
```

Desde la raíz, consola `cmd` de Windows:

```bat
cd bombardment-player && mvn clean && cd ..
tar -a -c -f G_E76.zip --exclude=.git --exclude=target bombardment-player
```

Windows 10 y posteriores incluyen `tar`; la extensión `.zip` con `-a` genera
el archivo ZIP. También se puede comprimir desde el Explorador tras limpiar.

```text
[ID_EQUIP].zip
└── bombardment-player/
    ├── pom.xml
    ├── src/
    ├── doc/
    └── experiments/
```

Extraer el ZIP en una carpeta nueva, fuera del agregador, y ejecutar
`mvn package`. Solo un integrante envía la entrega. El nombre del archivo
debe coincidir con el ID asignado al equipo.

## Equipo, diario y trazabilidad

El trabajo es en pareja. La inscripción en el
[registro de equipos](https://docs.google.com/spreadsheets/d/1K2ne3P7kNAUARL9qk55Bv8w2oZKW5sFfFC0SWEL_uvk/edit?usp=sharing)
es obligatoria e incluye los NIF. Confirmar el ID de este proyecto antes de
nombrar la entrega. El repositorio de trabajo en GitHub debe ser privado y
dar acceso como colaborador a la cuenta encargada de revisarlo.

`bombardment-player/doc/registre.md` conserva el historial por fechas reales:
qué se cambia, qué se prueba y con qué resultado. Cada etapa cerrada se asocia
a un tag de GitHub cuyo checkout contenga el código probado. Conservar en
`bombardment-player/experiments/` el HTML y CSV de cada challenge citado e
incluirlos en el commit del tag. Las cifras del diario deben salir de ellos.
Un registro ausente o incoherente puede invalidar la entrega.

Para recuperar una etapa, ejecutar `git checkout NOMBRE_DEL_TAG` sobre una
copia de trabajo con los cambios guardados, sustituyendo el nombre por un
tag real del diario. El código y las evidencias de ese tag deben corresponder
a la versión probada.

Cada entrada incluye rivales, aperturas, partidas, tiempo, puntuación y error,
profundidad e incidencias. La [plantilla del diario](bombardment-player/doc/registre.md)
también distingue las sesiones documentales de las comparativas de juego.

## Uso de IA y defensa

Se admite apoyo para dudas de Java o algoritmos, depuración, automatización
de pruebas, gráficas y tablas a partir de CSV y revisión de redacción.
El autocompletado, los fragmentos pequeños y las refactorizaciones requieren
declaración. El equipo escribe su código y su análisis: no se encarga el
jugador, la búsqueda o la heurística completos, ni el análisis y las conclusiones
de la memoria.

La sección final de la memoria declara herramientas, usos y ejemplos de
peticiones; también es obligatoria si no hubo uso de IA. Omitir un uso que
requiere declaración constituye una falta. La prueba final puede incluir
preguntas teóricas y ampliaciones del código entregado: ambos integrantes
deben entenderlo y ser capaces de modificarlo.

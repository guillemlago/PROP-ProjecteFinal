# Guía técnica

Guía de consulta para desarrollar y comprobar el jugador. Las reglas de
evaluación y entrega están en [normativa y restricciones](normativa-y-restricciones.md).
La [referencia inicial completa](../../docs/referencia/README-inicial.md)
conserva también todos los ejemplos y comandos de partida.

## Entorno y comandos de trabajo

JDK 17 o posterior y Maven. El módulo del jugador compila para Java 17.
Desde la raíz del repositorio, comprobar el entorno y compilar:

```powershell
java -version
mvn -version
mvn clean install
```

`install` instala la API y el resto de módulos en el repositorio Maven local.
Después de instalar la API, el módulo del jugador puede compilarse solo:

```powershell
mvn -f bombardment-player/pom.xml package
```

Para ejecutar las pruebas del proyecto o únicamente las del jugador:

```powershell
mvn test
mvn -f bombardment-player/pom.xml test
```

En NetBeans, abrir la raíz como proyecto Maven y ejecutar **Build** sobre el
agregador. Para la interfaz, ejecutar `bombardment-ui`; los challenges también
se pueden lanzar desde la clase `bench.Challenge`.

En la revisión inicial de este equipo se utilizó Temurin 21.0.12.1 y Maven
3.9.11. El `java` del PATH ordinario apunta a Java 8 y Maven no está en ese
PATH; la comprobación se realizó ajustando el entorno solo para ese proceso.
Seleccionar un JDK compatible en el IDE y en Maven antes del desarrollo.

## Interfaz y lanzadores

Windows, desde la raíz:

```powershell
.\scripts\ui.bat
.\scripts\challenge.bat
```

Linux o macOS:

```sh
bash scripts/ui.sh
bash scripts/challenge.sh
```

Ambos archivos declaran `#!/usr/bin/env bash` y usan `set -euo pipefail`.
Se ejecutan con Bash; `sh` puede seleccionar un intérprete incompatible.

Los cuatro lanzadores originales no reciben argumentos. Su sección
`CONFIGURACIÓ` contiene las variables que se editan para elegir jugadores,
configuración, tamaño y tiempo. Por defecto recompilan con `BUILD=1`;
`BUILD=0` evita la recompilación. Esa compilación usa `-DskipTests`, por lo
que no sustituye la ejecución de pruebas.

En los lanzadores de challenges, `CONFIG` selecciona el archivo `.properties`;
su valor inicial es `challenges/exemple.properties`. Las claves `playerA` y
`playerB` de ese archivo seleccionan los rivales.

Para jugar, seleccionar `human` en un lado y la clase del jugador en el otro.
Los desplegables son editables. Un clic selecciona una piedra y muestra sus
destinos; al mantener el puntero se muestra la zona de explosión. Otro clic
en la piedra seleccionada, o un clic derecho, ejecuta la explosión.

La opción de jugadores aislados desmarcada permite depurar en la misma JVM.
Marcada utiliza un proceso por jugador, como en los challenges y el torneo.

## Ejecutar configuraciones sin editar el lanzador

Tras `mvn install` o `mvn package`, el banco puede invocarse directamente.
En PowerShell, mantener entre comillas el classpath porque contiene `;`:

```powershell
java -cp 'bombardment-bench\target\classes;bombardment-bench\target\lib\*' edu.upc.epsevg.prop.bombardment.bench.Challenge challenges/exemple.properties
java -cp 'bombardment-bench\target\classes;bombardment-bench\target\lib\*' edu.upc.epsevg.prop.bombardment.bench.Challenge challenges/benchmark-1-profe1.properties
java -cp 'bombardment-bench\target\classes;bombardment-bench\target\lib\*' edu.upc.epsevg.prop.bombardment.bench.Challenge challenges/benchmark-validacio-1-profe1.properties
```

En Linux o macOS el separador es `:`:

```sh
java -cp 'bombardment-bench/target/classes:bombardment-bench/target/lib/*' edu.upc.epsevg.prop.bombardment.bench.Challenge challenges/exemple.properties
java -cp 'bombardment-bench/target/classes:bombardment-bench/target/lib/*' edu.upc.epsevg.prop.bombardment.bench.Challenge challenges/benchmark-1-profe1.properties
java -cp 'bombardment-bench/target/classes:bombardment-bench/target/lib/*' edu.upc.epsevg.prop.bombardment.bench.Challenge challenges/benchmark-validacio-1-profe1.properties
```

Para nuevas comparaciones, copiar `challenges/exemple.properties` y modificar
la copia. Las rutas `openings` y `output` se resuelven respecto al directorio
del `.properties`, no respecto al directorio de trabajo de la consola.
La clase `Challenge` permite también argumentos `clave=valor` tras el fichero.

Mantener `timeMs=200` en las comparaciones de evaluación: si esa clave falta,
el banco usa 1000 ms por defecto. La normativa recoge la
[configuración efectiva de referencia](normativa-y-restricciones.md#benchmarks-y-puntuación),
incluidas las opciones que se completan por defecto.

## Especificaciones de jugadores

| Especificación | Significado |
| --- | --- |
| `human` | Jugador manual en la interfaz. |
| `random` | Jugador aleatorio. |
| `profe1` | Rival de referencia de nivel 1. |
| `edu.upc.epsevg.prop.bombardment.player.MyPlayer` | Clase del jugador. |
| `edu.upc.epsevg.prop.bombardment.player.MyPlayer(4,true)` | Ejemplo de carga por constructor, cuando exista esa firma. |
| `v2=edu.upc.epsevg.prop.bombardment.player.MyPlayer(2)` | Etiqueta de informe y argumentos, cuando exista esa firma. |
| `jar:ruta/jugador.jar` | Jugador cargado desde un JAR empaquetado. |

El cargador admite argumentos de tipo `String`, `int`, `long`, `double` y
`boolean`. Actualmente `MyPlayer` solo ofrece constructor sin argumentos y
constructor con nombre `String`: los ejemplos con otras firmas no funcionan
hasta que esas variantes se implementen.

Para comparar versiones futuras, conservar variantes configurables o JAR
congelados de los tags correspondientes; cambiar solo la etiqueta del informe
no crea una versión distinta del jugador.

## Contrato del jugador

`MyPlayer` implementa `IPlayer` e `IAuto`. La interfaz de juego contiene:

```java
PlayerMove move(GameStatus s);
void timeout();
String getName();
```

`move()` recibe el estado y devuelve movimiento, nodos, profundidad completada
y tipo de búsqueda. La firma del contenedor es:

```java
PlayerMove(Move move, long numberOfNodesExplored, int maxDepthReached, SearchType searchType);
```

`SearchType.MINIMAX_IDS` identifica la búsqueda prevista. `setHeuristic(double)`
permite informar opcionalmente del valor desde la perspectiva del jugador que
mueve. El nombre visible se obtiene de `getName()` y puede personalizarse.
La clase, el paquete y `player.class` se conservan.

## API de `GameStatus`

Coordenadas: `x` columna, `y` fila. `board[y][x]`; fila 0 abajo. Valores `1`
para blancas, `-1` para negras y `0` para vacío. Una matriz escrita en Java
presenta sus filas en el orden inverso al dibujo usual del tablero.

### Construcción

| Firma | Uso |
| --- | --- |
| `GameStatus(int n)` | Tablero cuadrado con dos filas por jugador. |
| `GameStatus(int n, int rows)` | Filas iniciales configurables. |
| `GameStatus(byte[][] board, PlayerType nextTurnPlayer)` | Posición arbitraria, con matriz cuadrada. |
| `GameStatus(GameStatus other)` | Copia para generar hijos sin modificar el padre. |
| `static GameStatus fromFen(String fen)` | Lectura de una posición FEN. |

### Consulta

| Firma | Resultado |
| --- | --- |
| `int getSize()` | Tamaño del tablero. |
| `boolean isInside(int x, int y)` | Pertenencia de una coordenada al tablero. |
| `int getPos(int x, int y)` / `int getPos(Point p)` | Contenido de una casilla. |
| `PlayerType getCurrentPlayer()` | Jugador al turno. |
| `boolean isGameOver()` | Estado terminal. |
| `PlayerType getWinner()` | Ganador; `null` si hay tablas o todavía no terminó. |
| `boolean isDraw()` | Tablas por tablero vacío. |
| `int getStoneCount(PlayerType p)` | Piedras de un jugador. |
| `List<Point> getStones(PlayerType p)` | Posiciones de sus piedras. |
| `int getGoalRow(PlayerType p)` | Fila de meta del jugador. |
| `Move getLastMove()` | Última jugada, o `null`. |
| `int getPlies()` | Número de medias jugadas realizadas. |
| `String toFen()` | Representación textual del tablero y turno. |
| `boolean equals(Object o)` / `int hashCode()` | Identidad por tablero y turno. |
| `String toString()` | Dibujo textual del tablero. |

### Generación y aplicación de jugadas

| Firma | Contrato |
| --- | --- |
| `List<Move> getMoves()` | Lista nueva de jugadas legales, pasos primero; vacía si terminó. |
| `boolean isLegal(Move m)` | Legalidad en ese estado. |
| `int explosionBalance(int x, int y)` | Rivales eliminados menos propias eliminadas, incluida la que explota; cero en casilla vacía. |
| `void movePiece(Move m)` | Aplica movimiento y cambia turno; lanza `IllegalArgumentException` si no es legal. |
| `protected void setCell(int x, int y, int v)` | Punto de actualización al heredar; llamar a `super`; no se invoca en constructores. |

`forceLoser(PlayerType)` es público para el motor; el jugador no lo utiliza.

### Ejemplo de coordenadas y explosión

Ejemplo de consulta de la API, conservado como documentación:

```java
byte[][] board = {
    { 1,  1,  0,  0,  0},
    { 0,  1,  0,  0,  0},
    { 0,  0, -1,  0,  0},
    { 0,  0,  0,  0,  0},
    {-1, -1,  0,  0, -1},
};
GameStatus s = new GameStatus(board, PlayerType.PLAYER1);
s.getPos(2, 2);           // -1: negra en c3
s.explosionBalance(1, 1); // -2: cae una negra y tres blancas
```

La notación `c2-d3` indica un paso; `e5*`, una explosión. El FEN escribe filas
de arriba abajo separadas por `/`, con `W`, `B` y `.`, y añade `w` o `b`
para el turno. Ejemplo 4 × 4: `BBBB/..../..../WWWW w`.

## Aperturas y coste orientativo de las pruebas

| Conjunto | Aperturas | Partidas al intercambiar colores | Coste orientativo a 200 ms |
| --- | --- | --- | --- |
| `prova-10` | 10 | 20 | Unos 3 minutos. |
| `prova-25` | 25 | 50 | Unos 8 minutos. |
| `prova-50` | 50 | 100 | Unos 15 minutos. |
| `benchmark-A` | 100 | 200 | Alrededor de una hora. |
| `benchmark-B` | 100 | 200 | Mismo tamaño de validación. |

Son referencias de coste de ejecución, no un calendario de trabajo ni tiempos
medidos del jugador actual. El hardware y la duración de las partidas influyen.

La comprobación de los FEN actuales encuentra tamaños 10, 25, 50, 100 y 100.
Los diez casos de `prova-10` están en `prova-25`, y los 25 de este último están
en `prova-50`: los conjuntos rápidos se solapan. A y B son disjuntos entre sí
y respecto a los rápidos. Esto confirma el comentario de `exemple.properties`
y corrige la afirmación de disjunción de los conjuntos rápidos de la referencia
inicial. La [evidencia de aperturas](evidencias/aperturas.json) conserva los
recuentos e intersecciones. Repetir la comprobación si cambian los archivos.

## Protocolo de experimentación

1. Escribir la hipótesis y fijar qué única variable se cambia.
2. Fijar rivales reales, variantes, aperturas, colores, 200 ms, gracia, aislamiento,
   opciones de JVM, paralelismo, semilla si corresponde y entorno de ejecución.
3. Compilar y ejecutar las pruebas de corrección antes del challenge.
4. Realizar primero una prueba rápida; ampliar la muestra para tomar decisiones.
5. Revisar incidencias de ambos jugadores, máximos de respuesta y resultado por color.
6. Copiar HTML y CSV originales de `results/` a `experiments/`, junto con la
   configuración y la identidad de las versiones comparadas.
7. Anotar puntuación y error estándar del informe, profundidad y nodos con la
   misma convención. Distinguir pruebas a profundidad fija de pruebas a tiempo fijo.
8. Incorporar las evidencias y el registro al commit que se etiqueta; publicar
   ese tag en el repositorio privado cuando se cierre la etapa.

No sumar resultados de conjuntos solapados como si fueran nuevas aperturas.
La evidencia de una mejora se basa en su comparación controlada, no en ganar
una partida de la interfaz. B se reserva para validación, sin ajuste de pesos.

El HTML del banco muestra puntuación, error estándar, Elo, profundidad,
incidencias y partidas. El CSV conserva también FEN, jugadas, nodos y tiempos
máximos por partida. Los logs están en `results/logs/`; revisar especialmente
los máximos que se acercan a 200 + 100 ms tras el calentamiento.

## Comandos de empaquetado conservados

Ejemplo con el ID **ilustrativo** `G_E76`; sustituirlo por el ID real.
En Linux o macOS, desde la raíz:

```sh
cd bombardment-player && mvn clean && cd ..
zip -r G_E76.zip bombardment-player -x "*/.git/*" "*/target/*"
```

En `cmd` de Windows, desde la raíz:

```bat
cd bombardment-player && mvn clean && cd ..
tar -a -c -f G_E76.zip --exclude=.git --exclude=target bombardment-player
```

Windows 10 y posteriores incluyen `tar`; `-a` selecciona ZIP por la extensión.
También es posible comprimir la carpeta desde el Explorador después de
limpiarla. Inspeccionar el ZIP y extraerlo fuera del proyecto para ejecutar
`mvn package` con la API instalada. Son instrucciones para I11; todavía no se
ha creado ni entregado el paquete final.

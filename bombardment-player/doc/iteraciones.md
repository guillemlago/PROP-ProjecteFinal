# Plan de trabajo por iteraciones

El objetivo es completar un jugador correcto, competitivo y explicable,
con experimentos reproducibles y una entrega comprobada. **No se asignan
fechas ni duraciones.** Se avanza cuando se cumplen los criterios de cierre.
Las fechas del [diario](registre.md) corresponderán al trabajo realmente hecho.
La [matriz de cobertura](cobertura-enunciado.md) relaciona cada requisito con
las iteraciones y las evidencias que permitirán verificarlo.

## Punto de partida

La infraestructura compila y sus 13 pruebas existentes pasan. `MyPlayer`
selecciona movimientos aleatorios, devuelve cero nodos y profundidad cero,
y todavía no tiene búsqueda ni pruebas propias. La valoración de material
presente en la clase no interviene en la selección del movimiento.

La base conceptual es el trabajo de Connecta-4: copias del tablero,
terminales antes del corte de profundidad, evaluación desde un punto de
vista fijo, minimax, alfa-beta y comparación de ordenaciones. De Multi-Snake
se conserva el hábito de justificar heurísticas y registrar métricas.
Bombardment necesita su propia valoración de avances y explosiones; una
heurística de ventanas de cuatro fichas no representa su objetivo.

## Tablero de avance

| Iteración | Resultado esperado | Dependencia | Estado |
| --- | --- | --- | --- |
| I00 | Documentación organizada y diario iniciado | Ninguna | Preparada; etapa del diario abierta |
| I01 | Modelo comprendido y casos de referencia | I00 | Pendiente; compilación inicial comprobada |
| I02 | Minimax de referencia a profundidad fija | I01 | Pendiente |
| I03 | Alfa-beta equivalente y medible | I02 | Pendiente |
| I04 | Profundización iterativa que respeta `timeout()` | I03 | Pendiente |
| I05 | Heurística propia explicada y contrastada | I04 | Pendiente |
| I06 | Ordenación de jugadas con mejora medida | I05 | Pendiente |
| I07 | Tabla de transposiciones correcta y acotada | I06 | Pendiente |
| I08 | Decisión documentada sobre mejoras tácticas | I07 | Pendiente; técnicas opcionales |
| I09 | Versión candidata y validación independiente | I08 | Pendiente |
| I10 | Memoria completa y preparación de la defensa | I09 | Pendiente; redacción progresiva desde I01 |
| I11 | ZIP reproducido y lista de entrega cerrada | I10 | Pendiente |

Los identificadores de versión de este plan son propuestas. No representan
tags creados ni experimentos realizados. Un tag solo se anotará como
existente cuando apunte al commit que contiene la versión y sus evidencias.

La ordenación avanzada, las tablas de transposiciones, Zobrist y las variantes
de búsqueda se estudian en I06–I08 como mejoras candidatas. Su adopción no es
obligatoria en el enunciado: se conservarán si se entienden y aportan valor.
Una alternativa descartada puede cerrar su estudio con una decisión y su evidencia.

## Criterio común de cierre

- [ ] Las tareas de la iteración están resueltas y sus decisiones se entienden.
- [ ] Pasan las pruebas de corrección afectadas; no se introducen incidencias.
- [ ] Se comparan variantes con una sola diferencia cuando se atribuye una mejora.
- [ ] Se conserva el código probado y, para cada challenge citado, su HTML y CSV.
- [ ] El diario recoge configuración, resultados reales y limitaciones.
- [ ] Se actualiza la memoria con las evidencias disponibles.
- [ ] La etapa técnica tiene un commit y tag verificables.
- [ ] Ambos integrantes pueden explicar y modificar lo desarrollado.

El criterio de challenge se aplica a las etapas con comparativas de juego.
Una revisión documental o una prueba unitaria se registra como tal, sin
inventar partidas, porcentajes, ficheros ni tags.

## I00 · Preparación y organización

**Resultado:** disponer de un mapa de trabajo y una documentación consultable.

- [x] Revisar los módulos, el README inicial y el trabajo previo disponible.
- [x] Redactar este plan, sin calendario y con dependencias.
- [x] Centralizar normativa, restricciones, evaluación y entrega.
- [x] Convertir los nueve PDF a Markdown, conservando sus 201 páginas visuales.
- [x] Conservar íntegra la referencia inicial y sus comandos.
- [x] Preparar la memoria, el índice de evidencias y el diario real.
- [x] Comprobar la compilación inicial y registrar su alcance.
- [ ] Confirmar integrantes, nombre e identificador del equipo del proyecto final.
- [ ] Verificar inscripción y los NIF requeridos en el registro, además del acceso de revisión al GitHub privado.
- [ ] Guardar los documentos en un commit y registrar su identificador real.
- [ ] Crear y publicar el tag de la etapa documental, anotando el commit que contiene sus evidencias.

**Cierre:** documentos enlazados y revisados, datos de equipo confirmados y
primera etapa del diario cerrada con su versión. La organización local no
confirma la configuración del repositorio remoto ni la inscripción.

## I01 · Reglas, API y casos de referencia

**Resultado:** comprender qué posiciones y movimientos debe manejar el jugador.

- [ ] Comprobar JDK 17 o posterior, Maven y compilación independiente del jugador con la API instalada.
- [ ] Repasar avances, diagonales vacías, explosiones y finales con ambos colores.
- [ ] Fijar las convenciones: `board[y][x]`, fila cero abajo y turno en cada estado.
- [ ] Preparar posiciones pequeñas y FEN con soluciones calculables a mano.
- [ ] Cubrir victoria por meta, eliminación, explosión que deja tablas y bordes.
- [ ] Comprobar que generar hijos mediante copia no modifica el estado recibido.
- [ ] Definir qué cuenta como nodo y como profundidad en todas las variantes.
- [ ] Documentar el tratamiento de estados terminales según el contrato del motor.

**Validación:** casos con los dos colores, una única jugada legal, posiciones
terminales y simetrías equivalentes. Conservar los estados de referencia para
las iteraciones siguientes.

**Cierre:** resultados esperados razonados y comprobables. Versión propuesta:
`v0.1-casos`. Documentar modelo y métricas en la memoria.

## I02 · Minimax de referencia

**Resultado:** búsqueda sencilla que sirva para comprobar las optimizaciones.

- [ ] Adaptar el esquema MAX/MIN trabajado en Connecta-4 a `Move` y `GameStatus`.
- [ ] Mantener el punto de vista del jugador raíz durante toda la búsqueda.
- [ ] Resolver terminales antes de evaluar el límite de profundidad.
- [ ] Usar inicialmente una evaluación sencilla, como diferencia de piedras.
- [ ] Inicializar la elección con una jugada legal, incluso si todas pierden.
- [ ] Establecer desempate determinista y convención de nodos.
- [ ] Separar terminales y heurística: ninguna valoración no terminal supera una victoria.
- [ ] Conservar una forma de ejecutar la referencia a profundidad fija para las pruebas.

**Validación:** victoria inmediata, defensa obligada, explosión decisiva,
tablas, derrota inevitable y equivalencia para ambos colores. Comparar el
valor obtenido con una enumeración manual en árboles pequeños.

**Cierre:** decisiones y valores correctos. Esta variante sirve de referencia
de corrección; no se considera todavía un jugador válido bajo tiempo.
Versión propuesta: `v0.2-minimax`.

## I03 · Poda alfa-beta

**Resultado:** obtener el valor de minimax explorando menos nodos.

- [ ] Incorporar alfa, beta y la condición de corte `alfa >= beta`.
- [ ] Propagar las cotas actuales desde la raíz y conservar el desempate definido.
- [ ] Comparar minimax y alfa-beta a igual profundidad, heurística y orden.
- [ ] Medir nodos y tiempo sin mezclar todavía otras optimizaciones.
- [ ] Preparar posiciones generadas con semillas fijas para ampliar la comparación.

**Validación:** igualdad de valores y jugada óptima; con idéntico orden y
desempate, comprobar también la selección de jugada. Incluir todas las
pruebas tácticas y casos donde se producen cortes.

**Cierre:** equivalencia comprobada y ahorro de nodos documentado; no se exige
que toda posición produzca una poda. Versión propuesta: `v0.3-alfabeta`.

## I04 · Profundización iterativa y tiempo

**Resultado:** jugador funcional dentro del presupuesto de 200 ms.

- [ ] Completar profundidades sucesivas 1, 2, 3… usando alfa-beta.
- [ ] Preparar una jugada legal de reserva antes de iniciar una búsqueda costosa.
- [ ] Consultar la señal `volatile` de `timeout()` en cada nodo y en operaciones largas.
- [ ] Descartar el resultado raíz de una iteración interrumpida.
- [ ] Devolver la mejor jugada de la última iteración completada.
- [ ] Reiniciar correctamente señal, contadores y estado de cada llamada a `move()`.
- [ ] Informar de nodos reales y profundidad completada en `PlayerMove`.
- [ ] Detener la profundización cuando el resultado esté resuelto o no quede trabajo útil.
- [ ] Revisar búsqueda monohilo, ausencia de archivos/red/`System.exit`, inactividad durante el turno rival y salida de depuración moderada.

**Validación:** interrupción antes de completar la primera profundidad,
interrupción a mitad de iteración, llamadas consecutivas, ambos colores y
posiciones con mucha ramificación. Ejecutar partidas en JVM aislada, con el
presupuesto y memoria de competición, incluyendo arranque frío y proceso caliente.

**Cierre:** cero jugadas ilegales, `null`, excepciones o procesos terminados
por el motor en las pruebas realizadas. No utilizar la gracia como tiempo
adicional de búsqueda. Versión propuesta: `v0.4-tiempo`.

## I05 · Heurística específica de Bombardment

**Resultado:** evaluar posiciones con criterios del juego y pesos justificables.

- [ ] Escribir una hipótesis por componente antes de incorporarlo.
- [ ] Estudiar material, avance hacia la meta y amenazas de victoria inmediata.
- [ ] Estudiar movilidad, caminos despejados y exposición a explosiones rivales.
- [ ] Valorar el balance de una explosión sin confundir ganancia de material con victoria.
- [ ] Probar términos por separado y después combinados, manteniendo un coste asumible.
- [ ] Ajustar pesos con los conjuntos de desarrollo y reservar `benchmark-B`.
- [ ] Comparar cada aportación con una variante que la desactive.
- [ ] Documentar unidades, perspectiva de evaluación y rango de valores.

**Validación:** posiciones comparables con avance seguro, amenaza rival,
explosión favorable y sacrificio perjudicial. Comprobar signos para ambos
colores y que los terminales dominan a la heurística.

**Cierre:** fórmula comprensible y aportaciones respaldadas por pruebas.
No se aceptan todos los términos por defecto: conservar los que aporten
valor. Versión propuesta: `v0.5-heuristica`.

## I06 · Ordenación de movimientos

**Resultado:** mejorar los cortes y la profundidad útil dentro del mismo tiempo.

- [ ] Probar primero la mejor jugada de la iteración anterior, si sigue siendo legal.
- [ ] Estudiar un orden barato para victorias, amenazas, avances y explosiones.
- [ ] Comparar el coste de ordenar con el ahorro conseguido.
- [ ] Añadir killer moves o historial solo como experimentos separados y explicables.
- [ ] Mantener una variante sin ordenación para aislar su efecto.

**Validación:** el valor a profundidad fija coincide con la referencia. Si
cambia una jugada empatada, justificarlo. Comparar nodos a profundidad fija
y profundidad/puntuación bajo 200 ms; son mediciones diferentes.

**Cierre:** mejora medida o decisión de descartar una variante con su evidencia.
Versión propuesta: `v0.6-ordenacion`.

## I07 · Transposiciones y hash

**Resultado:** reutilizar búsquedas sin alterar su corrección ni desbordar memoria.

- [ ] Justificar con estados reales por qué órdenes distintos pueden confluir.
- [ ] Definir una clave de tablero y turno; incluir tamaño si la representación lo necesita.
- [ ] Diseñar entradas con profundidad, valor, tipo de cota y mejor jugada.
- [ ] Distinguir valores exactos, cotas inferiores y cotas superiores.
- [ ] Definir capacidad, reemplazo y verificación de clave ante colisiones de índice.
- [ ] Si se usa Zobrist incremental, verificar avances y todas las eliminaciones de una explosión.
- [ ] Si se puntúa por distancia al final, normalizarla al guardar y recuperar valores.
- [ ] Evitar guardar como exacto un resultado incompleto por interrupción.
- [ ] Comparar con tabla desactivada y medir memoria dentro de `-Xmx1g`.

**Validación:** claves distintas según turno, equivalencia con hash recalculado,
colisiones forzadas por capacidad pequeña y equivalencia con alfa-beta sin
tabla en posiciones pequeñas.

**Cierre:** corrección y límites comprobados; mantener la tabla en la versión
final solo si su beneficio justifica el coste. Versión propuesta: `v0.7-transposiciones`.

## I08 · Mejoras tácticas y selección de técnicas

**Resultado:** decidir si compensa añadir una mejora adicional al jugador estable.

- [ ] Analizar derrotas concretas y distinguir errores de búsqueda y de evaluación.
- [ ] Estudiar extensiones tácticas limitadas si las explosiones causan efecto horizonte.
- [ ] Considerar búsqueda de ventana principal o ventanas de aspiración únicamente si se pueden justificar.
- [ ] Aplicar como máximo una técnica nueva por comparación.
- [ ] Acotar toda extensión y mantener las comprobaciones de interrupción.
- [ ] Registrar también las alternativas descartadas y el motivo.

**Validación:** regresión táctica, equivalencia cuando la técnica debe ser
exacta y comparativas con/sin cambio bajo el mismo presupuesto.

**Cierre:** decisión razonada sobre cada candidato. La iteración puede cerrarse
sin incorporar ninguna técnica adicional. Versión propuesta: `v0.8-seleccion`.

## I09 · Experimentos finales y versión candidata

**Resultado:** seleccionar una versión robusta con evidencia reproducible.

- [ ] Congelar las variantes antes de la comparación final.
- [ ] Completar las comparativas entre versiones para cada mejora conservada.
- [ ] Ejecutar `benchmark-A`: 100 aperturas, dos colores, 200 partidas y 200 ms.
- [ ] Ejecutar la validación reservada `benchmark-B` con la misma configuración.
- [ ] Verificar 8 × 8, dos filas, `timeMs=200`, `graceMs=100`, aislamiento, `-Xmx1g`, `-XX:ActiveProcessorCount=1` y `parallel=1` en la configuración efectiva.
- [ ] Comparar puntuación, error estándar, profundidad, nodos e incidencias.
- [ ] Revisar resultados por color y derrotas representativas mediante sus FEN y jugadas.
- [ ] Guardar HTML, CSV, configuración efectiva, entorno e identificadores de versión.
- [ ] Comprobar robustez con rivales propios de estilos distintos.
- [ ] Documentar que el rival oculto no puede validarse localmente.

**Cierre:** cero incidencias del jugador, datos consistentes y candidato
seleccionado por evidencia. Objetivo local: al menos 75 % contra la referencia
de nivel 1, con margen y sin degradación clara en la validación. Alcanzarlo
no permite afirmar un resultado frente al rival oculto.

Si la validación descubre un problema, volver a la iteración correspondiente.
Una vez consultado B, no reutilizarlo como conjunto de ajuste: buscar una
validación nueva e independiente para posteriores cambios. Versión propuesta: `v0.9-candidata`.

## I10 · Memoria y preparación de la defensa

**Resultado:** explicar qué se hizo, por qué y cuánto aporta.

- [ ] Revisar los tres bloques de documentación: optimizaciones (1,25), heurística (1,25) y resumen (0,5 puntos).
- [ ] Completar las comparativas con/sin cada optimización y sus limitaciones.
- [ ] Explicar la heurística, su ajuste y la aportación de sus componentes.
- [ ] Incorporar un resumen de resultados verificable con los CSV.
- [ ] Generar las imágenes de tablas y gráficas en `doc/img/` y usar rutas relativas.
- [ ] Revisar coherencia entre memoria, diario, código, tags y evidencias.
- [ ] Completar la declaración real de uso de IA.
- [ ] Ensayar la explicación de minimax, cotas, interrupción, hash y heurística.
- [ ] Practicar modificaciones pequeñas del código y razonar sus consecuencias.
- [ ] Revisar nombres, responsabilidades, comentarios y complejidad del código existente.

**Cierre:** memoria sin resultados inventados ni apartados pendientes; ambos
integrantes pueden defenderla y modificar el jugador. La discusión y las
conclusiones las redacta el equipo a partir de los datos. Versión propuesta: `v1.0-documentada`.

## I11 · Reproducción y entrega

**Resultado:** un paquete correcto que reproduzca el jugador documentado.

- [ ] Confirmar ID de este equipo, nombres e inscripción; no asumir que coincide con otra actividad.
- [ ] Revisar uno por uno PF01–PF20 y los requisitos de la matriz de cobertura, dejando evidencia o un pendiente explícito.
- [ ] Comprobar constructor sin argumentos, paquete, `MyPlayer` y `player.class`.
- [ ] Ejecutar las pruebas finales y compilar el módulo independiente con la API instalada.
- [ ] Limpiar `target/` y preparar `[ID_EQUIP].zip` con una carpeta raíz `bombardment-player/`.
- [ ] Incluir `pom.xml`, fuentes, documentación, imágenes y experimentos citados.
- [ ] Excluir salidas temporales y comprobar que los enlaces necesarios funcionan dentro de la entrega.
- [ ] Extraer el ZIP en otra carpeta y ejecutar allí `mvn package`.
- [ ] Verificar el JAR y realizar una prueba de carga del jugador empaquetado.
- [ ] Comprobar acceso de revisión y publicación de los tags en el GitHub privado.
- [ ] Registrar paquete, hash, versión y resultado de la reproducción.
- [ ] Designar al integrante que realizará la entrega y confirmar su envío cuando ocurra.

**Cierre:** paquete revisado y reproducido, evidencias archivadas y envío
confirmado. Preparar un ZIP no equivale a haberlo entregado. Versión propuesta: `v1.0-entrega`.

## Reparto del trabajo en pareja

En cada iteración, un integrante conduce el desarrollo y el otro revisa las
pruebas y su explicación; intercambiar funciones en la siguiente. Los nombres
se anotarán en el diario al realizar el trabajo. Los dos revisan los cambios
del algoritmo y firman las decisiones de selección de versión.

## Condición de proyecto completo

El proyecto está completo cuando I01–I11 cumplen sus criterios, la etapa de
preparación está versionada, todas las restricciones están verificadas y el
paquete entregado coincide con el código y los datos de la memoria.

La puntuación máxima combina 5 puntos frente a la referencia de nivel 1,
2 frente al rival de nivel 2 y 3 de documentación. El rival de nivel 2 y sus
aperturas no están disponibles: el objetivo del 10 guía el trabajo, pero su
resultado no se puede certificar localmente. El bonus del torneo es adicional.

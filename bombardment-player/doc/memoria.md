# Memoria · Bombardment

**Estado:** estructura de trabajo; desarrollo y experimentos del jugador pendientes.
**Equipo, ID e integrantes:** pendientes de confirmar para este proyecto.

La memoria se completará de forma progresiva durante las
[iteraciones](iteraciones.md), usando las evidencias del [diario](registre.md).
Los apartados siguientes son una guía de redacción; todavía no contienen
análisis ni conclusiones experimentales.

## 1. Mejoras y optimizaciones

### 1.1 Búsqueda de referencia y corrección

Pendiente: describir la adaptación de minimax al juego, el tratamiento de
terminales, el punto de vista de evaluación, los desempates y la convención
de nodos. Enlazar sus pruebas de corrección.

### 1.2 Poda alfa-beta y control de tiempo

Pendiente: explicar las cotas, la equivalencia con minimax y la reducción
de nodos; después, la profundización iterativa, la jugada de reserva y la
interrupción sin publicar resultados incompletos.

### 1.3 Optimizaciones seleccionadas

Para cada mejora realmente incorporada: problema, funcionamiento,
decisiones de implementación, coste, versión con/sin mejora y evidencia.
Incluir resultados de las alternativas descartadas si ayudan a justificar
la selección. No presentar una técnica del plan como implementada.

Las comparativas diferenciarán pruebas a profundidad fija y bajo el mismo
presupuesto de tiempo. Las tablas y gráficas se generarán como imágenes en
`img/` y se enlazarán mediante rutas relativas cuando existan.

## 2. Heurística

### 2.1 Definición y perspectiva

Pendiente: fórmula, componentes, pesos, unidades y rango; separar valores
terminales de evaluaciones no terminales.

### 2.2 Hipótesis y ajuste

Pendiente: explicar qué representa cada componente y cómo se ajustaron los
pesos en los conjuntos de desarrollo, preservando la independencia de B.

### 2.3 Aportación de los componentes

Pendiente: comparar variantes con/sin cada componente y explicar sus
resultados. El equipo redactará la discusión a partir de los experimentos.

## 3. Resumen de resultados

### 3.1 Entorno y protocolo

Pendiente: máquina, JDK, opciones de JVM, tiempo, aislamiento, paralelismo,
aperturas, semillas, versiones y reglas de cómputo de métricas.

### 3.2 Comparaciones y versión final

Pendiente: resultados frente a la referencia de nivel 1, comparaciones
entre versiones, validación independiente, resultados por color, profundidad,
nodos, tiempos e incidencias. Incorporar puntuación y error estándar.

No se dispone del rival oculto de nivel 2. Sus resultados solo se incluirán
si llegan a estar disponibles, con su procedencia. No hay challenges del
jugador realizados en la preparación documental.

### 3.3 Discusión y límites

Pendiente: conclusiones del equipo sobre fortalezas, errores observados,
incertidumbre y límites. Cada afirmación cuantitativa deberá enlazar con los
HTML/CSV archivados. La compilación inicial y las trece pruebas de
infraestructura se documentan en el diario, sin tratarlas como rendimiento competitivo.

## 4. Declaración de uso de IA

Registro iniciado con el apoyo realmente utilizado; se actualizará durante
el desarrollo y se revisará antes de la entrega.

| Herramienta | Uso realizado | Ejemplos de peticiones |
| --- | --- | --- |
| OpenAI Codex | Organización del plan sin calendario; preparación del diario, índices y normativa; reorganización del README; conversión local de PDF a Markdown y comprobaciones documentales. | «pasa los documentos de documentacion a md y añade normativas y restricciones que te vayas encontrando en un md y lo pones todo en el repo clonado»; «no hagas codigo solo dejame preparado lo de las iteraciones, documentacion y normativa y restricciones»; «creo que tenemos que hacer un diario asi que empieza a redactarlo (revisa el enunciado)». |
| OpenAI Codex | Auditoría documental de cobertura: comparación con el enunciado completo, aclaración de comandos y configuración, y matriz de requisitos e iteraciones. | «Revisa que las iteraciones y la normativa cubran todo el enunciado y que el README conserve todos los comandos y la información importante, sin tocar el código.» |

Durante esta sesión no se han modificado las fuentes Java ni se han escrito
las conclusiones del proyecto. La discusión y el análisis experimental
quedan pendientes de los integrantes. Se ha utilizado una herramienta temporal
de conversión documental fuera del repositorio, sin incorporarla al proyecto.

**Valoración del equipo sobre esta ayuda:** pendiente de revisión y redacción
por los integrantes. Añadir cualquier uso posterior de autocompletado,
fragmentos pequeños o refactorizaciones con sus ejemplos reales.

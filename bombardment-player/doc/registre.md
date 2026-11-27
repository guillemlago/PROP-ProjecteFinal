# Diario de trabajo y experimentos

Registro cronológico del trabajo real del proyecto. Las iteraciones se
planifican [sin calendario](iteraciones.md); aquí se anotan las fechas en
que se realiza cada sesión. Las cifras proceden de evidencias conservadas.

## Cómo mantener el diario

- Añadir una entrada por sesión con responsables, cambios, comprobaciones,
  resultados, decisiones y trabajo pendiente.
- Cuando una etapa técnica se cierre, indicar el tag real de GitHub y el
  commit probado. El checkout del tag debe contener el código y sus evidencias.
- Registrar rivales y versiones, número de partidas, aperturas, tiempo,
  aislamiento, recursos y paralelismo en cada challenge.
- Copiar HTML y CSV de cada challenge citado a `../experiments/` e incluirlos
  en el commit del tag. Anotar puntuación y error, profundidad e incidencias.
- Distinguir planificación, revisión documental, pruebas unitarias y partidas.
  Una sesión sin challenge no recibe porcentajes ni resultados de juego.
- Mantener abiertas las etapas que aún no tienen revisión o versión guardada;
  no presentar un tag propuesto como existente.

Las condiciones del registro se recogen en
[normativa y restricciones](normativa-y-restricciones.md#proyecto-final-condiciones-obligatorias)
y en la [referencia inicial](../../docs/referencia/README-inicial.md#registre-dexperiments).

## 2026-11-27 · Sesión 01 · Preparación documental y revisión inicial

**Iteración:** I00. **Estado:** abierta, pendiente de revisión del equipo y
de guardar esta documentación en un commit con su tag. **Tag:** todavía no
creado. **Código inspeccionado y compilado:** commit `7bb12c2`.

**Participación:** preparación documental y comprobaciones con apoyo de
OpenAI Codex. La identificación de integrantes y el reparto nominal de
responsabilidades quedan pendientes de confirmar.

### Objetivo de la sesión

Organizar el proyecto final en iteraciones sin fechas de entrega, preparar
el diario, reunir las normas y restricciones y convertir el material de
consulta a Markdown. La sesión se limita a documentación y planificación.

### Trabajo realizado

- Revisada la estructura Maven y el contrato del jugador, el modelo y el banco.
- Revisados minimax, alfa-beta y la heurística de ventanas del trabajo de
  Connecta-4, además de la organización de la actividad anterior.
- Confirmado el estado inicial: `MyPlayer` elige al azar; su función de
  material no se usa para elegir, y comunica cero nodos y profundidad cero.
- Preparado el plan I00–I11 con tareas, dependencias y criterios de cierre.
- Reorganizado el README principal conservando comandos y contenido técnico.
- Archivado íntegramente el README inicial en `docs/referencia/README-inicial.md`.
- Convertidos nueve PDF de `DOCUMENTACION`: 201 páginas con texto extraíble
  y vistas originales, con manifiesto de procedencia y hashes.
- Centralizadas las restricciones de Bombardment y separadas las de
  Multi-Snake y el documento externo de instalación de aplicaciones.
- Preparada la estructura de la memoria y la declaración del apoyo de IA.
- Preparado el procedimiento para archivar y citar futuros experimentos.

### Comprobaciones y resultados reales

| Comprobación | Resultado | Evidencia |
| --- | --- | --- |
| `mvn -B -ntp clean install` con JDK compatible | Compilación e instalación correctas de los cinco proyectos Maven. | [Estado inicial](evidencias/estado-inicial.md). |
| Pruebas del modelo | 7 ejecutadas, 0 fallos, 0 errores y 0 omitidas. | [Informe del modelo](evidencias/inicial-edu.upc.epsevg.prop.bombardment.GameStatusTest.txt). |
| Pruebas del aislamiento | 6 ejecutadas, 0 fallos, 0 errores y 0 omitidas. | [Informe del aislamiento](evidencias/inicial-edu.upc.epsevg.prop.bombardment.engine.IsolationTest.txt). |
| Pruebas propias del jugador | No existen todavía; Maven informa que no hay pruebas que ejecutar en el módulo. | Revisión de `bombardment-player` y salida de compilación. |
| Conjuntos de aperturas | 10, 25, 50, 100 y 100 FEN; los rápidos se solapan y A/B son independientes entre sí y de ellos. | [Recuentos, intersecciones y hashes](evidencias/aperturas.json). |
| Conversión documental | Nueve Markdown y 201 vistas; las páginas sin texto extraíble se conservan visualmente. | [Manifiesto](../../docs/asignatura/manifest.json). |
| Conservación de información y enlaces | Referencia inicial íntegra al normalizar las rutas de imagen; enlaces locales y vistas comprobados sin errores. | [Revisión documental](evidencias/revision-documental.json) y [mapa de cobertura](../../docs/referencia/cobertura.md). |

Se han inspeccionado visualmente páginas representativas de los nueve
documentos, incluidos esquemas, capturas y páginas sin texto extraíble.
La comprobación de archivos confirma que los cambios del repositorio se
limitan a documentación y sus recursos; las fuentes y la configuración
del proyecto conservan su contenido.

La revisión del entorno utilizó Windows 11, Temurin 21.0.12.1 y Maven 3.9.11,
con compilación para Java 17. El PATH ordinario selecciona Java 8; la ejecución
usó un entorno temporal con el JDK compatible.

**Challenges realizados:** ninguno. No hay puntuación, error de juego,
profundidad competitiva ni incidencias de partidas que declarar. Las trece
pruebas del modelo y motor no demuestran la fuerza del jugador.

### Decisiones y asuntos detectados

- Desarrollar primero una referencia minimax comprobable, después alfa-beta
  y control de tiempo, y medir cada mejora posterior por separado.
- Mantener el plan sin fechas; usar fechas reales en este diario.
- Reservar `benchmark-B` para validar y no ajustar pesos con ese conjunto.
- Corregir en la documentación de trabajo una discrepancia: los conjuntos
  rápidos están anidados; no se deben contar como muestras independientes.
- Conservar las atribuciones y el contenido de los documentos de referencia.
- Mantener como pendientes las búsquedas, heurística y pruebas del jugador.

### Pendiente para cerrar la etapa

- [ ] Revisar los documentos entre los dos integrantes y confirmar el reparto.
- [ ] Confirmar nombre, miembros, ID e inscripción del equipo del proyecto final.
- [ ] Comprobar visibilidad privada y acceso de revisión del repositorio GitHub.
- [ ] Guardar la documentación y sus evidencias en un commit.
- [ ] Crear y publicar el tag de esta etapa y anotar aquí su nombre e identificador reales.

## 2026-11-27 · Sesión 02 · Auditoría de cobertura del enunciado

**Iteración:** I00. **Estado:** etapa documental abierta; commit y tag aún
pendientes de guardar. **Referencia revisada:** `7bb12c2:README.md` completo.
**Participación:** revisión documental con apoyo de OpenAI Codex.

### Objetivo y trabajo realizado

- Contrastados los apartados del enunciado con las iteraciones, la normativa,
  el README y la guía técnica.
- Preparada una [matriz de 32 puntos de cobertura](cobertura-enunciado.md),
  con fuente, iteraciones afectadas y comprobación prevista.
- Añadidas al plan las comprobaciones explícitas de entorno, restricciones
  de ejecución, configuración efectiva de benchmark y revisión final PF01–PF20.
- Aclarado que transposiciones, Zobrist y variantes avanzadas son candidatas
  opcionales, cuya adopción requiere una decisión justificada.
- Completados en el README los lanzadores de ambas plataformas, `mvn install`,
  `CONFIG`, `playerA`/`playerB` y la recuperación de etapas por `git checkout`.
- Corregida la invocación documentada de los scripts de Linux/macOS: requieren
  `bash`, según sus cabeceras y el uso de `set -euo pipefail`.
- Documentado que el banco usa 1000 ms si se omite `timeMs`, mientras que los
  benchmarks de evaluación fijan explícitamente 200 ms.
- Conservada la distinción entre requisitos obligatorios, recomendaciones,
  decisiones internas y condiciones de actividades anteriores.

### Comprobaciones y límites

La [auditoría archivada](evidencias/auditoria-enunciado.json) recoge la
conservación de los comandos, las 30 firmas extraídas de los bloques de API,
los enlaces locales, la referencia inicial y la comparación de hashes de los
archivos protegidos antes y después de esta revisión.

Esta sesión no añade compilaciones ni challenges. Las trece pruebas del
modelo y motor pertenecen a la sesión inicial; no se presentan como pruebas
nuevas. La cobertura verificada es documental: implementación, experimentos,
inscripción, acceso remoto y tags siguen pendientes según el plan.

## Plantilla para una nueva sesión

Copiar este apartado al añadir actividad real; no rellenar resultados por adelantado.

- **Fecha real y número de sesión:** pendiente.
- **Iteración y estado:** pendiente.
- **Responsables y revisión:** pendiente.
- **Commit de código y tag real, o motivo por el que la etapa sigue abierta:** pendiente.
- **Objetivo y cambios realizados:** pendiente.
- **Hipótesis o problema tratado:** pendiente.
- **Pruebas o comandos realmente ejecutados:** pendiente.
- **Resultados y enlaces a las evidencias:** pendiente.
- **Decisión del equipo y justificación:** pendiente.
- **Limitaciones y siguiente paso:** pendiente.

Para un challenge, añadir:

- **Jugador A y versión / jugador B y versión:** pendiente.
- **Configuración, aperturas y número de partidas a ambos colores:** pendiente.
- **Tiempo, gracia, JVM, aislamiento, paralelismo, semilla y entorno:** pendiente.
- **Victorias / tablas / derrotas y puntuación ± error estándar:** pendiente.
- **Profundidad, nodos y tiempo máximo de A y B:** pendiente.
- **Incidencias de cada jugador, con su tipo:** pendiente.
- **HTML, CSV y configuración archivados en `../experiments/`:** pendiente.
- **Comparación con la hipótesis y decisión, redactadas por el equipo:** pendiente.

# Revisión inicial del proyecto

**Fecha real:** 2026-11-27. **Código revisado:** commit `7bb12c2`.
Esta comprobación precede al desarrollo del jugador. Las modificaciones de
la sesión son documentales; no alteran las fuentes Java, los POM ni los lanzadores.

## Estado del jugador

`MyPlayer` escoge al azar entre los movimientos de `getMoves()` y devuelve
cero nodos y profundidad cero. La función de evaluación de material está
presente, pero no interviene en esa elección. No hay pruebas propias en el
módulo del jugador. La implementación de búsqueda sigue pendiente.

## Entorno de la comprobación

| Elemento | Valor observado |
| --- | --- |
| Sistema | Windows 11, amd64. |
| JDK utilizado | Eclipse Temurin 21.0.12.1+1-LTS. |
| Nivel de compilación | Java 17 (`maven.compiler.release`). |
| Maven | Apache Maven 3.9.11. |
| Comando | `mvn -B -ntp clean install`, desde la raíz. |
| Resultado global | `BUILD SUCCESS`; los cinco proyectos Maven terminan correctamente. |
| Tiempo global informado por Maven | 31,258 s; es tiempo de construcción, no tiempo de búsqueda. |

El entorno ordinario selecciona Java 8 y no encuentra Maven en PATH. Se
seleccionaron temporalmente el JDK 21 y Maven disponibles para este proceso,
sin modificar la configuración global del equipo.

## Pruebas ejecutadas

| Suite | Ejecutadas | Fallos | Errores | Omitidas | Informe conservado |
| --- | --- | --- | --- | --- | --- |
| `GameStatusTest` | 7 | 0 | 0 | 0 | [Modelo](inicial-edu.upc.epsevg.prop.bombardment.GameStatusTest.txt). |
| `IsolationTest` | 6 | 0 | 0 | 0 | [Aislamiento](inicial-edu.upc.epsevg.prop.bombardment.engine.IsolationTest.txt). |
| Total | 13 | 0 | 0 | 0 | Suites existentes de infraestructura. |

Maven indicó que el módulo del jugador no tiene pruebas que ejecutar.
El repositorio local de dependencias emitió avisos por ausencia de checksums
para el artefacto de referencia; no impidieron completar la construcción.

## Alcance de la evidencia

La compilación y las pruebas existentes comprueban la base de trabajo.
No se ejecutaron challenges ni se midió fuerza de juego, profundidad útil,
cumplimiento competitivo del tiempo o rendimiento de una búsqueda propia.

La [comprobación de aperturas](aperturas.json) conserva el tamaño, las
intersecciones y los hashes de los conjuntos actuales. El
[manifiesto documental](../../../docs/asignatura/manifest.json) identifica
los nueve PDF y las 201 páginas de la conversión.

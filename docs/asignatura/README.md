# Material de consulta en Markdown

Conversión de los nueve PDF de `DOCUMENTACION`: **201 páginas**, con texto
extraíble y una vista de cada página. Se conserva el idioma y la autoría
presentes en los documentos. Los originales permanecen en su ubicación.

| Documento | Páginas | Uso en el proyecto |
| --- | --- | --- |
| [Java: sesión 1](java-sesion-1.md) | 30 | Sintaxis y fundamentos de Java. |
| [Java: colecciones y mapas](java-colecciones.md) | 81 | POO, colecciones y estructuras de datos. |
| [Java: sesión 3](java-sesion-3.md) | 28 | Material complementario de Java. |
| [Búsqueda no informada](cerca-no-informada.md) | 12 | Representación y exploración del espacio de estados. |
| [Búsqueda informada](cerca-informada.md) | 8 | Heurísticas y evaluación de alternativas. |
| [Git con NetBeans](git-netbeans.md) | 15 | Flujo de trabajo con el IDE y control de versiones. |
| [Guía rápida de Git](guia-git.md) | 16 | Commits, ramas y sincronización. |
| [Actividad 1: Multi-Snake](actividad-1-multi-snake.md) | 9 | Contexto de la actividad anterior, con requisitos propios. |
| [Instalación de aplicaciones: htop](hkt2-instalacion-aplicaciones.md) | 2 | Documento externo al proyecto Bombardment. |

## Cómo consultar la conversión

Cada documento tiene apartados por página. El texto se presenta en bloques
para preservar ejemplos, comandos y distribución sin interpretar símbolos
como etiquetas de Markdown. La sección desplegable **Ver página original**
permite consultar esquemas, capturas, tablas y texto integrado en imágenes.

No se ha aplicado OCR. Las páginas sin texto extraíble están identificadas
en el documento y en [el manifiesto](manifest.json). Algunas otras páginas
solo permiten extraer un encabezado o pie: su contenido completo sigue
disponible en la vista original. La conversión no sustituye una revisión
visual de fórmulas, diagramas o fragmentos de código.

El manifiesto recoge el nombre y SHA-256 de cada PDF, el número de páginas,
el Markdown generado y los caracteres extraídos por página. Las 201 vistas
se encuentran en `img/`, agrupadas por documento.

## Alcance de los materiales

Las reglas vigentes de Bombardment están centralizadas en la
[normativa del proyecto](../../bombardment-player/doc/normativa-y-restricciones.md).
Las condiciones de Multi-Snake y de htop se recogen en apartados separados
de esa normativa. Los ejemplos antiguos de Java, Git o búsqueda son material
de aprendizaje; no añaden requisitos de entrega ni cambian la versión de Java
o los límites de ejecución de Bombardment.

Los ZIP de `DOCUMENTACION` contienen proyectos y bibliotecas, no documentos
PDF adicionales. Sus fuentes y Javadoc permanecen en su formato original;
no forman parte de esta conversión de los nueve documentos.

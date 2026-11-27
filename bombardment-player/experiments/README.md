# Evidencias de los experimentos

**Estado actual:** todavía no se han realizado challenges del jugador.
Las pruebas de infraestructura iniciales están en
[`../doc/evidencias/`](../doc/evidencias/estado-inicial.md).

Archivar aquí el HTML y CSV originales de cada challenge citado en el
[diario](../doc/registre.md). El banco los genera en `results/`; ese directorio
de salida está excluido de Git. Las copias citadas deben quedar versionadas
en esta carpeta, en el mismo commit al que apunta el tag de la etapa.

Para cada experimento conservar:

- Resumen `.html` y partidas `.csv` completos.
- Copia del `.properties` y de cualquier parámetro sobreescrito al ejecutar.
- Identificadores de commit/tag y parámetros de ambos jugadores.
- JDK, entorno, recursos, tiempo, gracia, aislamiento y paralelismo.
- Aperturas, semilla cuando corresponda y referencia al archivo utilizado.

Usar nombres con la **fecha real**, una descripción y un identificador de
ejecución; mantener la relación entre HTML y CSV. Las fechas no son plazos
planificados. Si se renombran archivos, registrar la correspondencia original.

## Índice

Sin entradas de juego por el momento. Al archivar un challenge, añadir una
fila con su identificador, hipótesis, versiones, configuración, HTML, CSV y
etapa del diario. Una propuesta de experimento permanece en el plan hasta
que se ejecute; no se crea aquí una fila con resultados estimados.

# Datos

## `crudos/`
Archivos **tal como se descargaron** del DANE. No se modifican nunca: son la fuente de verdad
y permiten reproducir todo el análisis desde cero.

Archivos esperados:

| Archivo | Descripción | Fuente | Fecha de descarga |
|---|---|---|---|
| _(pendiente)_ | Microdatos / anexos EAC 2024 | DANE | |

## `procesados/`
Datasets generados por `notebook/EAC_2024_analisis.ipynb` después de la limpieza y
transformación (valores nulos, duplicados, tipos de dato, codificaciones).

| Archivo | Generado por | Descripción |
|---|---|---|
| `eac_2024_limpio.csv` | Módulo 1 del notebook | Dataset depurado listo para análisis |

## Diccionario de variables

_(Pendiente — documentar aquí el nombre, tipo y significado de cada variable usada,
tomándolo de la ficha metodológica del DANE.)_

# Presentación de apoyo

| Archivo | Qué es |
|---|---|
| `EAC-2024-presentacion.pptx` | Presentación de apoyo del video — 15 diapositivas, formato 16:9, presentador único |
| `figuras/` | Las figuras de los cuadernos exportadas a PNG, que son las que usa la presentación |

El guion hablado, con tiempos por diapositiva, está en
[`../video/guion-video.md`](../video/guion-video.md). Cada diapositiva lleva además su
texto en las **notas del orador**, así que se puede presentar directamente desde la vista
de presentador de PowerPoint.

## Estructura

| # | Diapositiva | Etapa |
|---|---|---|
| 1 | Portada | — |
| 2 | Por qué la Encuesta Anual de Comercio | — |
| 3 | Separador | Etapa 1 |
| 4 | Nueve problemas, y tres se resolvieron sin tocar nada | Etapa 1 |
| 5 | Separador | Etapa 2 |
| 6 | La media describe a una empresa que casi no existe | Etapa 2 |
| 7 | El 1 % de las empresas hace el 38,6 % de las ventas | Etapa 2 |
| 8 | Los atípicos no son ruido: son el sector | Etapa 2 |
| 9 | Cada decisión está en una celda, con su salida | Etapa 2 |
| 10 | La hipótesis se confirma y se corrige | Etapa 2 |
| 11 | Separador | Etapa 3 |
| 12 | Estimar el tamaño de una empresa sin ver sus balances | Etapa 3 |
| 13 | La métrica que decide no es el R² | Etapa 3 |
| 14 | Qué decisión habilita esto en la práctica | Etapa 3 |
| 15 | Lo que me llevo | — |

## Cómo se regeneran las figuras

Salen de los cuadernos ya ejecutados, no se vuelven a calcular:

```python
import json, base64
nb = json.load(open("notebook/EAC_2024_analisis.ipynb", encoding="utf-8"))
img = nb["cells"][122]["outputs"][0]["data"]["image/png"]   # celda 3.1.3
open("presentacion/figuras/fig-3.1.3-media-vs-mediana.png", "wb").write(base64.b64decode(img))
```

Si se vuelve a ejecutar un cuaderno y cambia una figura, hay que reexportar el PNG y
actualizar la diapositiva que lo usa.

## La diapositiva 9 es evidencia de código

La rúbrica puntúa «muestra correctamente **el código**». La diapositiva 9 reproduce la celda
2.6.1 del cuaderno con su salida real (`Total: 1,145 empresas (11.6 % del dataset)`) y el
cálculo del peso de esos outliers (`0.740`). Si el cuaderno se vuelve a ejecutar y alguna de
esas dos cifras cambia, hay que actualizarla también aquí.

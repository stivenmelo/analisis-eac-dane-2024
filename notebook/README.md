# Cuadernos

Dos cuadernos, en este orden. El primero produce el archivo del que parte el segundo.

| Cuaderno | Qué hace | Celdas |
|---|---|---|
| [`EAC_2024_analisis.ipynb`](EAC_2024_analisis.ipynb) | Etapas 1 y 2 completas, más las figuras de la Etapa 3 | 125 (50 de código) |
| [`EAC_2024_modelo.ipynb`](EAC_2024_modelo.ipynb) | El modelo predictivo de la Etapa 3 | 33 (15 de código) |

## `EAC_2024_analisis.ipynb`

Tiene tabla de contenido enlazada al principio: cada numeral lleva a su apartado.

| Sección | Qué resuelve |
|---|---|
| **1. Módulo 1** | Carga el archivo con los tipos correctos, documenta las 63 variables, diagnostica nueve problemas de calidad y los corrige. Termina guardando `datos/procesados/eac_2024_limpio.csv` |
| **2. Módulo 2** | Tendencia central, dispersión, gráficos, comparación entre grupos y outliers. Termina con la tabla maestra de estadísticos y el veredicto sobre la hipótesis |
| **3. Módulo 3** | Las tres figuras declarativas que cuentan el hallazgo |
| **4. Conclusiones** | Los tres cierres del trabajo |

**La regla que ordena el cuaderno:** en la sección 1 no se calcula ninguna estadística. La 1
limpia y guarda; la 2 abre el archivo limpio y lo analiza. Por eso la sección 2 se puede
ejecutar sola, sin volver a correr todo el Módulo 1.

Cada celda de código empieza con un comentario que lleva el número de su apartado, y cada
apartado termina con un bloque **Resultado** que dice qué cifra debe dar.

## `EAC_2024_modelo.ipynb`

Estima la producción bruta de una empresa a partir de su personal ocupado y su nómina — dos
datos que se observan desde fuera, sin ver los estados financieros.

| Sección | Qué resuelve |
|---|---|
| **1** | Librerías, carga del dataset depurado y **la trampa**: qué variables no pueden ser predictores porque son componentes contables del objetivo |
| **2** | Variables del modelo y partición entrenamiento / prueba (80/20) |
| **3** | Tres modelos: simple log–log, múltiple log–log y el mismo sin logaritmos |
| **4** | Evaluación con métricas comparables, validación cruzada y por qué el R² no es la métrica adecuada aquí |
| **5** | Dispersión con la recta, predicho frente a observado y diagnóstico de residuos |
| **6** | Qué dice el modelo y su aplicación profesional |

**Resultado:** R² de 0,729 y error mediano del 35,5 % sobre 1.959 empresas no vistas.

## Cómo ejecutarlos

```bash
pip install -r ../requirements.txt
jupyter notebook EAC_2024_analisis.ipynb
```

Las rutas funcionan igual ejecutando desde esta carpeta o desde la raíz del repositorio: la
primera celda de 1.1.2 detecta dónde está y ajusta. En Google Colab se abren y se ejecutan en
orden, sin cambios.

> Antes de entregar o de grabar el video conviene un **Kernel → Restart & Run All** del
> cuaderno de análisis, para que la numeración de celdas guardada corresponda a una corrida
> limpia de arriba a abajo.

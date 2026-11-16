# Análisis de la Encuesta Anual de Comercio (EAC) 2024 — DANE

Proyecto final de la asignatura **DataXperience** — Universidad EAN.

Tomé los microdatos de la **Encuesta Anual de Comercio 2024** del DANE —10.238 empresas
comerciales colombianas con 63 variables cada una—, los limpié, los describí con estadística
y entrené un modelo para estimar el tamaño de una empresa sin ver sus estados financieros.

> **El hallazgo:** el sector está muy concentrado. El 1 % de las empresas genera el **38,6 %**
> de las ventas y el 10 % mayor, el **71,9 %** (Gini de 0,791). Por eso la venta *media* del
> sector describe a una empresa que casi no existe: el **84,9 %** vende por debajo de ella.

---

## 1. Qué hay en este repositorio

| Archivo | Qué es |
|---|---|
| [`notebook/EAC_2024_analisis.ipynb`](notebook/EAC_2024_analisis.ipynb) | **El cuaderno principal.** Etapas 1 y 2 completas y las figuras de la Etapa 3. 125 celdas, con tabla de contenido enlazada. |
| [`notebook/EAC_2024_modelo.ipynb`](notebook/EAC_2024_modelo.ipynb) | **El modelo predictivo** de la Etapa 3: regresión log–log, partición train/test, validación cruzada e interpretación. |
| [`datos/crudos/`](datos/crudos/) | Los archivos tal como los publica el DANE, sin tocar, más el diccionario de datos y la ficha metodológica. |
| [`datos/procesados/`](datos/procesados/) | `eac_2024_limpio.csv` (lo que produce la Etapa 1) y `eac_2024_estadisticos_modulo2.csv` (la tabla maestra de la Etapa 2). |
| [`presentacion/`](presentacion/) | `EAC-2024-presentacion.pptx` — 15 diapositivas con notas del orador — y `figuras/` con los PNG que usa. |
| [`video/guion-video.md`](video/guion-video.md) | El guion hablado, con tiempos por diapositiva calculados sobre el conteo real de palabras. |
| [`docs/ficha-metodologica-resumen.md`](docs/ficha-metodologica-resumen.md) | Resumen de la ficha del DANE: qué mide la EAC, a quién deja fuera y qué se puede preguntarle. |
| [`docs/rubrica-proyecto-final.md`](docs/rubrica-proyecto-final.md) | La rúbrica de Canvas y el estado del proyecto frente a cada criterio. |
| [`requirements.txt`](requirements.txt) | pandas, numpy, matplotlib, seaborn, openpyxl, scikit-learn, ipykernel. |

## 2. Los datos

- **Fuente:** DANE — Encuesta Anual de Comercio (EAC), año de referencia **2024**.
  [Portal de la operación](https://www.dane.gov.co/index.php/estadisticas-por-tema/comercio-interno/encuesta-anual-de-comercio-eac)
  · [Microdatos (ANDA)](https://microdatos.dane.gov.co/index.php/catalog/MICRODATOS/about)
- **Unidad de observación:** la empresa comercial (microdato anonimizado).
- **Unidad monetaria:** miles de pesos corrientes.
- **Es un censo, no una muestra.** El DANE mide a todas las empresas que cumplen sus
  criterios, así que los estadísticos de este trabajo son parámetros poblacionales de ese
  universo, no estimaciones con margen de error.

> ⚠️ **El límite del alcance.** Solo entran empresas con 10 o más personas ocupadas **o**
> ventas anuales desde $2.300 millones. Eso deja fuera al comercio pequeño y al informal, que
> es la mayoría de los establecimientos del país. Todas las conclusiones son sobre **el
> comercio formal mediano y grande**, nunca sobre «el comercio colombiano».

## 3. Qué pregunté y qué encontré

| Pregunta | Respuesta | Dónde |
|---|---|---|
| ¿Qué tan concentrado está el sector? | Gini de **0,791**. El 1 % mayor genera el 38,6 % de las ventas; el 10 % mayor, el 71,9 % | cuaderno 2.4.3 |
| ¿Sirve la venta promedio para describir al sector? | No. Media 57.513.659 frente a mediana 13.603.354 miles de pesos, y el 84,9 % vende menos que la media | 2.2.1 y 2.2.2 |
| ¿La concentración es igual en todo el comercio? | No. El coeficiente de variación va de **1,77 a 6,70** entre dominios de actividad | 2.5.1 y 3.1.2 |
| ¿Se paga mejor en las empresas grandes? | Sí, de forma monotónica: la remuneración mediana sube **+38,5 %** del tramo micro al grande | 2.5.2 |
| ¿Qué hacer con los 1.145 atípicos (11,6 %)? | Conservarlos: concentran el **74,0 %** de las ventas. No son ruido, son el objeto de estudio | 2.6 |
| ¿Se puede estimar el tamaño de una empresa sin sus balances? | Sí, con personal y nómina: **R² 0,729** y error mediano del **35,5 %** sobre datos no vistos | cuaderno del modelo |

## 4. Las tres etapas del curso

### Etapa 1 — Módulo 1: Fundamentos y preparación de datos ✅

| # | Tarea | Dónde |
|---|---|---|
| 1 | Seleccionar y **justificar** el conjunto de datos | cuaderno [1.2](notebook/EAC_2024_analisis.ipynb) |
| 2 | Explorar estructura, tipos y variables | 1.3 y 1.4 |
| 3 | **Diagnosticar** problemas de calidad | 1.5 — nueve problemas documentados |
| 4 | Limpiar y transformar | 1.6 y 1.7 |

**Resultado:** de 10.238 × 63 a **9.909 filas × 71 columnas**. Se eliminaron 329 empresas sin
actividad en 2024 (3,2 %) y se conservaron los 185 valores negativos, que son pérdidas reales.

### Etapa 2 — Módulo 2: Análisis estadístico ✅

| # | Tarea | Dónde |
|---|---|---|
| 1 | Medidas de **tendencia central** | 2.2 |
| 2 | Medidas de **dispersión** | 2.3 |
| 3 | **Comparar y contrastar** variables | 2.5 |
| 4 | **Outliers**, relaciones e hipótesis | 2.6 y 2.7 |

**Hipótesis contrastada:** se confirma que el sector está concentrado, y se corrige en un
punto — la concentración **no es uniforme** entre subsectores. La asimetría está en las
magnitudes, no en los ratios.

### Etapa 3 — Módulo 3: Modelado matemático y storytelling ✅

| # | Tarea | Dónde |
|---|---|---|
| 1 | **Visualizaciones** que resuman los hallazgos | cuaderno 3.1.1–3.1.3 y [`presentacion/figuras/`](presentacion/figuras/) |
| 2 | **Narrativa (storytelling)** | [`video/guion-video.md`](video/guion-video.md) y las 15 diapositivas |
| 3 | **Modelo predictivo entrenado y evaluado** | [`notebook/EAC_2024_modelo.ipynb`](notebook/EAC_2024_modelo.ipynb) |
| 4 | **Aplicación profesional concreta** | cuaderno del modelo 6.2 y diapositiva 14 |

**El modelo:** regresión lineal sobre logaritmos que estima la producción bruta a partir del
personal ocupado y la nómina —dos datos que un banco o una entidad pública ya observan por la
planilla de seguridad social—. Evaluado sobre 1.959 empresas que no vio al entrenar.

> **Por qué log–log y no la escala original.** El modelo sin logaritmos da un R² *mejor*
> (0,808 frente a 0,729) y un error mediano casi el doble de malo (62,8 % frente a 35,5 %). En
> un sector con Gini 0,791 el R² mide sobre todo lo bien que se predicen las pocas empresas
> enormes: elegir por R² habría sido elegir mal. Está desarrollado en 4.4 del cuaderno del modelo.

## 5. Cómo ejecutar el análisis

### Opción A — Google Colab
Abrir [`notebook/EAC_2024_analisis.ipynb`](notebook/EAC_2024_analisis.ipynb) en
[Colab](https://colab.research.google.com/) y ejecutar las celdas en orden.

### Opción B — Entorno local
```bash
pip install -r requirements.txt
jupyter notebook notebook/EAC_2024_analisis.ipynb
```

**El orden importa:** el cuaderno de análisis genera `datos/procesados/eac_2024_limpio.csv` en
su apartado 1.7.2, y tanto la sección 2 como el cuaderno del modelo parten de ese archivo. Las
rutas funcionan igual ejecutando desde `notebook/` o desde la raíz del repositorio.

## 6. Integrantes

| Nombre completo | Rol / aporte principal | Correo institucional |
|---|---|---|
| Stiven Melo | Proyecto completo: limpieza, análisis, modelo, presentación y video | |


## 7. Video de presentación

- **Duración:** 2 a 5 minutos (fuera de ese rango no se califica). El guion está cronometrado
  en **4:40**, con 20 segundos de margen.
- **Guion y tiempos:** [`video/guion-video.md`](video/guion-video.md)
- **Ver el video:** https://youtu.be/GgUPByaIKXI

## 8. Estado del proyecto

- [x] **Módulo 1** — Fundamentos y preparación de datos
- [x] **Módulo 2** — Análisis estadístico descriptivo
- [x] **Módulo 3** — Modelado, visualización y storytelling
- [x] Presentación de apoyo (15 diapositivas con notas del orador)
- [x] Guion del video, dentro del límite de duración
- [x] **Video grabado y publicado** — https://youtu.be/GgUPByaIKXI
- [x] Enlace del video en este README (sección 7) y en [`video/README.md`](video/README.md)
- [ ] Repositorio público y enlace pegado en Canvas

### Detalles que faltan en los cuadernos

- Ejecutar el cuaderno completo de arriba a abajo (*Restart & Run All*) antes de entregar: la
  numeración de celdas guardada no corresponde a una corrida limpia.


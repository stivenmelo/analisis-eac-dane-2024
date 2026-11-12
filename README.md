# Análisis de la Encuesta Anual de Comercio (EAC) 2024 — DANE

Proyecto final de la asignatura **DataXperience** — Universidad EAN.
Análisis exploratorio, limpieza y visualización de los microdatos de la **Encuesta Anual de Comercio (EAC)** publicada por el **DANE** (Departamento Administrativo Nacional de Estadística) de Colombia.

---

## 1. Contexto del proyecto

La **Encuesta Anual de Comercio (EAC)** es una operación estadística del DANE que caracteriza al sector comercio en Colombia: ventas, consumo intermedio, personal ocupado, sueldos y salarios, inversión y valor agregado, desagregados por actividad comercial (CIIU Rev. 4 A.C.) y por escala de personal.

Con este conjunto de datos buscamos responder preguntas como:

- ¿Qué actividades comerciales concentran la mayor proporción de las ventas del sector?
- ¿Cómo se relacionan el personal ocupado y la producción bruta entre subsectores?
- ¿Qué diferencias existen en la remuneración promedio según la escala de personal de la empresa?
- ¿Qué tan concentrado está el sector comercio en Colombia?

> **Nota:** completar/ajustar las preguntas de investigación cuando el equipo defina el enfoque final.

## 2. Justificación de la elección del dataset

_(Pendiente de redacción — Módulo 1, punto 2)_

Ideas a desarrollar:
- Relevancia del sector comercio en la economía colombiana y en nuestra formación profesional.
- Datos oficiales, públicos, de libre uso y con documentación metodológica completa.
- Tamaño y riqueza suficientes para aplicar limpieza, transformación y análisis estadístico real.

## 3. Fuente de los datos

- **Entidad:** DANE — Departamento Administrativo Nacional de Estadística
- **Operación:** Encuesta Anual de Comercio (EAC)
- **Año de referencia:** 2024
- **Enlace:** https://www.dane.gov.co/index.php/estadisticas-por-tema/comercio-interno/encuesta-anual-de-comercio-eac
- **Microdatos:** https://microdatos.dane.gov.co/index.php/catalog/MICRODATOS/about
- **Licencia / condiciones de uso:** datos públicos del DANE (ver condiciones en el portal de microdatos)

## 4. Estructura del repositorio

```
EncuestaAnualdeComercio-EAC-2024/
├── README.md               ← contexto, integrantes y enlace al video
├── requirements.txt        ← librerías usadas en el análisis
├── datos/
│   ├── crudos/             ← datos originales descargados del DANE (sin modificar)
│   └── procesados/         ← dataset depurado que produce el notebook
├── notebook/
│   └── EAC_2024_analisis.ipynb   ← cuaderno de Google Colab con todo el código
├── presentacion/           ← presentación de apoyo (PDF o PPTX)
├── video/                  ← video de presentación o enlace al video
└── docs/
    └── capturas/           ← capturas de pantalla usadas como evidencia
```

## 5. Integrantes del equipo

| Nombre completo | Rol / aporte principal | Correo institucional |
|---|---|---|
| Stiven Melo | | |
| _(pendiente)_ | | |
| _(pendiente)_ | | |

## 6. Video de presentación

- **Duración:** entre 2 y 5 minutos
- **Enlace:** _(pendiente — pegar aquí el enlace público al video)_
- **Ubicación en el repositorio:** carpeta [`video/`](video/)

## 7. Etapas del proyecto

El proyecto se construye en **tres etapas**, una por módulo del curso. La entrega es **única y al final**, en este mismo repositorio.

### Etapa 1 — Módulo 1: Fundamentos y preparación de datos ✅

Selección y justificación del dataset, exploración inicial, limpieza y tratamiento de nulos y outliers.

**Completada.**

### Etapa 2 — Módulo 2: Análisis Estadístico

**Objetivo:** aplicar medidas estadísticas descriptivas para comprender el comportamiento de los datos.

| # | Tarea | Estado |
|---|---|---|
| 1 | Calcular e interpretar **medidas de tendencia central** (media, mediana, moda) | ⬜ |
| 2 | Calcular e interpretar **medidas de dispersión** (rango, varianza, desviación estándar) | ⬜ |
| 3 | **Comparar y contrastar variables** usando análisis estadístico básico | ⬜ |
| 4 | Identificar **outliers, relaciones o posibles hipótesis** basadas en los valores | ⬜ |

**Evidencias que debe producir esta etapa:**

- Resultados con **explicaciones breves en lenguaje sencillo** (no solo la salida de `describe()`).
- **Tablas / resúmenes** de estadísticas.
- **Gráficos** que muestren la naturaleza de los datos (histogramas, diagramas de caja).
- **Interpretaciones relevantes para el contexto profesional** del equipo.

**Variables candidatas de la EAC para el análisis:** ventas, consumo intermedio, personal ocupado, sueldos y salarios, inversión y valor agregado — todas numéricas y en escalas muy distintas, lo que hace necesario el **coeficiente de variación** para compararlas entre sí.

> Dos preguntas del contexto que esta etapa puede responder con solo estadística descriptiva:
> - ¿La media de ventas se aleja mucho de la mediana? Si sí, el sector está **concentrado** en pocas empresas grandes (asimetría positiva).
> - ¿Qué subsector tiene mayor **variabilidad relativa** en remuneración? Se responde con el coeficiente de variación, no con la desviación estándar, porque las escalas difieren.

### Etapa 3 — Módulo 3

_(Pendiente — el enunciado aún no ha sido publicado.)_

## 8. Cómo ejecutar el análisis

### Opción A — Google Colab (recomendada)
1. Abrir `notebook/EAC_2024_analisis.ipynb` en [Google Colab](https://colab.research.google.com/).
2. Ejecutar las celdas en orden; la primera celda descarga/carga los datos de `datos/crudos/`.

### Opción B — Entorno local
```bash
pip install -r requirements.txt
jupyter notebook notebook/EAC_2024_analisis.ipynb
```

## 9. Estado del proyecto

### Etapas

- [x] **Módulo 1** — Fundamentos y preparación de datos (selección, exploración, limpieza)
- [ ] **Módulo 2** — Análisis estadístico descriptivo (tendencia central, dispersión, comparación de variables, outliers)
- [ ] **Módulo 3** — _(pendiente de completar con el enunciado)_

### Entregables del repositorio

- [x] `datos/` — datasets utilizados
- [ ] `notebook/EAC_2024_analisis.ipynb` — código del análisis *(creado, en desarrollo)*
- [ ] `presentacion/` — presentación de apoyo (PDF o PPTX)
- [ ] `video/` — video de presentación o enlace
- [ ] `README.md` — contexto ✅, integrantes ⬜, enlace al video ⬜

### Requisitos de entrega

- [ ] Equipo de **2 o 3 personas** (obligatorio)
- [ ] Repositorio **público** y consultable — *verificar antes de entregar*
- [ ] Video de **2 a 5 minutos**, público, explicando las **tres etapas**
      *(fuera de ese rango el video no se califica)*
- [ ] Enlace al repositorio pegado en la actividad **Entrega de Proyecto** de Canvas
      **por cada integrante** (el mismo enlace para todos)

> Únicamente se acepta la entrega por Canvas. No se admiten correo, Teams ni comentarios.
> El único canal para dudas es la mensajería de Canvas.

**Fecha límite de entrega:** 21 de noviembre, 23:59.

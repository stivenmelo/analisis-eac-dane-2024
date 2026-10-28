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

## 7. Cómo ejecutar el análisis

### Opción A — Google Colab (recomendada)
1. Abrir `notebook/EAC_2024_analisis.ipynb` en [Google Colab](https://colab.research.google.com/).
2. Ejecutar las celdas en orden; la primera celda descarga/carga los datos de `datos/crudos/`.

### Opción B — Entorno local
```bash
pip install -r requirements.txt
jupyter notebook notebook/EAC_2024_analisis.ipynb
```

## 8. Estado del proyecto

- [ ] **Módulo 1** — Fundamentos y preparación de datos (selección, exploración, limpieza)
- [ ] **Módulo 2** — _(pendiente de completar con el enunciado)_
- [ ] **Módulo 3** — _(pendiente de completar con el enunciado)_
- [ ] Presentación de apoyo
- [ ] Video (2–5 min)
- [ ] Entrega individual del enlace del repositorio en Canvas

**Fecha límite de entrega:** 21 de noviembre, 23:59.

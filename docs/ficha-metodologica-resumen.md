# Resumen de la Ficha Metodológica — Encuesta Anual de Comercio (EAC)

Resumen de `datos/crudos/EAC_Ficha Metodologica.pdf`
(DANE — DIMPE, código `DSO-EAC-FME-001`, versión 10, octubre 2024).

**Para qué sirve este documento:** entender qué mide la EAC, a quién mide y cómo, para poder
formular hipótesis que los datos puedan efectivamente responder — y no preguntas que el
diseño de la encuesta no permite contestar.

---

## Índice

1. [Qué es la EAC en una frase](#qué-es-la-eac-en-una-frase)
2. [Lo más importante: es un censo, no una muestra](#lo-más-importante-es-un-censo-no-una-muestra)
3. [Quién entra y quién no](#quién-entra-y-quién-no)
4. [Objetivos de la encuesta](#objetivos-de-la-encuesta)
5. [Las variables](#las-variables)
6. [Los indicadores y sus fórmulas](#los-indicadores-y-sus-fórmulas)
7. [Cobertura, periodo y recolección](#cobertura-periodo-y-recolección)
8. [Qué hay realmente en nuestros CSV](#qué-hay-realmente-en-nuestros-csv)
9. [Hipótesis propuesta](#hipótesis-propuesta)
10. [Hipótesis alternativas](#hipótesis-alternativas)
11. [Advertencias para el análisis](#advertencias-para-el-análisis)

---

## Qué es la EAC en una frase

Una operación estadística **anual** del DANE que mide **la estructura y el comportamiento
económico del sector comercio en Colombia** —ventas, costos, personal, remuneración,
inversión y valor agregado— empresa por empresa.

**Historia breve:** nace como complemento del Censo Económico Multisectorial de 1990.
Primera aplicación en 1994 (piloto), primera publicación en 1996, continua desde entonces.
Rediseñada en 2012 y 2013. Desde 2021 incorpora módulos de **gestión ambiental** y, desde
2022, de **Pérdidas y Desperdicios de Alimentos (PDA)**.

---

## Lo más importante: es un censo, no una muestra

> ⚠️ **Este es el dato metodológico que más cambia el análisis, y es fácil pasarlo por alto
> porque la operación se llama "encuesta".**

La ficha marca explícitamente la casilla **Censo**, y en los campos de diseño muestral dice
*"No aplica"*:

| Campo | Valor |
|---|---|
| Tipo de operación | **Censo** |
| Unidad de muestreo | No aplica *(por ser censo)* |
| Tamaño de muestra | No aplica |
| Diseño muestral | No aplica |
| Mantenimiento y rotación de la muestra | No aplica |

### Qué implica para nosotros

- **No hay factores de expansión ni pesos muestrales** que aplicar. Cada fila cuenta como una.
- **No hay error muestral ni intervalos de confianza que calcular** sobre la población
  objetivo: no estamos estimando a partir de una muestra, estamos **describiendo la
  población completa** de empresas que cumplen los parámetros de inclusión.
- Por eso la **estadística descriptiva es exactamente la herramienta correcta** para este
  dataset — que es justo lo que pide la Etapa 2 del proyecto. Las diferencias que
  encontremos entre grupos **son** diferencias reales, no estimaciones con incertidumbre
  de muestreo.

> 💡 **La frase que debe ir en el notebook:** *"Al tratarse de un censo y no de una muestra,
> los estadísticos calculados son parámetros poblacionales del universo de empresas que
> cumplen los parámetros de inclusión, no estimaciones."*

---

## Quién entra y quién no

### Parámetros de inclusión

Entran las empresas formalmente establecidas en Colombia cuya actividad principal es el
comercio y que cumplen **al menos uno** de estos dos criterios:

- **10 o más personas ocupadas**, **o**
- **ingresos por ventas anuales ≥ $2.300 millones** (valor de 2023, **actualizado cada año
  según el IPC**).

### Actividades cubiertas

Sección **G de la CIIU Rev. 4 A.C.** — comercio al por mayor y al por menor y reparación de
vehículos automotores y motocicletas. Divisiones **45, 46 y 47**.

### Exclusiones explícitas

| Se excluye | Matiz |
|---|---|
| Reparación y mantenimiento | Solo si **no** están relacionadas con la actividad comercial |
| Compraventas | — |
| Puestos de chance, loterías y rifas | — |
| Telemercadeo / ventas por catálogo (multinivel) | — |
| Comercio de mercancías usadas | **Excepto** vehículos automotores, si es conexo a la venta de vehículos nuevos |
| Venta en puestos móviles o fuera de establecimiento | — |

> ⚠️ **Sesgo de selección que hay que declarar en el análisis.** La EAC **no cubre el
> comercio pequeño ni el informal**: el umbral de 10 personas o $2.300 millones deja fuera
> a la inmensa mayoría de los establecimientos comerciales del país. Toda conclusión que
> saquemos es sobre **el comercio formal mediano y grande**, nunca sobre "el comercio
> colombiano" en general. Decirlo no debilita el trabajo — omitirlo sí lo invalida.

---

## Objetivos de la encuesta

**General:** conocer la estructura y el comportamiento económico del sector comercio a nivel
nacional para el análisis del sector y la conformación de agregados económicos.

**Específicos** (los que importan para nuestro análisis):

- Cuantificar los principales **agregados macroeconómicos**: producción bruta, consumo
  intermedio, valor agregado, personal ocupado, sueldos y salarios, prestaciones sociales y
  ventas — **por actividad comercial, escala de ventas y escalas de personal**.
- Cuantificar la composición de las personas empleadas **desagregada por sexo**, como soporte
  para indicadores de género.
- Generar estadísticas sobre **comercio electrónico y TIC** en el comercio.
- Generar estadísticas de las variables principales **a nivel departamental**.
- Generar estadísticas de **protección y gestión ambiental** en el sector.
- Medir los **alimentos que dejaron de ser aptos para consumo humano** (módulo PDA, aporta
  al ODS 12.3).

> 💡 **El tercer objetivo específico es un regalo para el proyecto:** el DANE ya declara que
> desagrega por **actividad, escala de ventas y escala de personal**. Esas son nuestras
> variables de agrupación naturales para "comparar y contrastar variables", el punto 3 de la
> Etapa 2.

---

## Las variables

### Variables de clasificación (categóricas, para agrupar)

Actividad **CIIU Rev. 4 A.C.**, **escalas de personal**, **escalas de ventas**,
**departamentos**, **organización jurídica**, tipo de establecimiento, tipo de unidad de
apoyo, ubicación, tamaño de empresa; y las del módulo ambiental (fuente de agua, destino y
tipo de residuos, fuente y planta de energía).

### Variables de estudio (las que se miden directamente)

Ingresos por ventas · gastos de personal (sueldos y prestaciones) · costos de la mercancía
vendida · gastos de operación · personal ocupado · inventarios · movimientos de activos
fijos · bienes TIC · uso de internet · ventas y compras por comercio electrónico ·
teletrabajo · capital y gasto en protección ambiental · consumo de agua y energía.

### Variables calculadas (las derivadas por el DANE)

**Producción bruta · consumo intermedio · valor agregado · remuneración · predominio por
sexo · relación costo-ventas · coeficiente técnico · excedente bruto de explotación.**

---

## Los indicadores y sus fórmulas

Vienen textuales de la ficha. Son importantes porque **explican la relación entre columnas
de nuestro CSV** y permiten validar los datos:

| Indicador | Fórmula |
|---|---|
| **Producción bruta** | Ingresos por ventas − costo de la mercancía vendida − costos de insumos y materiales para servicios de instalación/reparación/mantenimiento |
| **Consumo intermedio** | Suma de gastos en empaques, honorarios, arrendamiento, seguros, aseo y vigilancia, energía y gas, comunicaciones, otros servicios públicos, transporte y fletes, publicidad, mantenimiento, adecuaciones, outsourcing y personal suministrado por terceros |
| **Total sueldos y salarios** | Sueldos del personal permanente + **70 % del salario integral** + sueldos del personal temporal directo + apoyo de sostenimiento a aprendices |
| **Total prestaciones sociales** | Prestaciones del personal permanente + **30 % del salario integral** + prestaciones del temporal directo + cotizaciones patronales + aportes sobre nómina |
| **Personal total** | Propietarios, socios y familiares sin remuneración + permanente + temporal directo + temporal por agencia + aprendices |
| **Total remuneración** | Sueldos y salarios + prestaciones sociales |
| **Coeficiente técnico** | Consumo intermedio / producción bruta |
| **Relación costo-ventas** | Costo / ventas |
| **% mujeres en el empleo** | (Mujeres empleadas en la actividad *i* / total de personas en la actividad *i*) × 100 |

### Predominio por sexo

| % de mujeres empleadas | Clasificación |
|---|---|
| 0 % – 40 % | **Predominio hombres** |
| 41 % – 59 % | **Sin claro predominio por sexo** |
| 60 % – 100 % | **Predominio mujeres** |

> 💡 Esta tabla es una **variable categórica ya definida por el DANE** que podemos
> reconstruir desde `TOTMUJ` y `TOTHOM`. Es un eje de agrupación listo para usar, con corte
> oficial, sin tener que inventar umbrales.

---

## Cobertura, periodo y recolección

| Aspecto | Detalle |
|---|---|
| **Cobertura geográfica** | Territorio nacional |
| **Desagregación geográfica** | Total nacional + **9 dominios departamentales** (Bogotá, Antioquia, Valle del Cauca, Cundinamarca, Atlántico, Santander, Bolívar, Risaralda, Tolima) + dominio **"Otros departamentos"** |
| **Periodo de referencia** | Año calendario, 1 de enero a 31 de diciembre |
| **Periodicidad** | Anual |
| **Periodo de recolección** | 4 meses y medio del año siguiente al de referencia |
| **Método** | Formulario web de autodiligenciamiento (con opción Excel) |
| **Marco estadístico** | Directorio Estadístico de Empresas (DEST) del DANE, verificado contra el RUES y consultas directas |
| **Tasa óptima de imputación** | **No debe superar el 2 %** |
| **Microdatos anonimizados** | Disponibles desde 2003 en el ANDA del DANE |
| **Estándares** | CIIU Rev. 4 A.C. (actividades), CPC 2.1 A.C. (productos PDA), DIVIPOLA (geografía) |

> 💡 **Los 9 dominios departamentales explican la forma del archivo departamental.** El DANE
> solo garantiza representatividad para esos nueve más "Otros departamentos" — no para los
> 32 departamentos uno por uno. Si agrupamos por `DEPTO`, hay que respetar ese límite.

> 💡 **La tasa de imputación ≤ 2 %** es la garantía de calidad del propio DANE: menos del 2 %
> de los datos publicados son imputados. Es un argumento directo para la *Justificación de
> la elección del dataset* del README.

---

## Qué hay realmente en nuestros CSV

Verificado sobre los archivos de `datos/crudos/`:

| Archivo | Filas | Columnas | Separador | Decimal |
|---|---|---|---|---|
| `EAC_CIFRAS_2024_ANONIMIZADA_FINAL.csv` | **10.238** | **63** | `;` | coma |
| `EAC_CIFRAS_2024_ANONIMIZADA_DEP_FINAL.csv` | **14.995** | **5** | `;` | coma |

```python
import pandas as pd
df = pd.read_csv("datos/crudos/EAC_CIFRAS_2024_ANONIMIZADA_FINAL.csv",
                 sep=";", decimal=",", encoding="utf-8-sig")
```

> ⚠️ **Sin `sep=";"` y `decimal=","` pandas lee una sola columna de texto.** Es el primer
> tropiezo garantizado del notebook.

### Columnas clave del archivo nacional

| Columna | Qué es |
|---|---|
| `V1` | Identificador anonimizado de la empresa |
| `CORRELA_16` | Actividad CIIU agrupada en **16 categorías** |
| `CORRE_9` | Actividad CIIU agrupada en **9 categorías** |
| `IDOJ1` | **Organización jurídica** (13 valores) |
| `IDAIO` | **Año de inicio de operaciones** (93 valores) |
| `VENTA` | Ingresos por ventas |
| `TOTPERSO` | Personal total ocupado |
| `BRUTA` · `CONSUI` · `AGREGA` | Producción bruta, consumo intermedio, valor agregado |
| `SUELDOS` · `PRESTAC` · `TOTREM` | Sueldos, prestaciones, remuneración total |
| `TOTMUJ` · `TOTHOM` | Personal total por sexo |
| `CTO` · `INVINI` · `INVFIN` · `ROTACION` | Costo de mercancía e inventarios |

*(El archivo departamental solo trae `V1`, `DEPTO`, `CORRELA_9`, `VENTA` y `Personal`.)*

### Estadísticos descriptivos reales (archivo nacional, datos crudos)

Valores monetarios en **miles de pesos**:

| Variable | Media | Mediana | Desv. est. | CV | Media/Mediana |
|---|---|---|---|---|---|
| `VENTA` | 55.665.447 | 12.960.904 | 307.739.398 | **5,53** | **4,3×** |
| `BRUTA` | 11.856.158 | 2.629.690 | 58.967.485 | **4,97** | **4,5×** |
| `AGREGA` | 7.528.522 | 1.769.133 | 34.455.610 | **4,58** | **4,3×** |
| `TOTREM` | 3.232.989 | 820.664 | 16.264.161 | **5,03** | **3,9×** |
| `TOTPERSO` | 73,0 | 24,0 | 398,6 | **5,46** | **3,0×** |

> 📊 **Todas las variables tienen media muy superior a la mediana**, con coeficientes de
> variación entre 4,6 y 5,5. Según la tabla de las notas del Módulo 2 (Pág. 08), eso es
> **asimetría positiva fuerte y uniforme** en todo el dataset. No es un artefacto de una
> columna: es la forma del sector.

---

## Hipótesis propuesta

> ### El sector comercio formal colombiano está fuertemente concentrado: una minoría de empresas grandes genera la mayor parte de las ventas y del valor agregado, y esa concentración se refleja en una asimetría positiva marcada en todas las variables económicas de la EAC.

### Por qué esta hipótesis y no otra

1. **Se puede responder con estadística descriptiva pura** — exactamente lo que pide la
   Etapa 2 del proyecto. No necesita inferencia, modelos ni datos externos.
2. **Aprovecha que es un censo:** al no ser una muestra, la concentración que midamos es la
   concentración real, no una estimación.
3. **Usa las cinco medidas del módulo a la vez** (media, mediana, moda, desviación estándar,
   rango), que es literalmente el diagnóstico de las notas del Módulo 2 (Pág. 08).
4. **Responde la pregunta de investigación nº 4** que ya está en el README del proyecto:
   *"¿Qué tan concentrado está el sector comercio en Colombia?"*.

### Evidencia preliminar que ya la respalda

Calculada sobre `VENTA` del archivo nacional:

| Grupo | Empresas | % de las ventas totales |
|---|---|---|
| **Top 1 %** | 102 | **39,0 %** |
| **Top 5 %** | 511 | **62,0 %** |
| **Top 10 %** | 1.023 | **72,4 %** |
| **Top 20 %** | 2.047 | **82,7 %** |

> 📊 **102 empresas de 10.238 concentran el 39 % de las ventas del sector.** Y el 80 % de las
> empresas se reparte apenas el 17 % restante. La hipótesis no solo es plausible: la
> evidencia preliminar es contundente.

### Cómo contrastarla, punto por punto, con la Etapa 2

| Tarea de la Etapa 2 | Cómo la cumple esta hipótesis |
|---|---|
| **1. Tendencia central** | Media vs. mediana de `VENTA`, `AGREGA`, `TOTPERSO`. La razón media/mediana de **4,3×** es la medida directa de la concentración |
| **2. Dispersión** | Rango, varianza y desviación estándar de las mismas variables. El **CV de 5,53** permite comparar la variabilidad entre columnas con unidades distintas |
| **3. Comparar y contrastar** | Repetir el diagnóstico **por actividad (`CORRE_9`)**, **por escala de personal** y **por departamento**. ¿Hay subsectores más concentrados que otros? |
| **4. Outliers e hipótesis** | Aplicar la regla **1,5 × IQR** sobre `VENTA`. Los outliers superiores **no son errores** — son las grandes superficies y mayoristas. Decidir **conservarlos** es, en sí mismo, un hallazgo argumentado |

> ⚠️ **El punto 4 es donde esta hipótesis se vuelve interesante como ejercicio.** La regla del
> IQR va a marcar cientos de empresas como atípicas. Eliminarlas sería destruir justamente el
> fenómeno que estudiamos. Es el caso de "valor genuino pero excepcional" de
> las notas del Módulo 2 (Pág. 05), y justifica por escrito la decisión de **conservar y usar medidas
> robustas** (mediana, IQR) en lugar de recortar.

### Interpretación profesional (la cuarta evidencia exigida)

Si la hipótesis se confirma, las implicaciones son concretas:

- **Para el análisis económico:** reportar la *venta promedio* del sector es engañoso —
  describe a una empresa que casi no existe. La mediana es la cifra representativa.
- **Para políticas públicas:** un sector concentrado es más vulnerable a la salida de pocos
  actores, y las medidas de apoyo al comercio deberían segmentarse por escala.
- **Para quien trabaja con estos datos:** cualquier modelo que asuma normalidad sobre estas
  variables está mal especificado. Hace falta **transformación logarítmica** o métodos
  robustos — el puente directo con la Pág. 06 y
  la Pág. 07.

---

## Hipótesis alternativas

Por si el equipo prefiere otro enfoque. Las tres son contrastables con estadística
descriptiva y con las columnas que ya tenemos.

### B. Gradiente de remuneración por tamaño de empresa

> **A mayor escala de personal, mayor remuneración anual por trabajador.**

Evidencia preliminar (`TOTREM / TOTPERSO`, en miles de COP al año):

| Escala de personal | Empresas | Mediana | Media |
|---|---|---|---|
| 0–19 | 4.027 | 30.540 | 42.136 |
| 20–49 | 3.124 | 32.553 | 42.205 |
| 50–99 | 1.397 | 34.317 | 45.144 |
| 100–199 | 741 | 35.013 | 47.699 |
| **200+** | 532 | **39.274** | **50.760** |

> 📊 **El gradiente es monotónico y limpio:** la mediana sube en cada escalón, con un
> **+28,6 %** entre la escala más pequeña y la más grande. Responde la pregunta nº 3 del
> README y conecta con el objetivo específico del DANE de desagregar por escala de personal.

### C. Brecha de género en el empleo comercial

> **La participación de mujeres en el empleo varía sistemáticamente entre actividades
> comerciales.**

Usa `TOTMUJ`, `TOTHOM` y la clasificación oficial de **predominio por sexo** del DANE (los
cortes 40 % / 59 % de la tabla de arriba). Ventaja: el umbral no lo inventamos nosotros, lo
define la ficha metodológica, y el DANE declara este cruce como objetivo específico de la
operación.

### D. Eficiencia operativa por subsector

> **El coeficiente técnico (consumo intermedio / producción bruta) difiere entre comercio
> mayorista, minorista y de vehículos.**

Usa `CONSUI` y `BRUTA`, ya presentes en el CSV, agrupando por `CORRE_9`. Ventaja: es un
**ratio**, así que es comparable entre empresas de tamaños muy distintos — esquiva el
problema de escala que afecta a las demás variables.

---

## Advertencias para el análisis

### 1. Hay 329 filas completamente en cero

**329 registros** tienen simultáneamente `VENTA = 0`, `TOTPERSO = 0` y `BRUTA = 0`. Son el
**3,2 %** del archivo. Casi con seguridad son empresas en el directorio sin actividad
reportada en el periodo.

```python
inactivas = (df["VENTA"] == 0) & (df["TOTPERSO"] == 0)
df_activas = df[~inactivas]        # 9.909 filas
```

> ⚠️ **Decidir qué hacer con ellas antes de calcular nada.** Si se dejan, arrastran todas las
> medias hacia abajo y meten un pico espurio en la moda en 0. Si se quitan, hay que decirlo y
> justificarlo. **Es el primer hallazgo de limpieza del notebook** y encaja directo en la
> Etapa 1.

### 2. Hay valores negativos legítimos

| Columna | Negativos |
|---|---|
| `AGREGA` (valor agregado) | **151** (mínimo: −93.345.113) |
| `BRUTA` (producción bruta) | **34** (mínimo: −7.456.228) |

> ⚠️ **No son errores.** Por la fórmula de la ficha, la producción bruta es *ventas − costo de
> mercancía*: una empresa que vendió por debajo del costo da negativo. Es un resultado
> económico real (liquidación de inventario, pérdidas). **No filtrar por `> 0` sin pensarlo.**

### 3. Los valores monetarios están en miles de pesos

Lo que se lee como `12.994.085` son ~**$13.000 millones** de pesos. Hay que rotularlo en todos
los ejes y tablas, o las cifras no significan nada para quien lea el informe.

### 4. El archivo departamental tiene más filas que el nacional

14.995 vs. 10.238. No es un error: el archivo nacional es **una fila por empresa**, mientras
que el departamental desagrega **una fila por empresa y departamento** (una empresa con
operaciones en tres departamentos aparece tres veces).

> ⚠️ **Nunca cruzar los dos archivos por `V1` sin agregar primero**, o se duplican las ventas
> de las empresas multidepartamentales.

### 5. El universo no es "el comercio colombiano"

Ya dicho arriba, pero se repite porque es la limitación que un evaluador va a buscar: el
umbral de inclusión (10 personas o $2.300 millones) deja fuera al comercio pequeño y al
informal. **Declararlo explícitamente en el README y en el video.**

---

## Fuentes

- DANE – DIMPE. *Ficha Metodológica — Encuesta Anual de Comercio (EAC)*, código
  `DSO-EAC-FME-001`, versión 10, NTC PE 1000:2020, octubre 2024.
  Archivo local: `datos/crudos/EAC_Ficha Metodologica.pdf`
- Portal EAC: https://www.dane.gov.co/index.php/estadisticas-por-tema/comercio-interno/encuesta-anual-de-comercio-eac
- Microdatos (ANDA): https://microdatos.dane.gov.co/index.php/catalog/MICRODATOS/about

*Los estadísticos descriptivos de este documento se calcularon directamente sobre
`datos/crudos/EAC_CIFRAS_2024_ANONIMIZADA_FINAL.csv` (datos crudos, sin limpiar).*

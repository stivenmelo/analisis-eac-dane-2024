# Guion del video — EAC 2024

Proyecto **DataXperience** · Universidad EAN · Análisis de la Encuesta Anual de Comercio
(EAC) 2024 del DANE.

| | |
|---|---|
| **Presenta** | Stiven Melo (presentador único) |
| **Duración hablada** | **≈ 4:40** (el rango permitido es 2–5 min; fuera de ahí no se califica) |
| **Diapositivas** | 15, en `presentacion/EAC-2024-presentacion.pptx` |
| **Palabras habladas** | **658 palabras**, a 145 palabras por minuto — lectura natural, sin prisa |
| **Formato** | pantalla compartida con la presentación + cámara |

> ⏱️ **Los tiempos de la tabla salen del conteo real de palabras de cada bloque**, a 145
> palabras por minuto, que es un ritmo de lectura tranquilo. Si hablas más rápido sobra
> margen; si hablas más lento, el margen hasta los 5:00 absorbe la diferencia.

> ⚠️ **El enunciado pide equipo de 2 o 3 personas y que el video lo presente el equipo.**
> Este guion está escrito para una sola voz porque así está el proyecto hoy, pero el
> requisito sigue ahí y no se resuelve con el guion. Si no hay forma de sumar a alguien,
> vale la pena preguntarlo por la mensajería de Canvas **antes** de grabar — es el único
> canal admitido para dudas.

---

## Tabla de tiempos

| # | Diapositiva | Entra | Dura |
|---|---|---|---|
| 1 | Portada | 0:00 | 0:14 |
| 2 | El dataset y por qué lo elegí | 0:14 | 0:25 |
| 3 | Separador Etapa 1 | 0:39 | 0:04 |
| 4 | Etapa 1 · Lo que encontré al abrir el archivo | 0:43 | 0:28 |
| 5 | Separador Etapa 2 | 1:11 | 0:04 |
| 6 | Etapa 2 · La media describe a una empresa que casi no existe | 1:15 | 0:20 |
| 7 | Etapa 2 · Cuánta concentración hay | 1:35 | 0:22 |
| 8 | Etapa 2 · Los atípicos no son ruido, son el sector | 1:57 | 0:29 |
| 9 | Etapa 2 · Así se ve esa decisión en el código | 2:26 | 0:16 |
| 10 | Etapa 2 · La hipótesis se confirma y se corrige | 2:42 | 0:15 |
| 11 | Separador Etapa 3 | 2:57 | 0:04 |
| 12 | Etapa 3 · El modelo predictivo | 3:01 | 0:36 |
| 13 | Etapa 3 · La métrica que decide no es el R² | 3:37 | 0:15 |
| 14 | Aplicación profesional | 3:52 | 0:26 |
| 15 | Cierre | 4:18 | 0:22 |
| | **Total hablado** | | **4:40** |

> **Margen: 20 segundos** hasta el límite de 5:00, a 145 palabras por minuto. Si al
> cronometrar te pasas, el recorte menos doloroso es el **bloque 13 completo** (−15 s): lo
> que dice ya está escrito en su diapositiva. El segundo recorte sería la última frase del
> bloque 12 (−8 s).

---

## Guion

### 1 · Portada

**En pantalla:** portada con el título, el nombre y la asignatura.

> Hola, soy Stiven Melo y este es mi proyecto de DataXperience. Analicé la Encuesta Anual de
> Comercio 2024 del DANE: casi diez mil empresas comerciales colombianas, con sesenta y tres
> variables cada una.
---

### 2 · El dataset y por qué lo elegí

**En pantalla:** las cuatro tarjetas de cifras (10.238 empresas · 63 variables · censo ·
miles de pesos) y la nota de alcance.

> Elegí la EAC por una razón que lo cambia todo: no es una muestra, es un censo. Así que estos
> números no son estimaciones con margen de error: son el dato real.
>
> Eso sí: solo entran empresas de diez o más personas, o con ventas sobre dos mil trescientos
> millones. Es el comercio formal mediano y grande, no el comercio colombiano.
---

### 3 · Separador Etapa 1

**En pantalla:** separador oscuro, «Etapa 1 — Fundamentos y preparación de datos».

> Primera etapa: preparar los datos.
---

### 4 · Etapa 1 · Lo que encontré al abrir el archivo

**En pantalla:** la tabla de problemas detectados y las cifras del antes y el después.

> El archivo no se deja leer de entrada; eso se arregla al cargarlo. Lo interesante vino
> después: nueve problemas.
>
> Trescientas veintinueve empresas tenían todo en cero: no operaron en 2024 y arrastrarían los
> promedios. Las eliminé. Los valores negativos, en cambio, eran reales —empresas que
> vendieron por debajo del costo— y los conservé.
>
> Pasé de diez mil doscientas treinta y ocho empresas a nueve mil novecientas nueve.
---

### 5 · Separador Etapa 2

**En pantalla:** separador oscuro, «Etapa 2 — Análisis estadístico».

> Segunda etapa: medir.
---

### 6 · Etapa 2 · La media describe a una empresa que casi no existe

**En pantalla:** histograma de ventas con la mediana y la media marcadas
(`fig-3.1.3-media-vs-mediana.png`).

> Mi hipótesis: el sector está concentrado. La venta media es de cincuenta y siete mil
> quinientos millones de pesos; la mediana, trece mil seiscientos. El ochenta y cinco por
> ciento de las empresas vende menos que la media: ese promedio describe a una empresa que
> casi no existe.
---

### 7 · Etapa 2 · Cuánta concentración hay

**En pantalla:** curva de Lorenz (`fig-2.4.3-lorenz-gini.png`) y las tres cifras de Gini.

> Le puse número con la curva de Lorenz: cuanto más se hunde, más concentrado está el sector.
> El Gini de las ventas es cero coma setenta y nueve: el uno por ciento mayor genera el
> treinta y ocho por ciento de las ventas, y el diez por ciento mayor, el setenta y dos.
---

### 8 · Etapa 2 · Los atípicos no son ruido, son el sector

**En pantalla:** comparación con y sin outliers (`fig-2.6.3-outliers.png`).

> Aquí llegó la decisión más interesante. La regla del rango intercuartílico marca como
> atípicas a mil ciento cuarenta y cinco empresas, el once coma seis por ciento. Antes de
> borrarlas miré cuánto pesan: concentran el setenta y cuatro por ciento de las ventas.
>
> Borrar «el doce por ciento de las filas» suena asumible; borrar tres cuartas partes del
> sector, no. Las conservé, y cambié de herramienta: mediana y escala logarítmica.
---

### 9 · Etapa 2 · Así se ve esa decisión en el código

**En pantalla:** diapositiva con la celda 2.6.1 del cuaderno y su salida real.

> Y así se ve en el cuaderno: cinco líneas calculan el rango intercuartílico y marcan esas mil
> ciento cuarenta y cinco empresas, y una más mide cuánto pesan. Cada decisión está en su
> celda, con su resultado al lado.
---

### 10 · Etapa 2 · La hipótesis se confirma y se corrige

**En pantalla:** coeficiente de variación por dominio (`fig-3.1.2-cv-dominio.png`) y el
veredicto en tres líneas.

> La hipótesis se confirma, pero se cae en un punto, y ese punto es el hallazgo: suponía que
> la concentración era igual en todo el comercio, y no lo es. Varía casi cuatro veces entre
> dominios.
---

### 11 · Separador Etapa 3

**En pantalla:** separador oscuro, «Etapa 3 — Modelado matemático y storytelling».

> Tercera etapa: modelar.
---

### 12 · Etapa 3 · El modelo predictivo

**En pantalla:** predicho frente a observado (`fig-m5.2-predicho-observado.png`) y las
métricas.

> ¿Se puede estimar el tamaño de una empresa sin ver sus balances? Entrené una regresión que
> estima la producción bruta con dos datos observables desde fuera: cuánta gente emplea y
> cuánto les paga, en escala logarítmica.
>
> Sobre el veinte por ciento que nunca vio: R² de cero coma setenta y tres y error mediano del
> treinta y cinco por ciento. Y la nómina pesa cinco veces más que el número de empleados:
> cuánto paga una empresa dice más de su tamaño que a cuánta gente emplea.
---

### 13 · Etapa 3 · La métrica que decide no es el R²

**En pantalla:** tabla comparando el modelo lineal y el logarítmico.

> Una advertencia que vale más que el modelo: sin logaritmos el R² sube, pero el error mediano
> casi se duplica. El R² premia acertarle a las pocas empresas enormes. Elegir por R² habría
> sido elegir mal.
---

### 14 · Aplicación profesional

**En pantalla:** los tres usos y el recuadro de «para qué no sirve».

> ¿Para qué sirve? El personal y la nómina ya los observan un banco o una secretaría de
> desarrollo económico, por la planilla de seguridad social. Con esos dos datos se puede
> dimensionar un cliente antes de pedirle balances, o estimar un segmento sin esperar al DANE.
>
> Y para qué no sirve: con ese error no se decide un crédito. Sirve para segmentar y
> priorizar.
---

### 15 · Cierre

**En pantalla:** las tres conclusiones y el enlace al repositorio.

> Tres cosas me llevo: mirar la forma de la distribución antes que su centro; sospechar de
> toda media que no venga con su mediana; y entender que decidir qué hacer con los atípicos es
> de contenido, no de limpieza.
>
> Todo el código, los datos y esta presentación están en el repositorio. Gracias por verme.
---

## Antes de grabar

- [ ] **Ejecutar el cuaderno de arriba a abajo** (*Kernel → Restart & Run All*) antes de
      capturar la pantalla del bloque 9: la diapositiva muestra código real y su salida.
- [ ] Ensayar una vez con cronómetro. El rango **2:00–5:00** es eliminatorio.
- [ ] Grabar con la presentación a pantalla completa y la cámara visible al menos en la
      portada y el cierre: el enunciado pide que el video lo presente quien hizo el trabajo.
- [ ] Al subirlo (YouTube como «no listado» o Drive), **verificar el enlace desde una
      ventana de incógnito**. Si pide permiso, no está público.
- [ ] Pegar el enlace en `README.md` (sección 6) y en `video/README.md`.
- [ ] Entregar el enlace del repositorio en la actividad de Canvas.
- [ ] Completar la tabla de integrantes del `README.md` (sección 5).

## Cómo se pronuncian las cifras

Para que la narración fluya, el guion dice los números en palabras. Equivalencias por si
prefieres leerlas de la diapositiva:

| En pantalla | Se dice |
|---|---|
| 57.513.659 miles de $ | «cincuenta y siete mil quinientos millones de pesos» |
| 13.603.354 miles de $ | «trece mil seiscientos millones» |
| Gini 0,791 | «cero coma setenta y nueve» |
| R² 0,729 | «cero coma setenta y tres» |
| 35,5 % | «treinta y cinco por ciento» |
| 0,740 | «cero coma setenta y cuatro» |

> Las cifras monetarias de la EAC están en **miles de pesos**. Decirlo una vez (bloque 2) y
> después hablar en millones evita repetir la aclaración en cada cifra.

## De dónde sale cada cifra del guion

| Cifra | Celda del cuaderno |
|---|---|
| 10.238 × 63 → 9.909 × 71 | `EAC_2024_analisis.ipynb` 1.7.1 |
| 329 registros sin actividad | 1.5.3 / 1.6.2 |
| 185 valores negativos (151 + 34) | 1.5.4 |
| Media 57.513.659 · mediana 13.603.354 · 84,9 % | 2.2.1 y 2.2.2 |
| Gini 0,791 · 1 % → 38,6 % · 10 % → 71,9 % | 2.4.3 |
| 1.145 outliers = 11,6 % = 74,0 % de las ventas | 2.6.1 y 2.6.2 |
| **Código en pantalla del bloque 9** | **2.6.1 y 2.6.2** |
| CV por dominio de 1,77 a 6,70 | 2.5.1 y 3.1.2 |
| R² 0,729 · error mediano 35,5 % · elasticidades 0,16 y 0,81 | `EAC_2024_modelo.ipynb` 3.2 y 4.2 |
| Modelo lineal: R² 0,808 · error mediano 62,8 % | 4.2 |

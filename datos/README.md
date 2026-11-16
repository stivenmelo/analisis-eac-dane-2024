# Datos

Todo lo que entra y sale del análisis. Los valores monetarios están en **miles de pesos
corrientes**: lo que se lee como `12.994.085` son unos $13.000 millones.

## `crudos/` — como los publica el DANE

No se modifican nunca. Son la fuente de verdad y permiten reproducir el análisis desde cero.

| Archivo | Qué es | Filas × columnas |
|---|---|---|
| `EAC_CIFRAS_2024_ANONIMIZADA_FINAL.csv` | Microdato nacional: una fila por empresa | 10.238 × 63 |
| `EAC_CIFRAS_2024_ANONIMIZADA_DEP_FINAL.csv` | Microdato departamental: una fila por empresa y departamento | 14.995 × 5 |
| `EAC_Diccionario de datos_Nacional_2024.xlsx` | Diccionario oficial: descripción de cada variable, códigos CIIU y organización jurídica | — |
| `EAC_Diccionario de datos_Departamentos_2024.xlsx` | Diccionario del archivo departamental | — |
| `EAC_Ficha Metodologica.pdf` | Ficha metodológica del DANE (resumida en [`../docs/ficha-metodologica-resumen.md`](../docs/ficha-metodologica-resumen.md)) | — |

**Fuente:** DANE — Encuesta Anual de Comercio, año de referencia 2024.
Descargados de [microdatos.dane.gov.co](https://microdatos.dane.gov.co/index.php/catalog/MICRODATOS/about)
en octubre de 2025.

**Formato que hay que conocer antes de leerlos:** separador `;`, coma decimal y codificación
`utf-8-sig`. Sin esos tres ajustes, pandas lee una sola columna de texto — es el tropiezo que
el cuaderno provoca a propósito en 1.3.1 y resuelve en 1.3.2.

> ⚠️ **Los dos archivos no se pueden cruzar.** Al anonimizar, el DANE numeró el `V1` de cada
> archivo por separado, así que el mismo identificador no se refiere a la misma empresa.
> Comprobado en 1.5.8 del cuaderno; por eso no hay análisis por departamento.

## `procesados/` — lo que genera el cuaderno

| Archivo | Lo genera | Qué contiene |
|---|---|---|
| `eac_2024_limpio.csv` | apartado 1.7.2 | El dataset depurado: **9.909 filas × 71 columnas**. Es el punto de partida de la Etapa 2 y del cuaderno del modelo |
| `eac_2024_estadisticos_modulo2.csv` | apartado 2.7.1 | Tabla maestra de estadísticos descriptivos de las ocho variables analizadas |

**Qué cambió frente al crudo:** se eliminaron 329 empresas sin actividad en 2024 (3,2 %), se
normalizaron los códigos CIIU, se añadieron etiquetas legibles y 8 variables derivadas. El
detalle, decisión por decisión, está en el apartado 1.6 del cuaderno.

## Diccionario de variables del dataset depurado

Las 71 columnas de `eac_2024_limpio.csv`. La columna **Original DANE** es el nombre en el
archivo crudo; `—` significa que la variable no existe en el crudo y la construye el cuaderno.
Las descripciones vienen del diccionario oficial del DANE.

| Variable | Original DANE | Tipo | Nulos | Descripción |
|---|---|---|---|---|
| `empresa_id` | `V1` | entero | 0 | Consecutivo de identificación de la empresa |
| `actividad_16_cod` | `CORRELA_16` | texto | 0 | Correlativa a nivel de 16 dominios de estudio según la CIIU Rev 4. A.C. Se agrega a 16 dominios por temas de reserva estadística - Ver hoja "Correlativa CIIU" |
| `actividad_9_cod` | `CORRE_9` | texto | 0 | Correlativa a nivel de 9 dominios de estudio según la CIIU Rev 4. A.C. Se agrega a 9 dominios para dar trazabilidad frente a los mismos nueve dominios departamentales - Ver hoja "Correlativa CIIU" |
| `org_juridica_cod` | `IDOJ1` | entero | 0 | Tipo de organización jurídica - Ver hoja "Organ_Jurídica" |
| `anio_inicio` | `IDAIO` | entero | 0 | Año de inicio operaciones |
| `pct_insumos_reparacion` | `CIMREP` | decimal | 0 | Costo de insumos en los servicios de instalacion, reparación y mantenimiento respecto a los ingresos por ventas. (miles de pesos) |
| `produccion_bruta` | `BRUTA` | decimal | 0 | Producción Bruta. Corresponde a las ventas menos el costo de la mercancía y de insumos utilizados para prestar servicios de mantenimiento. (miles de pesos) |
| `consumo_intermedio` | `CONSUI` | decimal | 0 | Consumo Intermedio: gasto en empaques, honorarios, arrendamiento y gastos por activos adquiridos por derechos de uso, seguros, aseo y vigilancia, energía electríca, comunicaciones, otros servicios publicos, transporte, fletes y acarreos, propaganda y publicidad, mantenimiento, reparaciones y adecuaciones, gasto en personal suministrado a través de empresas esepcializadas en el suministro del personal, otros gastos inherentes a la actividad económica. (miles de pesos) |
| `gasto_gas_natural` | `GAS` | decimal | 0 | Gasto en gas natural (miles de pesos) |
| `gasto_empaques` | `EMPAQUE` | decimal | 0 | Gasto en Empaques y embalajes (miles de pesos) |
| `gasto_honorarios` | `HONORA` | decimal | 0 | Gasto en Honorarios y servicios técnicos (miles de pesos) |
| `gasto_comisiones` | `COMISION` | decimal | 0 | Gastos de ventas por comisión a terceros (miles de pesos) |
| `gasto_arriendos` | `ARRIENDO` | decimal | 0 | Gasto en Arrendamiento de bienes inmuebles y muebles (miles de pesos) |
| `gasto_seguros` | `SEGURO` | decimal | 0 | Gasto en Seguros,excepto los de prestaciones (miles de pesos) |
| `gasto_aseo_vigilancia` | `ASEO` | decimal | 0 | Gasto en Aseo y vigilancia (miles de pesos) |
| `gasto_energia` | `ENERGIA` | decimal | 0 | Gasto en Energía eléctrica comprada (miles de pesos) |
| `gasto_comunicaciones` | `COMUNICA` | decimal | 0 | Gasto en Comunicaciones (miles de pesos) |
| `gasto_servicios_publicos` | `PUBLICO` | decimal | 0 | Gasto en Otros servicios públicos (miles de pesos) |
| `gasto_transporte` | `FLETES` | decimal | 0 | Gasto en Transporte, fletes y acarreos (miles de pesos) |
| `gasto_publicidad` | `PUBLICI` | decimal | 0 | Gasto en Propaganda y publicidad (miles de pesos) |
| `gasto_mantenimiento` | `ADECUA` | decimal | 0 | Gasto en Mantenimiento, reparaciones (miles de pesos) |
| `gasto_regalias` | `REGALA` | decimal | 0 | Regalías causadas (miles de pesos) |
| `gasto_outsourcing` | `OUTSOURCING` | decimal | 0 | Costos y gastos por servicios contratados con terceros (outsoursing) (miles de pesos) |
| `gasto_otros` | `OTROS` | decimal | 0 | Otros gastos inherentes a la actividad comercial (miles de pesos) |
| `sueldos` | `SUELDOS` | decimal | 0 | Total Sueldos y salarios causados en el año (miles de pesos) |
| `prestaciones` | `PRESTAC` | decimal | 0 | Total Prestaciones sociales causadas en el año (miles de pesos) |
| `ventas` | `VENTA` | decimal | 0 | Ventas causadas en el año (miles de pesos) |
| `valor_agregado` | `AGREGA` | decimal | 0 | Valor Agregado: producción bruta - consumo intermedio (miles de pesos) |
| `personal_remunerado` | `PERREMUN` | decimal | 0 | Personal remunerado |
| `socios_sin_remuneracion` | `SOCIOS` | decimal | 0 | Propietarios, socios y familiares-Total sin remuneración |
| `personal_permanente` | `PERSONOM` | decimal | 0 | Personal permanente-Total |
| `personal_temporal_directo` | `DIRECTO` | decimal | 0 | Personal temporal directo-Total |
| `personal_agencias` | `AGENCIA` | decimal | 0 | Personal temporal cont a través de agencias - Total |
| `aprendices` | `APRENDIZ` | decimal | 0 | Aprendices-Total |
| `personal_total` | `TOTPERSO` | decimal | 0 | Personal total: incluye socios sin remuneración, personal permanente, temporal directo, aprendices y personal contratado a través de empresas especializadas en el suministro de personal |
| `socios_mujeres` | `PROMUJ` | decimal | 0 | Propietarios, socios y familiares-Mujeres |
| `socios_hombres` | `PROHOM` | decimal | 0 | Propietarios, socios y familiares-Hombres |
| `permanente_mujeres` | `PERMUJ` | decimal | 0 | Personal permanente-Mujeres |
| `permanente_hombres` | `PERHOM` | decimal | 0 | Personal permanente-Hombres |
| `temporal_directo_mujeres` | `DIRMUJ` | decimal | 0 | Personal temporal directo-Mujeres |
| `temporal_directo_hombres` | `DIRHOM` | decimal | 0 | Personal temporal directo-Hombres |
| `agencias_mujeres` | `AGEMUJ` | decimal | 0 | Personal temporal cont a través de agencias - Mujeres |
| `agencias_hombres` | `AGEHOM` | decimal | 0 | Personal temporal cont a través de agencias - Hombres |
| `aprendices_mujeres` | `APRENMUJ` | decimal | 0 | Aprendices-Mujeres |
| `aprendices_hombres` | `APRENHOM` | decimal | 0 | Aprendices-Hombres |
| `personal_mujeres` | `TOTMUJ` | decimal | 0 | Personal total-Mujeres |
| `personal_hombres` | `TOTHOM` | decimal | 0 | Personal total-Hombres |
| `sueldos_planta` | `SUEPLAN` | decimal | 0 | Sueldos Planta (miles de pesos) |
| `prestaciones_planta` | `PREPLAN` | decimal | 0 | Prestaciones Planta (miles de pesos) |
| `remuneracion_planta` | `REMPLAN` | decimal | 0 | Remuneración Planta (miles de pesos) |
| `cotizaciones_patronales` | `COTIZA` | decimal | 0 | Cotizaciones patronales obligatorias causadas en el año (miles de pesos) |
| `gasto_personal_agencias` | `GASAGEN` | decimal | 0 | Gastos causados por el personal temporal suministrado por agencias de empleo (miles de pesos) |
| `remuneracion_temporal` | `REMTEMP` | decimal | 0 | Remuneración temporal (miles de pesos) |
| `remuneracion_total` | `TOTREM` | decimal | 0 | Total Remuneracion (miles de pesos) |
| `inventario_inicial` | `INVINI` | decimal | 0 | Existencias a diciembre del año anterior al proceso (miles de pesos) |
| `inventario_final` | `INVFIN` | decimal | 0 | Existencias a dic 31 del año de proceso (miles de pesos) |
| `rotacion_inventarios` | `ROTACION` | decimal | 0 | Rotación de Inventarios (miles de pesos) |
| `inventario_promedio` | `INVPRO` | decimal | 0 | Inventario Promedio (miles de pesos) |
| `costo_mercancia_vendida` | `CTO` | decimal | 0 | Costo de mercancia vendida (miles de pesos) |
| `costo_mercancia_e_insumos` | `CTOINS` | decimal | 0 | Total costo de la mercancía más costo de insumos de actividades relacionadas con el comercio. (miles de pesos) |
| `costos_gastos_operacionales` | `GASTOS` | decimal | 0 | Total costos y gastos operacionales (miles de pesos) |
| `gastos_no_operacionales` | `GASTOSNOP` | decimal | 0 | Subtotal Gastos no operacionales (miles de pesos) |
| `costos_gastos_totales` | `GASTOPNOP` | decimal | 0 | Total Costos y gastos operacionales y no operacionales (miles de pesos) |
| `org_juridica` | — | texto | 0 | Etiqueta legible de `org_juridica_cod`, desde la hoja 2 del diccionario del DANE (1.6.4) |
| `actividad_16` | — | texto | 0 | Nombre del dominio de actividad de 16 categorías (1.6.5) |
| `actividad_9` | — | texto | 0 | Nombre del dominio de actividad de 9 categorías (1.6.5) |
| `antiguedad` | — | entero | 0 | Años de operación: 2024 − `anio_inicio` (1.6.7) |
| `tramo_personal` | — | texto | 0 | Tamaño por personal: Micro 1-10, Pequeña 11-50, Mediana 51-200, Grande >200 (1.6.7) |
| `margen` | — | decimal | 0 | `valor_agregado` / `ventas` (1.6.7) |
| `part_mujeres` | — | decimal | 0 | `personal_mujeres` / `personal_total` (1.6.7) |
| `remuneracion_media` | — | decimal | 88 | `remuneracion_total` / `personal_remunerado`, en miles de pesos al año (1.6.7) |

> Esta tabla se genera desde `eac_2024_limpio.csv` y el diccionario oficial del DANE, con la
> misma lógica del apartado 1.4.1 del cuaderno. El único dato faltante del dataset son los 88
> registros de `remuneracion_media`: empresas con personal pero sin remuneración reportada,
> donde la división daría un valor sin sentido (explicado en 1.6.7).

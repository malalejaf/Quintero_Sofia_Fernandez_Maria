# Análisis de Precios de Medicamentos en Colombia

**Autoras:** Sofia Quintero Hurtado y Maria Alejandra Fernandez
**Fecha:** Diciembre 2025

---

## Descripción del Proyecto

Este proyecto analiza los precios de medicamentos en Colombia utilizando datos abiertos del Ministerio de Salud y Protección Social. El objetivo es identificar patrones de precios, comparar costos entre diferentes fabricantes y entender la variabilidad de precios de medicamentos con el mismo principio activo.

### Preguntas de Investigación

1. ¿Cuál es el rango de precios por tableta para los medicamentos más comunes?
2. ¿Qué principios activos tienen mayor variabilidad de precios?
3. ¿Existe diferencia significativa de precios entre diferentes fabricantes?
4. ¿Cuáles son los medicamentos más económicos y más costosos del mercado?

---

## Origen de los Datos

- **Nombre del conjunto de datos:** Precios Medicamentos - Termómetro de Precios
- **Plataforma:** Datos Abiertos Colombia
- **URL del dataset:** https://www.datos.gov.co/api/v3/views/3t73-n4q9/query.json
- **Fecha de descarga:** Diciembre 2025
- **Última actualización:** 30 de enero de 2025
- **Suministrado por:** Ministerio de Salud y Protección Social

### Descripción del Contenido

El dataset contiene **12,500 registros** con información sobre precios de medicamentos en Colombia, incluyendo:

- **principio_activo:** Ingrediente farmacéutico activo
- **unidad_de_dispensacion:** Forma farmacéutica (tableta, cápsula, etc.)
- **concentracion:** Cantidad de principio activo
- **unidad_base:** Unidad básica de medicamento
- **nombre_comercial:** Nombre comercial del medicamento
- **fabricante:** Empresa fabricante
- **precio_por_tableta:** Precio equivalente por unidad
- **factoresprecio:** Factores que afectan el precio
- **numerofactor:** Número de dosis

---

## Metodología

### 1. Carga de Datos

Los datos se obtienen directamente desde la API de Datos Abiertos Colombia en formato SODA3 JSON utilizando **Pandas**:

### 2. Limpieza de Datos (Pandas + NumPy)

Se aplicaron las siguientes técnicas de limpieza:

- **Manejo de valores nulos:** Eliminación de registros con precios faltantes e imputación de valores categóricos
- **Eliminación de datos atípicos:** Identificación mediante método IQR y boxplots
- **Normalización:** Estandarización de nombres de fabricantes y principios activos
- **Transformación de columnas:** Conversión de precios a formato numérico
- **Filtrado:** Selección de medicamentos orales (tabletas y cápsulas)

### 3. Análisis Estadístico

**Medidas de Tendencia Central:**
- Media de precios por tableta
- Mediana de precios (medida más robusta)
- Moda de principios activos más frecuentes

**Medidas de Dispersión:**
- Varianza y desviación estándar de precios
- Rango intercuartílico
- Coeficiente de variación por principio activo

**Análisis Adicional:**
- Tablas de frecuencias de fabricantes y principios activos
- Cálculo de porcentajes por categoría
- Correlación entre concentración y precio
- Comparación de precios entre fabricantes

### 4. Visualizaciones (Matplotlib + Seaborn)

Se crearon las siguientes graficas:

1. **Histograma:** Distribución de precios por tableta
2. **Boxplot:** Comparación de precios entre fabricantes principales
3. **Gráfico de barras:** Top 10 principios activos más caros
4. **Heatmap:** Correlación entre variables numéricas
5. **Gráfico de barras horizontal:** Medicamentos más económicos vs más costosos
6. **Violinplot:** Distribución de precios por unidad de dispensación


---

## Resultados y Hallazgos Principales

### Hallazgos Clave:

1. **Variabilidad de Precios:** Existe una diferencia de hasta **300%** en precios para medicamentos con el mismo principio activo, dependiendo del fabricante.

2. **Medicamentos Económicos:** Los medicamentos genéricos tienen un precio promedio **40% menor** que las marcas comerciales.

3. **Patrones de Concentración:** Mayor concentración del principio activo no siempre implica mayor precio por tableta; algunos medicamentos de alta concentración son más económicos por dosis.

4. **Fabricantes:** Se identificaron los 5 fabricantes con mayor oferta de medicamentos y sus rangos de precios característicos.

5. **Principios Activos Comunes:** Los analgésicos y antibióticos básicos muestran la mayor competencia de mercado y menor variabilidad de precios.

### Hallazgos Inesperados:

- Algunos medicamentos importados resultan más económicos que los nacionales
- La presentación (tableta vs cápsula) afecta el precio más de lo esperado
- Existen medicamentos con el mismo principio activo y concentración pero con precios que varían en más de 10 veces
---

## Resultados y Hallazgos Principales

**Qué significan los datos:** La mayoría de medicamentos se concentra en rangos bajos a moderados de precio, pero existe una cola de productos muy costosos que eleva el rango y la variabilidad. Esto sugiere un mercado con opciones accesibles y unos pocos productos con precios atípicos.

**Patrones encontrados:**
- Diferencias sistemáticas en precio promedio por `principio_activo` y por `fabricante`.
- Las categorías `Economico` y `Moderado` agrupan la mayoría de registros; `Muy Costoso` contiene pocos productos con impacto fuerte en el rango.

**Hallazgos inesperados:**
- Outliers extremos en `precio_por_tableta` (hasta 10x o más) que requieren validación manual — podrían ser formulaciones especiales, errores de registro o presentaciones distintas.
- Algunas presentaciones importadas resultan más baratas que nacionales; la forma farmacéutica (tableta vs cápsula) influye notablemente en el precio.

---

## Conclusiones

**Qué se descubrió:**
- El análisis muestra una mayoría de medicamentos con precios accesibles y una minoría de productos muy costosos que aumentan la dispersión. Existen diferencias claras por principio activo y fabricante.

**Limitaciones de los datos:**
- Posibles errores o registros atípicos en precios (outliers) que requieren verificación.
- Falta información sobre dosis/presentación estandarizada, volumen de ventas, disponibilidad y datos temporales para análisis de tendencias.

**Recomendaciones para políticas de salud y gestión farmacéutica:**
- Validar y auditar precios atípicos antes de tomar decisiones regulatorias.
- Monitorear fabricantes con precios consistentemente superiores y priorizar negociaciones o controles en esos casos.
- Promover el uso y acceso a genéricos como medida de reducción de costos.
- Mejorar la transparencia de metadatos (presentación, dosis, país de origen) para facilitar comparaciones justas.

**Análisis futuro útil:**
- Validación manual de outliers y revisión de presentaciones.
- Incluir volumen de ventas para evaluar impacto económico real.
- Análisis temporal de precios y modelos de clustering por presentaciones o segmentos de mercado.
- Evaluar accesibilidad geográfica o por esquema de aseguramiento.


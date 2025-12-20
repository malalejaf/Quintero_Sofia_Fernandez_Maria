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

Los datos se obtienen directamente desde la API de Datos Abiertos Colombia en formato JSON utilizando **Pandas** y SODA3:

```python
import pandas as pd
import requests

url = "https://www.datos.gov.co/api/v3/views/3t73-n4q9/query.json"
response = requests.get(url)
data = response.json()
df = pd.json_normalize(data)
```

### 2. Limpieza de Datos (Pandas + NumPy)

Se aplicaron las siguientes técnicas de limpieza:

- **Manejo de valores nulos:** Eliminación de registros con precios faltantes e imputación de valores categóricos
- **Eliminación de datos atípicos:** Identificación mediante método IQR y boxplots
- **Normalización:** Estandarización de nombres de fabricantes y principios activos
- **Transformación de columnas:** Conversión de precios a formato numérico
- **Filtrado:** Selección de medicamentos orales (tabletas y cápsulas)

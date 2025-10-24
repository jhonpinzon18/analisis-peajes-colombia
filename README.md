# Análisis de Peajes en Colombia con Big Data

[![Apache Spark](https://img.shields.io/badge/Apache%20Spark-3.x-E25A1C?style=flat&logo=apache-spark&logoColor=white)](https://spark.apache.org/)
[![Hadoop](https://img.shields.io/badge/Hadoop-3.x-66CCFF?style=flat&logo=apache-hadoop&logoColor=black)](https://hadoop.apache.org/)
[![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=flat&logo=python&logoColor=white)](https://www.python.org/)

## Descripción

Este proyecto implementa un sistema de análisis de datos utilizando tecnologías de Big Data para procesar información de 98,306 transacciones de peajes en Colombia. El sistema utiliza Apache Spark (PySpark) sobre Hadoop HDFS para realizar procesamiento batch, incluyendo limpieza de datos, transformaciones y análisis exploratorio.

## Objetivos

El proyecto busca identificar patrones de tráfico vehicular, analizar la recaudación por peaje y categoría de vehículo, detectar comportamientos de evasión y examinar tendencias temporales en el uso de la red de peajes nacional.

---

## Archivos Generados

El procesamiento genera los siguientes archivos de resultados en HDFS:

| Archivo | Descripción |
|---------|-------------|
| `datos_limpios.parquet/` | Dataset completo procesado en formato Parquet optimizado |
| `datos_limpios.csv/` | Dataset completo procesado en formato CSV |
| `analisis_por_peaje.csv/` | Métricas agregadas por peaje: tráfico, recaudación y tarifas promedio |
| `analisis_por_categoria.csv/` | Análisis segmentado por las 9 categorías de vehículos |
| `analisis_temporal.csv/` | Tendencias y patrones por año y mes |
| `resumen_estadistico.csv/` | Estadísticas descriptivas del dataset |

---

## Tecnologías Utilizadas

- **Apache Hadoop 3.x** - Sistema de archivos distribuido (HDFS) y gestor de recursos (YARN)
- **Apache Spark 3.x** - Motor de procesamiento distribuido en memoria
- **PySpark 3.x** - API de Python para Apache Spark
- **Python 3.12** - Lenguaje de programación principal
- **Java 17** - Entorno de ejecución para Hadoop y Spark

---

## Instrucciones de Ejecución

### Requisitos Previos

Es necesario tener instalado y configurado Hadoop, Spark y Python. El dataset `peajes_colombia.csv` debe estar disponible en HDFS en la ruta `/Tarea3/`.

### Ejecución del Análisis

```bash
# Iniciar servicios de Hadoop
start-dfs.sh && start-yarn.sh

# Verificar que los servicios estén activos
jps

# Ejecutar el script de análisis
spark-submit analisis_peajes.py

# Revisar los resultados generados
hdfs dfs -ls /Tarea3/Resultados_Peajes_Colombia/
```

### Ejecución en Modo Interactivo

Para desarrollo o pruebas, se puede ejecutar el análisis en modo interactivo:

```bash
pyspark
>>> exec(open('analisis_peajes.py').read())
```

---

## Características del Dataset

El dataset contiene 98,306 registros con las siguientes columnas:

- **IdPeaje**: Identificador único del peaje
- **Peaje**: Nombre del peaje
- **IdCategoriaTarifa**: Categoría del vehículo (1-9)
- **FechaDesde** y **FechaHasta**: Período de vigencia de la tarifa
- **ValorTarifa**: Valor de la tarifa en pesos colombianos
- **Trafico**: Número de vehículos
- **TraficoEvasores**: Vehículos que evadieron el pago
- **TraficoExentos787**: Vehículos exentos según la Ley 787

---

## Procesamiento Implementado

### Limpieza de Datos

El proceso incluye eliminación de registros duplicados, tratamiento de valores nulos, corrección de tipos de datos y validación de la integridad de la información.

### Transformaciones

Se calculan nuevas columnas derivadas:
- **TraficoTotal**: Suma de tráfico regular, evasores y exentos
- **PorcentajeEvasion**: Proporción de vehículos que evadieron el pago
- **RecaudacionEstimada**: Producto del tráfico por el valor de la tarifa
- **TipoVehiculo**: Clasificación en livianos, pesados y especiales según la categoría

### Análisis Exploratorio

El análisis incluye estadísticas descriptivas generales, identificación de los peajes con mayor tráfico y recaudación, distribución por categorías de vehículos, análisis de tendencias temporales y cálculo de tasas de evasión.

### Técnicas de Procesamiento

Se utilizan DataFrames de Spark para operaciones de agregación y consultas tipo SQL, junto con RDDs para transformaciones personalizadas tipo map-reduce cuando es necesario.

---

## Estructura del Repositorio

```
analisis-peajes-colombia/
├── analisis_peajes.py              # Script principal de PySpark
├── datos_limpios.parquet/          # Dataset procesado (Parquet)
├── datos_limpios.csv/              # Dataset procesado (CSV)
├── analisis_por_peaje.csv/         # Métricas por peaje
├── analisis_por_categoria.csv/     # Métricas por categoría
├── analisis_temporal.csv/          # Análisis temporal
└── resumen_estadistico.csv/        # Estadísticas descriptivas
```

---

## Contexto del Proyecto

Este proyecto fue desarrollado como parte del curso de Big Data y Análisis de Datos Distribuidos en la Universidad Nacional Abierta y a Distancia (UNAD). El trabajo demuestra la implementación de un pipeline completo de procesamiento batch, aplicando técnicas de ETL, análisis exploratorio y almacenamiento distribuido.

---

## Autor

**Jhon Pinzón Rodriguez**  
Universidad Nacional Abierta y  a Distancia (UNAD)  
jhpinzonr@unadvirtual.edu.co  
[GitHub: @jhonpinzon18](https://github.com/jhonpinzon18)

---

## Información del Proyecto

- **Fecha**: Octubre 2025
- **Versión**: 1.0
- **Estado**: Completo y funcional

---

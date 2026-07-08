# Estudio estadístico de variaciones meteorológicas y oceánicas en Cantabria

**Trabajo Fin de Máster — Máster en Ciencia de Datos**  
Sara Lanza Sarabia · Universidad de Cantabria · 2025–2026

---

## Descripción

Análisis estadístico de series temporales de temperatura, precipitación y nivel del mar en Cantabria, aplicando técnicas no paramétricas para la detección de tendencias, cambios estructurales y señales de cambio climático regional.

El trabajo compara dos estaciones meteorológicas con entornos contrastados — **Santander** (litoral, 3 m s.n.m., 1961–2025) y **Tama** (valle interior, 250 m s.n.m., 1972–2025) — e incorpora el análisis del nivel del mar a partir de los registros históricos del mareógrafo del IEO-CSIC en Santander (1943–2017).

---

## Contexto

Este repositorio recoge el código y los datos completos utilizados en el TFM del Máster en Ciencia de Datos de la Universidad de Cantabria, con el objetivo de garantizar la trazabilidad y reproducibilidad del análisis.

---

## Fuentes de datos

- **AEMET** — Datos diarios de temperatura y precipitación descargados mediante la API de datos abiertos de AEMET (Python/requests).
- **IEO-CSIC** — Registros horarios del nivel del mar del mareógrafo de Santander (facilitados por el Centro Oceanográfico de Santander).

---

## Estructura del repositorio

```text
.
├── temperatura/
│   ├── Bloque1_AnalisisTemperatura.Rmd      # Análisis de extremos térmicos y test de Montecarlo-KS
│   ├── Bloque1_AnalisisTemperatura.html     # Output renderizado
│   └── figuras/                            # Gráficas generadas
│
├── precipitacion/
│   ├── Bloque2_AnalisisPrecipitacion.Rmd    # Análisis del régimen pluviométrico, rachas, PCI/SI y centroide
│   ├── Bloque2_AnalisisPrecipitacion.html   # Output renderizado
│   └── figuras/                            # Gráficas generadas
│
├── nivel_del_mar/
│   ├── Bloque3_NivelMar.Rmd                 # Análisis mareográfico: filtro de Godin, análisis armónico y tendencias
│   ├── Bloque3_NivelMar.html                # Output renderizado
│   └── figuras/                            # Gráficas generadas
│
└── descarga_datos/
    └── descarga_datosAEMET.ipynb            # Descarga y curado de datos vía API AEMET
```

---

## Contenido por bloque

- **Temperatura**: limpieza e imputación de NA, identificación de días de calor/frío extremo (percentiles 95/5), test de Montecarlo-KS para contrastar su distribución temporal.
- **Precipitación**: tratamiento de valores especiales de AEMET (_Ip_, _Tr_, bloques _Acum_), imputación de NA mediante cadenas de Markov, rachas de sequía/lluvia, intensidad media, índices PCI/SI, centroide anual y análisis de sensibilidad frente a los meses de primavera.
- **Nivel del mar**: remuestreo horario, filtro de Godin, análisis armónico (`oce::tidem`), tendencia del nivel medio y evolución de extremos anuales.
- **Descarga de datos**: notebook de Python que documenta la consulta a la API de datos abiertos de AEMET, la unión de los JSON por periodos y la fusión con los registros históricos del Instituto Oceanográfico.

---

## Métodos estadísticos

- **Test de Mann-Kendall** con corrección TFPW para autocorrelación
- **Estimador de Sen** con intervalos de confianza al 95%
- **Test de Pettitt** con verificación de robustez ante años inválidos
- **Test de Monte Carlo-KS** para extremos térmicos
- **Tests de Wilcoxon y t de Student** para comparación entre periodos
- **Análisis armónico** (oce::tidem) para control de calidad mareográfico
- **Filtro de Godin** para eliminación de la señal mareal
- **Índices PCI y SI** de concentración y estacionalidad de precipitación
- **Centroide de precipitación** como día del año en que se alcanza el 50% de la acumulación anual

---

## Requisitos

```r
# Paquetes principales de R
install.packages(c(
  "tidyverse", "lubridate", "zoo",
  "trend", "modifiedmk",
  "oce", "knitr", "kableExtra",
  "ggplot2", "patchwork"
))
```

Para el notebook de descarga de datos (Python):
```bash
pip install requests pandas
```

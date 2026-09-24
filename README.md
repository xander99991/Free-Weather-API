Variabilidad climática y El Niño en tres regiones del Ecuador (1995–2025)

Universidad Yachay Tech
Maestría en Ciencia de Datos
Fundamentos de Ciencia de Datos
Tarea 1: Contestando preguntas sobre los datos
Autor: Alexander Omar Fernández Pérez
Fecha: septiembre de 2026

Descripción
En este proyecto se descargan datos meteorológicos diarios desde la API gratuita de Open-Meteo , se guardan en un archivo local, se exploran con estadísticas descriptivas y cinco gráficas en Matplotlib , y se responden tres preguntas sobre el clima en la Sierra, la Costa y la Amazonía del Ecuador.

Región	Provincia	Ciudad	Latitud	Longitud
Sierra	Pichincha	Quito	-0,18	-78,47
Costa	Guayas	Guayaquil	-2.19	-79.89
Amazonía	Napo	Tena	-0,99	-77.81

Preguntas de investigación
P1. ¿Se han calentado las tres regiones del Ecuador entre 1995 y 2025?
P2. ¿El fenómeno de El Niño afecta por igual a la Costa, la Sierra y la Amazonía?
P3. ¿Qué región enfrenta mayor déficit hídrico y en qué meses?

Estructura del repositorio
├── README.md                 ← Este archivo
├── requirements.txt          ← Librerías necesarias
├── descargar_datos.py        ← Script que lee los datos desde la API y los guarda en CSV
├── tarea1_clima.ipynb        ← Notebook con el EDA, las gráficas y las respuestas
├── data/
│   └── clima_ecuador.csv     ← Datos descargados (3 ciudades × 11.323 días)
└── figuras/
    ├── 01_heatmap_anomalias_temp.png
    ├── 02_tendencia_max_min.png
    ├── 03_anomalia_lluvia_el_nino.png
    ├── 04_balance_hidrico.png
    └── 05_reloj_lluvia.png

Datos
Fuente: Open-Meteo, API de Tiempo Histórico ( archive-api.open-meteo.com/v1/archive)
Periodo: 1 de enero de 1995 a 31 de diciembre de 2025, con frecuencia diaria
Zona horaria: América/Guayaquil
Uso de la API: una sola llamada para las 3 ciudades (unas 2.400 llamadas ponderadas, dentro del límite gratuito de 10.000 por día)

Variables descargadas
Variable (API)	Descripción	Unidad
temperature_2m_mean	Temperatura media diaria a 2 m	°C
temperature_2m_max	Temperatura máxima diaria	°C
temperature_2m_min	Temperatura mínima diaria	°C
precipitation_sum	Precipitación total diaria	mm
precipitation_hours	Horas con precipitación	h
et0_fao_evapotranspiration	Evapotranspiración de referencia (FAO Penman-Monteith)	mm
shortwave_radiation_sum	Radiación solar de onda corta	MJ/m²
wind_speed_10m_max	Velocidad máxima del viento a 10 m	km/h

Variables calculadas
Variable	Fórmula	Uso
Anomalía de temperatura	Temperatura del mes − promedio 1995–2025 del mismo mes	P1
Anomalía de lluvia	Lluvia del mes − promedio 1995–2025 del mismo mes	P2
Equilibrio hídrico climático	Lluvia − ET₀	P3
Amplitud térmica	Máxima − mínima	EDA / P1

Visualizaciones
Gráfica 1. Anomalías mensuales de temperatura (P1)
Gráfica 2. Tendencia de las temperaturas máxima y mínima (P1)
Gráfica 3. Anomalía de lluvia y episodios de El Niño (P2)
Gráfica 4. Balance hídrico climático por mes (P3)
Gráfica 5. Ciclo anual de la lluvia (contexto)

Resultados
P1. ¿Se han calentado las tres regiones?
Sí, sobre todo en las temperaturas máximas.

P2. ¿El Niño afecta por igual a las tres regiones?
No. Su efecto se concentra en la Costa.

P3. ¿Qué región tiene mayor déficit hídrico?
La Costa (Guayaquil): 5 meses al año, de agosto a diciembre , con el punto más crítico en octubre y noviembre 

Limitaciones
Datos de reanálisis, no de estaciones. Son estimaciones de modelo en celdas de varios kilómetros. En zonas de montaña, como Quito, pueden diferir de lo registrado en la ciudad.
Posible quiebre en 2017. La opción predeterminada de la API ("Best Match") combina varios modelos e incorpora ECMWF IFS desde 2017, lo que puede generar saltos artificiales en las series.
Las tendencias estimadas son mayores que las reportadas a escala global y deben validarse con estaciones del INAMHI.

Fuente de datos y licencia
Datos meteorológicos de Open-Meteo.com (Historical Weather API), con licencia CC BY 4.0 . Se usan con multas académicas y no comerciales.
Zippenfenig, P. (2023). Open-Meteo.com Weather API [software informático]. Zenodo. https://doi.org/10.5281/ZENODO.7970649



# Variabilidad climática y El Niño en tres regiones del Ecuador (1995–2025)

**Universidad Yachay Tech**, Maestría en Ciencia de Datos
**Asignatura:** Fundamentos de Ciencia de Datos, Tarea 1: *Contestando preguntas sobre los datos*
**Autor:** Alexander Omar Fernández Pérez
**Fecha:** septiembre de 2026

---

## Descripción

En este proyecto se descargan datos meteorológicos diarios desde la API gratuita de **[Open-Meteo](https://open-meteo.com/)**, se guardan en un archivo local, se exploran con estadística descriptiva y **cinco gráficas en Matplotlib**, y se responden tres preguntas sobre el clima en la **Sierra, la Costa y la Amazonía** del Ecuador.

| Región | Provincia | Ciudad | Latitud | Longitud |
|---|---|---|---|---|
| Sierra | Pichincha | Quito | -0.18 | -78.47 |
| Costa | Guayas | Guayaquil | -2.19 | -79.89 |
| Amazonía | Napo | Tena | -0.99 | -77.81 |

## Preguntas de investigación

1. **P1.** ¿Se han calentado las tres regiones del Ecuador entre 1995 y 2025?
2. **P2.** ¿El fenómeno de El Niño afecta por igual a la Costa, la Sierra y la Amazonía?
3. **P3.** ¿Qué región enfrenta mayor déficit hídrico y en qué meses?

## Estructura del repositorio

```
├── README.md                 ← Este archivo
├── requirements.txt          ← Librerías necesarias
├── descargar_datos.py        ← Script que lee los datos desde la API y los guarda en CSV
├── weather_api.ipynb        ← Notebook con el EDA, las gráficas y las respuestas
├── data/
│   └── clima_ecuador.csv     ← Datos descargados (3 ciudades × 11.323 días)
└── figuras/
    ├── 01_heatmap_anomalias_temp.png
    ├── 02_tendencia_max_min.png
    ├── 03_anomalia_lluvia_el_nino.png
    ├── 04_balance_hidrico.png
    └── 05_reloj_lluvia.png
```

## Cómo reproducir el análisis

```bash
# 1. Clonar el repositorio
git clone <URL-del-repositorio>
cd <carpeta-del-repositorio>

# 2. Instalar las librerías
pip install -r requirements.txt

# 3. Descargar los datos (una sola llamada a la API)
python descargar_datos.py

# 4. Abrir el notebook y ejecutar todas las celdas
jupyter notebook weather_api.ipynb
```

> El archivo `data/clima_ecuador.csv` ya está incluido, así que el paso 3 es opcional.

## Datos

- **Fuente:** Open-Meteo, [Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api) (`archive-api.open-meteo.com/v1/archive`)
- **Periodo:** 1 de enero de 1995 a 31 de diciembre de 2025, con frecuencia diaria
- **Zona horaria:** America/Guayaquil
- **Uso de la API:** una sola llamada para las 3 ciudades (unas 2.400 llamadas ponderadas, dentro del límite gratuito de 10.000 por día)

### Variables descargadas

| Variable (API) | Descripción | Unidad |
|---|---|---|
| `temperature_2m_mean` | Temperatura media diaria a 2 m | °C |
| `temperature_2m_max` | Temperatura máxima diaria | °C |
| `temperature_2m_min` | Temperatura mínima diaria | °C |
| `precipitation_sum` | Precipitación total diaria | mm |
| `precipitation_hours` | Horas con precipitación | h |
| `et0_fao_evapotranspiration` | Evapotranspiración de referencia (FAO Penman-Monteith) | mm |
| `shortwave_radiation_sum` | Radiación solar de onda corta | MJ/m² |
| `wind_speed_10m_max` | Velocidad máxima del viento a 10 m | km/h |

### Variables calculadas

| Variable | Fórmula | Uso |
|---|---|---|
| Anomalía de temperatura | Temperatura del mes − promedio 1995–2025 del mismo mes | P1 |
| Anomalía de lluvia | Lluvia del mes − promedio 1995–2025 del mismo mes | P2 |
| Balance hídrico climático | Lluvia − ET₀ | P3 |
| Amplitud térmica | Máxima − mínima | EDA / P1 |

## Visualizaciones

### Gráfica 1. Anomalías mensuales de temperatura (P1)
![Gráfica 1](figuras/01_heatmap_anomalias_temp.png)

### Gráfica 2. Tendencia de las temperaturas máxima y mínima (P1)
![Gráfica 2](figuras/02_tendencia_max_min.png)

### Gráfica 3. Anomalía de lluvia y episodios de El Niño (P2)
![Gráfica 3](figuras/03_anomalia_lluvia_el_nino.png)

### Gráfica 4. Balance hídrico climático por mes (P3)
![Gráfica 4](figuras/04_balance_hidrico.png)

### Gráfica 5. Ciclo anual de la lluvia (contexto)
![Gráfica 5](figuras/05_reloj_lluvia.png)

## Resultados

### P1. ¿Se han calentado las tres regiones?

**Sí, sobre todo en las temperaturas máximas.**

| Ciudad | Máxima (°C/década) | Mínima (°C/década) |
|---|---|---|
| Quito | +0,73 | −0,37 |
| Guayaquil | +0,95 | +0,26 |
| Tena | +0,81 | +0,58 |

El calentamiento es mayor de día que de noche. En Quito, las máximas suben y las mínimas bajan, por lo que aumenta la amplitud térmica diaria.

### P2. ¿El Niño afecta por igual a las tres regiones?

**No. Su efecto se concentra en la Costa.** En Guayaquil, El Niño 1997–98 generó anomalías de lluvia de unos +800 mm/mes; el episodio de 2015–16 fue moderado y el de 2023–24 casi no dejó un exceso de lluvia. En Quito y Tena no se observa un patrón claro durante los episodios de El Niño.

### P3. ¿Qué región tiene mayor déficit hídrico?

**La Costa (Guayaquil): 5 meses al año, de agosto a diciembre**, con el punto más crítico en octubre y noviembre (unos −60 mm/mes). Quito tiene un balance cercano a cero en julio y agosto, y Tena no presenta déficit en ningún mes.

## Limitaciones

1. **Datos de reanálisis, no de estaciones.** Son estimaciones de modelo en celdas de varios kilómetros. En zonas de montaña, como Quito, pueden diferir de lo registrado en la ciudad.
2. **Posible quiebre en 2017.** La opción predeterminada de la API ("Best Match") combina varios modelos e incorpora ECMWF IFS desde 2017, lo que puede generar saltos artificiales en las series. Se recomienda repetir el análisis con un solo modelo (`models=era5`).
3. **Las tendencias estimadas** son mayores que las reportadas a escala global y deberían validarse con estaciones del INAMHI.

## Herramientas

Python 3 · `requests` · `pandas` · `numpy` · `matplotlib` · Jupyter / VS Code

## Fuente de datos y licencia

Datos meteorológicos de [Open-Meteo.com](https://open-meteo.com/) (Historical Weather API), con licencia [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Se usan con fines académicos y no comerciales.

> Zippenfenig, P. (2023). *Open-Meteo.com Weather API* [Computer software]. Zenodo. https://doi.org/10.5281/ZENODO.7970649
>
> Hersbach, H. et al. (2023). *ERA5 hourly data on single levels from 1940 to present* [Data set]. ECMWF. https://doi.org/10.24381/cds.adbb2d47

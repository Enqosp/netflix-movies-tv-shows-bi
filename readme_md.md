# 🎬 Netflix Catalog Analytical Dashboard (2021)

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-00758F?style=for-the-badge&logo=powerbi&logoColor=white)
![Power Query](https://img.shields.io/badge/Power_Query-00838F?style=for-the-badge&logo=powerbi&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)

---

## 📋 1. Resumen Ejecutivo & Objetivos del Proyecto
Este proyecto presenta una solución de **Business Intelligence** integral desarrollada en **Power BI** para explorar, analizar y visualizar la oferta global de contenidos de Netflix hasta mediados de 2021.

### Objetivos Clave:
* **Analizar la estructura del catálogo:** Identificar la proporción histórica entre largometrajes (*Movies*) y series de televisión (*TV Shows*).
* **Evaluar métricas de duración sin contaminación de datos:** Diseñar medidas analíticas aisladas para minutos (películas) y temporadas (series), evitando la mezcla errónea de unidades heterogéneas.
* **Mapear tendencias de adquisición e historial de estrenos:** Analizar los hábitos de la industria audiovisual a lo largo de las décadas (`release_year`) frente a las estrategias de incorporación de catálogo de la plataforma (`date_added`).
* **Optimizar la experiencia de usuario (UX/UI):** Implementar la jerarquía visual de Tamara Munzner, reservando el espacio principal para la macroinformación y aprovechando *Tooltips* emergentes interactivos para el detalle micro.

---

## 🛠️ 2. Arquitectura de Datos y Limpieza (Data Quality)
El procesamiento de datos se realizó a través del editor **Power Query (M)** en Power BI, asegurando los estándares de gobernanza y calidad de datos (*Data Quality*).

### Transformaciones y Limpieza Realizadas:
1. **Validación de Categorías (`type`):** Verificación al 100% de la integridad de los registros, confirmando valores limpios y normalizados para *Movie* y *TV Show*.
2. **Extracción Numérica de Duración (`duracion_num`):** Descomposición de la columna original `duration` en valores puramente numéricos mediante delimitadores de texto para permitir operaciones aritméticas de agregación y promedios.
3. **Parseo de Fechas (`date_added`):** Conversión de cadenas de texto a formato nativo *Datetime*, extrayendo campos temporales como Año de Agregación y Mes.
4. **Tratamiento de Nulos y Cadenas Descomprimidas:** Imputación de valores no disponibles en campos cualitativos (`director`, `cast`, `country`) para evitar vacíos en las segmentaciones geográficas y descriptivas.

---

## 📐 3. Modelado y Medidas DAX Principales
Se construyeron medidas calculadas en DAX con filtrado contextual directo utilizando `CALCULATE`, garantizando que cada formato de contenido mantenga su unidad de medida adecuada.

```dax
// Conteo General de Títulos
Total Titulos = COUNTROWS(netflix_titles)

// Duración Promedio en Minutos (Exclusivo para Películas)
Prom_Minutos = 
CALCULATE(
    AVERAGE(netflix_titles[duracion_num]), 
    netflix_titles[type] = "Movie"
)

// Extensión Promedio en Temporadas (Exclusivo para Series)
Prom_Temporadas = 
CALCULATE(
    AVERAGE(netflix_titles[duracion_num]), 
    netflix_titles[type] = "TV Show"
)

```

---

## 🎨 4. Diseño UI/UX e Interacción (Tooltips Dinámicos)

Para mantener la pulcritud visual y evitar sobrecargar la interfaz con tarjetas estáticas innecesarias, el tablero implementa Información sobre Herramientas (*Tooltips*) contextuales:

* **Gráfico Circular (Distribución por Tipo):** Despliega de forma dinámica únicamente `Prom_Minutos` al posar el cursor sobre el sector de Películas, y conmuta a `Prom_Temporadas` al consultar el sector de Series.
* **Top 10 Géneros y Países:** Las barras desglosadas responden al contexto del filtro, garantizando que géneros cinematográficos o producciones regionales muestren la medida exacta de su formato.
* **Líneas de Evolución Temporal:** Permite inspeccionar volúmenes y métricas de extensión promedio según el Año de Estreno o el Año de Incorporación.

---

## 📊 5. Vista Previa del Dashboard

---

## 💡 6. Hallazgos Analíticos y Conclusiones de Negocio

1. **Dominio de Largometrajes:** El catálogo refleja una composición predominantemente orientada a películas (∼69.61%) frente a series (∼30.39%).
2. **Duración Promedio del Cine:** La duración media general de las películas se consolida en ∼103.91 minutos, manteniéndose bastante estable en las producciones agregadas en los últimos años.
3. **Estrategia de Renovación en Series:** El promedio global de temporadas para series se ubica en ∼1.76 temporadas, evidenciando un modelo enfocado en miniseries y lanzamientos recientes de pocas temporadas para incentivar el consumo rápido.
4. **Patrones Históricos por Año de Estreno:** Las series estrenadas en décadas pasadas muestran un promedio de temporadas superior al de las producciones más recientes, reflejando la transición del formato televisivo tradicional hacia la era del streaming.

---

## 📁 7. Estructura del Repositorio (.PBIP)

Este repositorio utiliza el formato **Power BI Project (.pbip)**, optimizado para el control de versiones con Git:

```text
├── Netflix Peliculas y Series.Report/          # Formato visual, páginas y layout
├── Netflix Peliculas y Series.SemanticModel/   # Modelo de datos, relaciones y medidas
├── .gitignore                                     # Archivo para ignorar configuraciones locales
├── dashboard.png                                  # Imagen de vista previa del reporte
└── Netflix Peliculas y Series.pbip             # Archivo ejecutable del proyecto

```

---

## 🚀 8. Instrucciones de Uso

### Requisitos Previos

* **Power BI Desktop** (Versión actualizada con soporte para proyectos `.pbip`).

### Pasos para Ejecutar Localmente:

1. Clona este repositorio en tu equipo:
```bash
git clone [https://github.com/Enqosp/netflix-movies-tv-shows-bi.git](https://github.com/Enqosp/netflix-movies-tv-shows-bi.git)

```


2. Navega a la carpeta principal e ingresa a la raíz del proyecto.
3. Abre el archivo ejecutable `Netflix Peliculas y Series.pbip` directamente en Power BI Desktop.
4. Explora las interacciones utilizando los segmentadores (*slicers*) superiores e interactuando con los gráficos mediante el cursor para activar los *Tooltips*.

---

*Proyecto desarrollado con fines analíticos y académicos.*

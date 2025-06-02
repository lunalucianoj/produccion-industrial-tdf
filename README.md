# Predicción de la Producción Industrial Mensual por Sector en Tierra del Fuego

**Materia:** Aprendizaje Automático  
**Carrera:** Tecnicatura Superior en Ciencia de Datos e Inteligencia Artificial  
**Institución:** Politécnico Malvinas Argentinas  
**Alumno:** Luciano Luna  
**Año:** 2025

---

## 📌 Descripción del Proyecto

Este proyecto propone desarrollar un modelo de regresión supervisada capaz de predecir la producción industrial mensual en la provincia de Tierra del Fuego AeIAS, desagregada por sector. Para ello, se integraron tres fuentes de datos oficiales sobre empleo, establecimientos y producción industrial. El análisis busca identificar patrones entre las variables estructurales (empleo y establecimientos) y el comportamiento productivo de sectores clave como el electrónico, textil, plástico, entre otros.

---

## 🎯 Objetivo

**Objetivo General:**  
Construir un modelo de regresión supervisada que estime la producción mensual por sector industrial en función de:

- La cantidad de empleados por sector industrial.
- El número de establecimientos activos por sector.
- Variables temporales: mes y año.

**Objetivos Específicos:**

- Integrar y limpiar datasets históricos industriales.
- Unificar los datos en un único dataset estructurado por sector, mes y año.
- Establecer una base de entrenamiento para aplicar modelos de predicción.

---

## 🧩 Preguntas de Investigación

- ¿Es posible predecir el volumen de producción mensual en un sector a partir de las demás variables?
- ¿Cuáles son los sectores más sensibles a los cambios en empleo y cantidad de establecimientos?
- ¿Existen patrones estacionales o tendencias particulares en algunos sectores?

---

## 🌍 Contexto y Relevancia

Tierra del Fuego posee una estructura productiva altamente concentrada en la industria manufacturera. La posibilidad de anticipar caídas o aumentos en la producción por sector representa una herramienta de gran utilidad para la planificación económica regional, el diseño de políticas públicas, y la toma de decisiones en sectores industriales estratégicos. Este proyecto transforma datos administrativos en información valiosa para la gestión y el análisis prospectivo.

---

## 🗂️ Descripción de los Datasets

| Dataset | Fuente | Años | Variables principales |
|--------|--------|------|------------------------|
| **Producción Industrial por sector** | Instituto Provincial de Estadísticas y Censos (TDF AeIAS) | 2013–2025 | Año, mes, sector, volumen de producción |
| **Empleo en establecimientos industriales** | TDF AeIAS | 2001–2025 | Año, mes, sector, empleados |
| **Cantidad de establecimientos industriales** | TDF AeIAS | 2001–2025 | Año, mes, sector, establecimientos |

Los tres datasets fueron preprocesados para:

- Normalizar los nombres de sectores y meses.
- Unificar las estructuras.
- Resolver inconsistencias y valores nulos o atípicos.
- Convertir los datos a formato largo (tidy).

El dataset final tiene 1746 filas y 6 columnas: `anio`, `mes`, `sector`, `Produccion`, `empleados`, `establecimientos`.

---

## 🏗️ Estructura del Repositorio

```plaintext
├── data/
│   ├── raw/              <- Archivos Excel originales
│   ├── processed/        <- CSVs intermedios y finales
│
├── notebooks/
│   └── 01_exploracion_y_union_datasets.ipynb  <- Notebook principal de integración y limpieza
│
├── README.md             <- Este archivo


Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io


--------

<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>

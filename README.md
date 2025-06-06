# Predicción de la Producción Industrial Mensual por Sector en Tierra del Fuego

**Materia:** Aprendizaje Automático  
**Carrera:** Tecnicatura Superior en Ciencia de Datos e Inteligencia Artificial  
**Institución:** Politécnico Malvinas Argentinas  
**Alumno:** Luciano Luna  
**Año:** 2025

---

## Descripción del Proyecto

Este proyecto propone desarrollar un modelo de regresión supervisada capaz de predecir la producción industrial mensual en la provincia de Tierra del Fuego AeIAS, desagregada por sector. Para ello, se integraron tres fuentes de datos oficiales sobre empleo, establecimientos y producción industrial. Se busca identificar patrones entre las variables estructurales (empleo y establecimientos) y el comportamiento productivo de sectores clave como el electrónico, textil, plástico, entre otros.

---

## Objetivo

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

## Preguntas de Investigación

- ¿Es posible predecir el volumen de producción mensual en un sector a partir de las demás variables?
- ¿Cuáles son los sectores más sensibles a los cambios en empleo y cantidad de establecimientos?
- ¿Existen patrones estacionales o tendencias particulares en algunos sectores?

---

## Contexto y Relevancia

Tierra del Fuego posee una estructura productiva altamente concentrada en la industria manufacturera. La posibilidad de anticipar caídas o aumentos en la producción por sector representa una herramienta de gran utilidad para la planificación económica regional, el diseño de políticas públicas, y la toma de decisiones en sectores industriales estratégicos. Este proyecto transforma datos administrativos en información valiosa para la gestión y el análisis prospectivo.

---

## Modelo Propuesto

Este proyecto se enmarca en una tarea de **aprendizaje supervisado de tipo regresión**, cuyo objetivo es **predecir la cantidad mensual de producción industrial** por sector industrial en Tierra del Fuego.

Las variables independientes disponibles (`empleados`, `establecimientos`, `anio`, `mes`) permiten entrenar modelos de regresión con el objetivo de estimar la variable dependiente `produccion`.

Modelos sugeridos a utilizar:

- **Regresión Lineal Múltiple**
- **Árboles de Decisión para regresión**
- **Random Forest Regressor**
- **Regresión Ridge (regularizada)**

Estas técnicas permitirán evaluar tanto relaciones lineales como no lineales, y considerar posibles interacciones entre variables temporales y estructurales del sector industrial.

---



## Descripción de los Datasets

| Dataset | Fuente | Años | Variables principales |
|--------|--------|------|------------------------|
| **Producción Industrial por sector** | Instituto Provincial de Estadísticas y Censos (TDF AeIAS) | 2013–2025 | Año, mes, sector, volumen de producción |
| **Empleo en establecimientos industriales** | Instituto Provincial de Estadísticas y Censos (TDF AeIAS) | 2001–2025 | Año, mes, sector, empleados |
| **Cantidad de establecimientos industriales** | Instituto Provincial de Estadísticas y Censos (TDF AeIAS) | 2001–2025 | Año, mes, sector, establecimientos |


## Origen y Descarga de los Datos
Los datos fueron descargados desde el sitio oficial del Instituto Provincial de Estadísticas y Censos (IPEC) de Tierra del Fuego el día 13 de mayo de 2025.
Los archivos originales se encuentran en la carpeta data/raw del repositorio, con los siguientes nombres:

14_3_01_Personal_industria_rama-1.xlsx → Información mensual sobre personal ocupado en establecimientos industriales.

14_3_02_Establecimientos_industriales_rama-1.xlsx → Cantidad de establecimientos industriales por rama de actividad.

14_3_03_Produccion_Industrial-1-1.xlsx → Producción industrial mensual según rubro.

---

Los tres datasets fueron preprocesados para:
- Normalizar los nombres de sectores y meses.
- Unificar las estructuras.
- Resolver inconsistencias y valores nulos o atípicos.

---

---

## Estructura del Dataset Final

El dataset consolidado resultante contiene las siguientes variables:

| Variable          | Tipo de Dato | Descripción |
|------------------|--------------|-------------|
| `anio`           | int64        | Año del registro (2001 a 2025) |
| `mes`            | object       | Mes del registro (en minúsculas, e.g., `"enero"`) |
| `sector`         | object       | Sector industrial (e.g., `"Textiles"`, `"Pesqueras"`) |
| `Produccion`     | int32      | Producción total mensual del sector (en unidades, según sector) |
| `empleados`      | int32        | Cantidad de empleados del sector ese mes |
| `establecimientos` | int32      | Cantidad de establecimientos industriales activos ese mes |

El dataset final tiene por el momento 881 filas y 6 columnas: `anio`, `mes`, `sector`, `Produccion`, `empleados`, `establecimientos`.
Los tipos de datos fueron cuidadosamente transformados para garantizar compatibilidad con modelos de regresión y visualizaciones.

---
## Estructura de los Datasets Procesados

Tras la limpieza, unificación y validación de los tres datasets originales, se generaron los siguientes conjuntos de datos finales:

| Archivo CSV | Descripción |
|-------------|-------------|
| `produccion_total_por_sector_v2.csv` | Producción mensual por sector, normalizada y transformada |
| `empleados_total_por_sector_v2.csv` | Empleo mensual por sector, normalizado |
| `establecimientos_total_por_sector_v2.csv` | Cantidad de establecimientos activos por sector |
| `dataset_unificado_industria_v2.csv` | Unificación completa de los tres datasets, incluyendo valores nulos en producción antes de 2013 |
| `dataset_test_real.csv` | Registros sin datos de producción, reservados como casos reales para predicción |
| `dataset_final.csv` | Dataset final para entrenamiento supervisado, con registros completos de 2013 a 2025 |

El archivo `dataset_final.csv` será utilizado para entrenar y evaluar modelos de regresión supervisada.  
El archivo `dataset_test_real.csv` contiene observaciones sin valores de producción y se utilizará para realizar predicciones con el modelo una vez entrenado.



## Estructura del Repositorio - 2DA ENTREGA


├── data/
│   ├── raw/              <- Archivos Excel originales
│   ├── processed/        <- CSVs intermedios y finales
│
├── notebooks/
│   └── 01_exploracion_y_union_datasets.ipynb  <- Notebook principal de integración y limpieza
│
├── README.md             <- Este archivo

### Pasos realizados

1. **Carga de datos crudos:** se importaron 3 archivos `.xlsx` correspondientes a producción, empleo y establecimientos industriales por sector.

2. **Limpieza y transformación:**
   - Se identificaron estructuras no tabulares (por ejemplo, subtítulos, múltiples hojas y encabezados intermedios).
   - Se normalizaron columnas como `mes` y `sector` para asegurar la consistencia.
   - Se eliminaron columnas innecesarias y registros vacíos.
   - Se imputaron valores faltantes específicos en sectores como *Pesqueras*, aplicando interpolación manual basada en el promedio entre el mes anterior y el posterior.

3. **Unificación de datasets:**
   - Se realizó un `merge` progresivo de los tres datasets procesados usando como claves las variables `anio`, `mes` y `sector`.
   - Se mantuvieron los valores faltantes (`NaN`) en las columnas de producción en años donde no había datos disponibles.

4. **Exportación de datos:**
   - Cada dataframe intermedio fue exportado a la carpeta `data/processed/`.
   - A partir del dataset unificado, se separaron los registros sin producción (df_test) y se generó el dataset final (df_final) con información completa, que será utilizado para el entrenamiento de modelos supervisados.



---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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

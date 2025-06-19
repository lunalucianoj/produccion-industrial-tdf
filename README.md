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

------------

---

## Tercera Entrega: Presentación del Modelo y Análisis de Resultados

**Descripción:** Esta sección documenta el modelo final aplicado, el análisis exploratorio y la evaluación de resultados según lo solicitado en la entrega 3.

---

### Origen de los datos (resumen)

- Fuente: Instituto Provincial de Estadísticas y Censos (IPEC) – Tierra del Fuego AeIAS.
- Fecha de descarga: 13/05/2025.
- Archivos originales disponibles en `data/raw/`.
- Se combinaron 3 fuentes: producción, empleados y establecimientos industriales.

---

### Análisis exploratorio relevante

- Se separaron los sectores según la unidad de medida reportada: unidades o kilogramos.
- Se descartaron sectores con comportamiento errático o no explicable por variables estructurales:
  - **Otros** fue excluido del análisis en unidades.
  - **Plástica** fue excluido del análisis en kilogramos.
- Se detectaron correlaciones sólidas entre producción, empleo y establecimientos en los sectores **Electrónica**, **Confeccionista**, **Textil** y **Pesquera**.

---

### Modelo de Aprendizaje Automático aplicado

Se construyó un modelo supervisado de regresión estructurado en tres fases:

1. **Fase 1:** Modelos lineales y regularizados (Ridge, Lasso, ElasticNet).
2. **Fase 2:** Modelos no lineales (Árboles de decisión, Random Forest, KNN).
3. **Fase 3:** Validación cruzada (5-fold) para evaluar estabilidad y robustez.

---

### Modelos finales seleccionados

- **Modelo Ridge (conjunto en unidades):**  
  - Sectores: Confeccionista y Electrónica.  
  - Variables: empleados, establecimientos, año, dummy sector.  
  - Mejor desempeño general en test (R² = 0.918) y validación cruzada.

- **Modelo ElasticNet (conjunto en kilogramos):**  
  - Sectores: Textil y Pesquera.  
  - Variables: empleados, establecimientos, año, dummy sector.  
  - R² en test = 0.688. Mejor balance entre precisión y estabilidad en CV.

---

## Comparación Final de Modelos

Se resumen aquí los modelos seleccionados para cada sector y conjunto combinado. Los modelos generales fueron seleccionados para el análisis final por su mejor rendimiento en precisión y estabilidad, evaluados tanto por test como por validación cruzada.

| Sector / Conjunto      | Modelo Final     | R² (mejor test) | R² promedio (CV) | Comentario                                                   |
| ---------------------- | ---------------- | --------------- | ---------------- | ------------------------------------------------------------ |
| **Pesquera**           | ElasticNet       | 0.204           | -0.190           | Único modelo con R² positivo; resto con mal desempeño        |
| **Textil**             | Ridge Regression | 0.673           | -1.475           | Mejor R² en test; validación cruzada no favorable en general |
| **Electrónica**        | Ridge Regression | 0.642           | 0.547            | Mejor modelo y más estable en CV                             |
| **Confeccionista**     | ElasticNet       | 0.076           | 0.034            | Mejor entre todos los pobres resultados                      |
| **General Unidades**   | Ridge Regression | 0.918           | 0.872            | Mejor balance entre precisión y estabilidad                  |
| **General Kilogramos** | ElasticNet       | 0.688           | 0.317            | Único modelo robusto en CV                                   |

---

### Evaluación sobre test

Para cada modelo final se mostró:

- Comparación entre producción real y predicha.
- Histograma de errores residuales.
- Gráfico de residuos vs valores predichos.
- Curvas de evolución mensual (producción real vs modelo).

Sectores destacados:

- **Electrónica:** modelo Ridge general predice con alta precisión, bajo error y buena forma.
- **Pesquera:** modelo ElasticNet muestra alineamiento consistente con los datos reales.

---

### Predicción sobre datos reales sin producción

Se aplicaron ambos modelos sobre el conjunto `df_test`, que contiene datos de 2001–2012 sin información de producción.

- El modelo Ridge predice valores razonables y estables para Confeccionista y Electrónica.
- El modelo ElasticNet muestra un comportamiento diferenciado entre Textil (alta y estable) y Pesquera (más oscilante, pero coherente).

Este paso permite validar el modelo como herramienta útil para simular datos históricos o proyectar información faltante.

---

### Conclusiones finales

- Es posible predecir la producción mensual por sector industrial utilizando solo variables estructurales básicas (empleo, establecimientos y año).
- Los modelos generales con variables categóricas (dummy) permiten capturar diferencias sectoriales sin perder estabilidad.
- Se identificaron sectores más sensibles a cambios estructurales (Electrónica y Textil).
- El enfoque aplicado permite automatizar simulaciones históricas y mejorar la planificación basada en datos.

---



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

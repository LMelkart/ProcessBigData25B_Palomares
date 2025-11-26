# Predicción de Sobrecarga de Trabajo y Cuidados con ENUT usando PySpark
### Elaboró: Leon Palomares
### Matrícula: (puedes agregarla aquí)
### Maestría en Ciencia de Datos

Este proyecto implementa un flujo completo de machine learning usando PySpark para analizar la Encuesta Nacional de Uso del Tiempo (ENUT) y predecir la probabilidad de que una persona experimente sobrecarga alta de trabajo total (productivo + no remunerado + cuidados).

Incluye análisis exploratorio, ingeniería de variables, creación de una métrica social (SOBRECARGA_ALTA), preparación de datos, entrenamiento de un modelo de clasificación, evaluación mediante métricas robustas (ROC y PR), visualizaciones y conclusiones interpretativas desde una perspectiva social.

### Objetivo del proyecto

Construir un modelo de clasificación capaz de identificar quiénes presentan sobrecarga alta de tiempo, integrando:

* horas dedicadas a trabajo para el mercado

* horas de trabajo doméstico no remunerado

* horas de cuidado

* horas de apoyo a otros hogares

* variables sociodemográficas (sexo, edad, tipo de localidad)

Los objetivos son:

✔ Analizar desigualdades en uso del tiempo
✔ Incorporar conceptos de desigualdad de género y cuidados
✔ Construir una métrica social: SOBRECARGA_ALTA (1/0)
✔ Entrenar un modelo de ML para predecir sobrecarga
✔ Interpretar cuáles variables explican mejor la desigualdad
✔ Generar visualizaciones y análisis exploratorio

### Pipeline de Modelado
#### 1. Carga de datos

Se cargaron los módulos de la ENUT:

tvar_crea → variables de uso del tiempo (minutos)

tsdem → características sociodemográficas

tmodulo → validación de tiempos reportados

Los datos se cargan a Spark como DataFrames y se preparan mediante joins.

#### 2. Limpieza y preparación
Acciones realizadas:

Eliminación de columnas duplicadas o irrelevantes

Conversión a formato numérico

Manejo de valores nulos mediante imputación o reemplazo por 0

Validación de consistencia temporal (no exceder 1440 minutos diarios)

Exclusión de variables

Se eliminaron variables que incluían cuidados pasivos para evitar doble contabilización:

ACTIV_PROD_CON_CP

CUID_INT_*_CON_CP

CUID_ESP_INT_HOG_CON_CP

etc.

También se descartaron variables agregadas redundantes como:

ACTIV_PROD_SIN_CP

ACTIV_MERC

#### 3. Construcción de la métrica SOBRECARGA

#### 4. Selección de características

Se incluyeron variables de:

✔ Trabajo productivo

TRAB_MERC_PV, TRAS_TRAB, BUS_TRAB, PROD_BIEN_TRAB_AUTO

✔ Trabajo no remunerado doméstico

TRAB_NO_REM_HOG, PREP_SERV_ALIM, LIMP_VIV, LIMP_ROP, MANT_VIV, COMPRAS_HOG, PAGOS_TRAM_HOG, ORG_SUP_HOG

✔ Cuidado directo

TRAB_NO_REM_CUID_HOG, CUID_INT_0A5_SIN_CP, CUID_INT_6A14_SIN_CP, CUID_INT_15A59, CUID_INT_60MAS_SIN_CP

✔ Apoyo a otros hogares

APOY_HOG_FAM, TRAB_NO_REM_OTROS_HOG, TRAB_DOM_OTROS_HOG_FAM, CUID_ESP_DISC_ENF, CUID_PER_OTROS_HOG, TRAB_NO_REM_NO_FAM

✔ Sociodemográficas

SEXO
EDAD
TLOC (tipo de localidad)

#### 5. Ensamble y escalado

Se utilizó:

VectorAssembler para crear el vector de entrada

StandardScaler para normalizar los datos

Esto mejora estabilidad y desempeño en modelos lineales.

#### 6. Entrenamiento del modelo

#### 7. Evaluación del modelo

Se calcularon:

Accuracy

Área bajo la curva ROC

Curva Precision–Recall
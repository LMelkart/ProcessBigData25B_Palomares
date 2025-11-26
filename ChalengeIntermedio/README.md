# Predicción de Calidad del Vino con PySpark
#### Elaboró: Leon Palomares
#### Matricula: 325057406
#### Maestría en Ciencia de Datos


Este proyecto implementa un flujo completo de Machine Learning usando PySpark para predecir si un vino tiene alta calidad (≥ 7) utilizando los datasets de vino tinto y vino blanco del repositorio UCI.

Incluye análisis exploratorio, ingeniería de características, escalado, entrenamiento, evaluación con métricas avanzadas (ROC y Precision-Recall), así como visualizaciones y conclusiones del modelo.

## 📂 Estructura del proyecto

/ProyectoVinos
│── data/
│     ├── winequality-red.csv
│     ├── winequality-white.csv
│
│── notebook/
│     ├── ChallengeIntermedio.ipynb
│
│── README.md

## Objetivo del proyecto

Desarrollar un modelo de clasificación que permita identificar si un vino es de alta calidad, basándose en sus características físico-químicas: 

•	Fixed acidity (acidez fija)
•	Volatile acidity (acidez volátil)
•	Citric acid (ácido cítrico)
•	Residual sugar (azúcar residual)
•	Chlorides (cloruros)
•	Free sulfur dioxide (SO₂ libre)
•	Total sulfur dioxide (SO₂ total)
•	Density (densidad)
•	pH
•	Sulphates (sulfatos)
•	Alcohol


Para esto se busca:

* Unificar los datasets de vino tinto y blanco.

* Realizar limpieza y transformación de datos.

* Construir un pipeline reproducible de ML.

* Evaluar el rendimiento usando métricas robustas.

* Interpretar curvas ROC y Precision-Recall.

* Explorar relaciones entre variables mediante matriz de correlación.

## Requisitos
🔧 Dependencias instalables con pip:

pyspark
pandas
numpy
matplotlib


## Pipeline de Modelado
### 1. Carga y unión de datos

Los datasets “red” y “white” se cargan como DataFrames Spark y se unen usando unionByName.

### 2. Limpieza y preparación
Eliminación de columnas no necesarias
Conversión de tipos
Creación de columna objetivo label:

1 → calidad ≥ 7
0 → calidad < 7

### 3. Selección de características

Se seleccionan únicamente las columnas numéricas relevantes.

### 4. Ensamble y escalado

'VectorAssembler' para producir el vector de entrada
'StandardScaler' para normalizar variables y mejorar el desempeño del modelo

### 5. Entrenamiento

Se emplea:
LogisticRegression (modelo base)
División de datos 82% entrenamiento / 18% prueba

### 6. Evaluación

Se utiliza:
Accuracy
Precision, Recall y F1
Curva ROC y AUC
Curva Precision-Recall
Matriz de correlación

### Resultados principales
Matriz de correlación

La matriz evidencia:
Variables fuertemente correlacionadas (p. ej. densidad ↔ alcohol)
Relaciones directas e inversas con la calidad
Potenciales redundancias en las características
Variables que deberían revisarse para feature selection
Esto ayuda a detectar multicolinealidad y posibles mejoras del modelo.

Curva ROC

La curva ROC muestra:
Qué tan bien separa el modelo las clases
Un AUC cercano a 1 implica excelente capacidad de discriminación
Si el AUC es moderado, indica que se puede mejorar con otros modelos o balanceo de clases

Curva Precision-Recall
Particularmente útil cuando hay clases desbalanceadas.
Interpretación:
Alta a la izquierda ⇒ el modelo detecta bien los positivos con bajo nivel de falsos positivos
Si luego desciende ⇒ el modelo pierde precisión cuando intenta aumentar el recall
PR más sensible al desbalance que la ROC
Idealmente: se quiere una curva que permanezca lo más arriba posible.

📈 Métricas finales (ejemplo)

Métrica	Resultado
Accuracy	0.8255
<img width="630" height="470" alt="imagen" src="https://github.com/user-attachments/assets/15f74c8a-1d93-4f5c-b6a7-6efac011f5b1" />
AUC ROC	0.8266

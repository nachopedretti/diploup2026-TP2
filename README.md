# TP2 – Smoking Prediction

Desarrollar un modelo de Machine Learning para predecir si una persona es fumadora o no, utilizando distintas características de salud.

## Desarrollo

Dividí el trabajo en 6 notebooks, como fue indicado:

### 01 – Lectura y Discovery

Cargué los datos y revisé su estructura, tipos de variables, valores faltantes y distribución de fumadores y no fumadores.

### 02 – EDA

Luego del análisis de las variables encontré diferencias en algunas características de salud y también una relación importante entre género y smoking.

Casi ninguna mujer fuma en la base original. Esto puede llegar a tomarse como una variable muy importante a la hora de la predicción. Durante todo el trabajo me pregunté si convenía tomar esta variable para la futura predicción o eliminarla para que no pondere tanto la decisión de si fuma o no.

### 03 – Preprocesamiento

Preparé los datos para entrenar los modelos. Separé Train y Test, transformé las variables categóricas en binarias y dejé los conjuntos con las mismas 24 características.

### 04 – Entrenamiento y Optimización

Probé distintas versiones de Random Forest y Regresión Logística. Random Forest obtuvo buenos resultados, pero probando varias combinaciones no podía bajar lo suficiente el overfitting.

Finalmente me quedé con Regresión Logística, que si bien bajó un poco el Accuracy, redujo bastante el overfitting.

### 05 – Validación

Comparé los resultados en Train y Test. Elegí Regresión Logística balanceada con umbral 0.55 por su estabilidad y Recall elevado.

Encontré una limitación importante: el modelo no logró identificar mujeres fumadoras. Después de varias pruebas, decidí mantener las 24 variables y dejar esta observación para futuras mejoras.

### 06 – Predicción

Utilicé el modelo elegido para predecir los 5.692 registros de entrega.

Obtuve 3.231 fumadores y 2.461 no fumadores. Exporté el archivo `smoking_predictions.csv` con los resultados.

## Modelo seleccionado

Elegí **Regresión Logística balanceada**, con umbral **0.55**, utilizando 24 variables.

Resultados en Test:

- Accuracy: 72,36%
- Precision: 57,89%
- Recall: 90,23%
- F1-score: 70,53%

**TRAIN**

```text
              precision    recall  f1-score   support

           0       0.91      0.62      0.74     25337
           1       0.58      0.90      0.70     14663

    accuracy                           0.72     40000
   macro avg       0.74      0.76      0.72     40000
weighted avg       0.79      0.72      0.73     40000
```

**TEST**

```text
              precision    recall  f1-score   support

           0       0.92      0.62      0.74      6334
           1       0.58      0.90      0.71      3666

    accuracy                           0.72     10000
   macro avg       0.75      0.76      0.72     10000
weighted avg       0.79      0.72      0.73     10000
```

Elegí este modelo por su estabilidad entre Train y Test, evitando el overfitting observado en Random Forest. Con este último probé diferentes combinaciones de parámetros para intentar reducirlo, pero no logré los resultados que buscaba.

## Limitaciones

Encontré una diferencia importante en las predicciones por género. El modelo no logró identificar mujeres fumadoras en Test, mientras que en hombres alcanzó un Recall del 93,92%.

El modelo le da mucho peso al género para decidir si una persona fuma o no. Pensé en eliminar esta variable, pero finalmente decidí mantenerla, ya que en la base original la proporción de mujeres fumadoras es mucho menor que la de hombres.

Decidí mantener las 24 variables y dejar esta limitación identificada para futuras mejoras.

## Resultado final

Predicciones sobre 5.692 registros:

- 3.231 fumadores.
- 2.461 no fumadores.

El archivo final es `results/smoking_predictions.csv`, con las columnas `ID` y `smoking_prediction`.

## Estructura del repositorio

- `notebooks/`: las 6 notebooks del trabajo.
- `data/raw/`: datos originales.
- `data/processed/`: datos procesados.
- `models/`: modelos entrenados.
- `results/`: predicciones finales.
- `requirements.txt`: dependencias del proyecto.

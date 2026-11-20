# Spaceship Titanic — Clasificación con Redes Neuronales Artificiales

## 1. Descripción del proyecto

Este proyecto tiene como objetivo desarrollar un modelo de Machine Learning basado en redes neuronales artificiales para predecir si los pasajeros de la nave *Spaceship Titanic* fueron transportados a otra dimensión.

Para realizar esta predicción, utilizamos información sobre las características de los pasajeros, como su edad, planeta de origen, destino, estado de criosueño, ubicación de su cabina y gastos realizados durante el viaje.

El problema corresponde a una **clasificación binaria supervisada**, ya que buscamos predecir la variable `Transported`, que puede tomar dos valores:

- `True`: el pasajero fue transportado.
- `False`: el pasajero no fue transportado.

## 2. Objetivo

Construir, entrenar y evaluar una red neuronal artificial que permita clasificar a los pasajeros a partir de sus características, utilizando técnicas de análisis exploratorio, preprocesamiento e ingeniería de características.

También buscamos comparar diferentes arquitecturas de redes neuronales para identificar una configuración que presente un buen equilibrio entre desempeño predictivo y complejidad.

## 3. Conjunto de datos

Se utilizó el dataset **Spaceship Titanic**, compuesto por tres archivos:

| Archivo | Descripción |
|---|---|
| `train.csv` | 8,693 pasajeros con la variable objetivo |
| `test.csv` | 4,277 pasajeros sin la variable objetivo |
| `sample_submission.csv` | Ejemplo del formato de entrega |

Entre las variables utilizadas se encuentran `HomePlanet`, `CryoSleep`, `Cabin`, `Destination`, `Age`, `VIP` y los gastos en servicios de la nave.

La variable objetivo es `Transported`.

## 4. Metodología

### Análisis exploratorio de datos (EDA)

Se revisaron las dimensiones de los conjuntos de datos, los tipos de variables, los valores faltantes, las distribuciones y las relaciones entre las características de los pasajeros.

Entre los principales hallazgos encontramos:

- El 24.01% de los pasajeros de entrenamiento tenía al menos un valor faltante.
- La variable `Transported` estaba prácticamente balanceada.
- Los pasajeros en criosueño presentaron una mayor proporción de transporte.
- Se identificaron diferencias en las proporciones de transporte según el planeta de origen.
- Los pasajeros transportados tendieron a registrar menores gastos en los servicios analizados.

### Preprocesamiento

Se aplicaron técnicas de preparación de datos para convertir las variables originales en características numéricas compatibles con una red neuronal.

Los procedimientos principales fueron:

1. Imputación de valores faltantes mediante mediana y moda.
2. Extracción de características de `PassengerId` y `Cabin`.
3. Codificación de variables categóricas mediante One-Hot Encoding.
4. Estandarización de variables numéricas mediante StandardScaler.
5. División estratificada de los datos en entrenamiento (80%) y validación (20%).

Después del preprocesamiento obtuvimos **28 características numéricas**.

## 5. Arquitectura de la red neuronal

Se desarrolló una red neuronal multicapa (*Multilayer Perceptron*, MLP) utilizando TensorFlow y Keras.

Se compararon tres arquitecturas:

| Modelo | Arquitectura | Parámetros |
|---|---|---:|
| A — Inicial | 28 → 32 → 16 → 1 | 1,473 |
| B — Simple | 28 → 16 → 1 | 481 |
| C — Amplio | 28 → 64 → 32 → 1 | 3,969 |

La arquitectura seleccionada fue el **Modelo B**, que utiliza:

- 28 características de entrada.
- Una capa oculta de 16 neuronas con activación ReLU.
- Una neurona de salida con activación Sigmoid.
- Optimizador Adam con learning rate de 0.001.
- Función de pérdida Binary Crossentropy.

## 6. Resultados

Los modelos se evaluaron con un conjunto de validación de 1,739 pasajeros.

| Modelo | Accuracy | Precision | Recall | F1-score |
|---|---:|---:|---:|---:|
| A — Inicial | 80.51% | 81.33% | 79.57% | 80.44% |
| B — Simple | 80.45% | 80.04% | 81.51% | 80.77% |
| C — Amplio | 80.28% | 81.99% | 77.97% | 79.93% |

El Modelo A obtuvo el mayor accuracy, mientras que el Modelo B consiguió el mejor F1-score y recall, utilizando una cantidad menor de parámetros.

Por esta razón, seleccionamos el Modelo B para generar las predicciones finales.

### Matriz de confusión del Modelo B

| Resultado | Pasajeros |
|---|---:|
| Verdaderos negativos | 685 |
| Falsos positivos | 178 |
| Falsos negativos | 162 |
| Verdaderos positivos | 714 |

El modelo clasificó correctamente a 1,399 de los 1,739 pasajeros de validación.

## 7. Predicciones finales

Una vez seleccionada la arquitectura, se entrenó nuevamente la red neuronal utilizando los 8,693 registros etiquetados.

El entrenamiento definitivo se realizó durante 59 épocas y obtuvo un accuracy de entrenamiento de 81.64%.

Posteriormente, se generaron predicciones para los 4,277 pasajeros del conjunto `test.csv`.

Los resultados se almacenaron en `submission.csv`, respetando el formato solicitado.

## 8. Tecnologías utilizadas

- Python
- Google Colab
- Pandas y NumPy
- Matplotlib y Seaborn
- Scikit-learn
- TensorFlow y Keras
- SciPy
- GitHub

## 9. Conclusiones

Durante el desarrollo del proyecto comprobamos que el análisis exploratorio y el preprocesamiento son etapas importantes para construir un modelo de clasificación.

También observamos que aumentar el número de capas o neuronas no necesariamente mejora el rendimiento de una red neuronal.

El Modelo B permitió obtener un accuracy de validación de 80.45% y un F1-score de 80.77%, utilizando únicamente 481 parámetros entrenables.

Estos resultados muestran que una arquitectura relativamente sencilla puede ofrecer un desempeño competitivo dentro de los modelos evaluados.

Finalmente, logramos desarrollar un proceso completo de Machine Learning, desde la exploración de los datos hasta la generación de predicciones para nuevos pasajeros.

## 10. Archivos del proyecto

| Archivo | Contenido |
|---|---|
| `Spaceship_Titanic.ipynb` | Análisis, preprocesamiento, entrenamiento y evaluación |
| `submission.csv` | Predicciones finales |
| `requirements.txt` | Dependencias del proyecto |
| `README.md` | Documentación general |

---

**Proyecto académico — Redes Neuronales Artificiales.**

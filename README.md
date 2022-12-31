### Diplomado en Introducción a la Ciencia de Datos con Python

## Proyecto: Proyeccion de diabetes
Carmen Diaz

Utilize el proceso CRISP-DM https://es.wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining

CRISP-DM divide el proceso de minería de datos en seis fases principales:4 

## Comprensión del negocio

El accidente cerebrovascular es un importante problema de salud pública que conduce a un aumento de la mortalidad. Los factores de riesgo modificables para el accidente cerebrovascular incluyen hipertensión, diabetes, tabaquismo y abuso de alcohol. Entre estos factores de riesgo, la diabetes y la hipertensión van en rápido crecimiento conduciendo a un aumento sustancial de las enfermedades cardiovasculares y los accidentes cerebrovasculares.

El Dataset, obtenido de Kaggle, incluye data sobre diabetes, hipertension y stroke.


## Preparación de los datos

Se codificaron las variables categoricas con OneHotEncoder (por cada categoria un valor de 1) y las numericas se estandarizaron con StandardScaler (z-score). El particionado del dataset se hizo en 80% de entrenamiento y 20% de test (holdout)

Se definio un pipeline para hacer este pre-procesamiento de datos. 

## Fase de Modelado

Al Pipeline se agregó el algoritmo clasificador xgboost. El entranamiento se hizo usando validación cruzada con 5 folders, y se utilizó para el hyper parameter tunning `RandomizedSearchCV`.

## Evaluación 


Al hacer la evaluacion se obtuvieron las siguientes metricas en los datos de test (holdout) o sea los datos que no conoce el modelo. Note: Utilicé un threshold de 0.5

- Accuracy = 0.76
- Precision 0.74
- Recall 0.79
- F1 0.76

El area bajo la curva ROC es 0.832.


## Implementación

Para usar en la implementación se guardo el pipeline que contenia el pre-procesamiento de las variables y el modelo en si. El Pipeline fue serializado (guarda en forma binaria) con el formato pickle de python.

Como demo de implementación se recuperó el pipeline serializado y se hizo predicciones con los datos de test (holdout). Para hacer la predicción se invoca el método `predict_proba` del pipeline citado.

Este método puede ser también expuesto en una REST API usando, por ejemplo los frameworks de Python Flask o FastAPI


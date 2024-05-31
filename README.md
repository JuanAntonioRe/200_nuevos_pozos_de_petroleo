# 200 pozos nuevos de petróleo :rocket:

Este es un proyecto para poner en práctica el **Aprendizaje automático en negocios**. Esto significa que se va a determinar si el modelo es rentable o no.

Se hace uso de la técnica de bootstrapping.

## Descripción del proyecto
Una compañía de extracción de petróleo llamada OilyGiant quiere abrir 200 pozos nuevos.

Hay 3 datasets que tienen datos sobre muestras de crudo de tres regiones, cada dataset corresponde a una región. Ya se conocen los parámetros de cada pozo petrolero de cada región.

La tarea es crear un modelo que ayude a elegir la región con el mayor margen de beneficio, analizando los beneficios y riesgos potenciales utilizando la técnica bootstrapping.

Para este proyecto contamos son estas condiciones:
* El presupuesto para el desarrollo de 200 pozos petroleros es de 100 millones de dólares.
* Un barril de materias primas genera 4.5 USD de ingresos. El ingreso de una unidad de producto es de 4500 dólares (el volumen de reservas está expresado en miles de barriles).
* Después de la evaluación de riesgo, se mantendrán solo las regiones con riesgo de pérdidas inferior al 2.5%. De las que se ajustan a los criterios, se debe seleccionar la región con el beneficio promedio más alto.

## Objetivo
Al tratarse de un modelo para calcular la mayor ganancia, tenemos una tarea de regresión lineal.

Los 3 datasets tienen las mismas columnas:
* id — identificador único de pozo de petróleo
* f0, f1, f2 — tres características de los puntos (su significado específico no es importante, pero las características en sí son significativas)
* product — volumen de reservas en el pozo de petróleo (miles de barriles).

Nuestro objetivo es la columna `'product'` porque el mayor volúmen de reserva nos dará un mayor margen de ganancia.

## Desarrollo del proyecto
### Descarga y preparación de los datos.
Se importaron los datos utilizando Pandas revisando si hay valores ausentes o duplicados y se explica como se procesaron. Además se explica la eliminación de columnas que no contienen información útil para el modelo.

### Entrenamiento y prueba el modelo para cada región
Se dividen los datos en un conjunto de entrenamiento y un conjunto de validación con una proporción de 75:25

Posteriormente se entrena el modelo y se hacen predicciones para el conjunto de validación.

Se muestra el volumen medio de reservas predicho y el valor RMSE del modelo.

Finalmente se analizan los resultados.

### Cálculo de ganancias
Dada la inversión de 100 millones por 200 pozos petrolíferos, de media un pozo petrolífero debe producir al menos un valor de 500,000 dólares en unidades para evitar pérdidas (esto es equivalente a 111.1 unidades). 

Se compara esta cantidad con la cantidad media de reservas en cada región.

Se eligen los 200 pozos con los valores de predicción más altos de cada una de las 3 regiones.

Almacena las predicciones para los 200 pozos para cada una de las 3 regiones.

Cálculo de la ganancia potencial de los 200 pozos principales por región.

### Riesgo de pérdidas
Se emplea la técnica del bootstrapping con 1000 muestras para hallar la distribución de los beneficios.

Encontrar el beneficio promedio, el intervalo de confianza del 95% y el riesgo de pérdidas.

## Conclusiones
Haciendo uso del método de bootstrapping, la **región 1** es la región que tuvo mayor beneficio promedio (139 milllones de dólares), la que tiene el intervalo de confianza de 95% más grande (de 139 a 140 millones de dólares) y no hay riesgo de pérdida. Por lo que la región 1 es la mejor para invertir los 100 millones de dólares.

Con esto decimos que nuestro modelo funcionó correctamente, es decir, es rentable.

## Tecnologías usadas
* Pandas
* Numpy
* sklearn: 
    + train_test_split
    + LinearRegression
    + mean_squared_error
    + StandardScaler
# Documentación del entregable de Análisis Exploratorio y Curación de Datos

## Criterios de exclusión de ejemplos
1. Se eliminan ejemplos donde el tamaño de la construcción es menor a 66,93 (percentil 1%) y es mayor a 294 (percentil 95%).
2. Se eliminan ejemplos que tengan más de 5 habitaciones (ejemplos de 6 habitaciones o más representan menos del 1% del total).

## Criterios de inclusión de ejemplos
1. Se incluyeron columnas procesadas desde el conjunto de datos de Airbnb con información sobre: la mediana del precio diario, la mediana del precio semanal, y la mediana del   precio mensual, para aquellos ejemplos de dicho conjunto de datos donde la cantidad de casos para el zipcode sea mayor a 1.

## Características seleccionadas

### Características categóricas: se seleccionaron utilizando la Razón de correlación (eta) con valores de a pares mayores a 0.4.
1. Type: tipo de propiedad. 3 valores posibles
2. Suburb: Suburbio. 314 valores posibles.
3. SellerG: Agente Inmobiliario (vendedor). 268 valores posibles.
4. CouncilArea: Consejo de gobierno de la zona. 33 valores posibles.
5. Postcode: Código Postal.
Todas las características categóricas fueron codificadas con un método OneHotEncoding previo tratamiento de valores faltantes de la variable CouncilArea.

### Características numéricas: se seleccionaron utilizando el Coeficiente de correlación de Pearson (r) con valores de a pares |r|>0.5.
1. Rooms: Cantidad de habitaciones.
2. Distance: Distancia al centro de la ciudad.
3. BuildingArea: Área construida.
4. Propertycount: Número de propiedades que existen en el suburbio.
5. Latitude: Latitud.
6. Longitude: Longitud.
7. YearBuilt: Año de construcción.
8. Car: número de cocheras.


### Transformaciones:

1. Todas las columnas numéricas fueron estandarizadas utilizando StandardScaler para imputación de valores faltantes por medio de KNN.
2. Los valores faltantes de CouncilArea fueron imputados de forma manual a apartir de los valores de Postcode.
3. Los valores faltantes de las columnas 'YearBuilt', ‘BuildingArea’, ‘airbnb_price_median’, ‘airbnb_weekly_price_median’ y ‘airbnb_monthly_price_median’ fueron imputadas utilizando KNN con K=5 y considerando sólo variables numéricas (no todo el dataset).
4. En PCA se compara el método realizando un escalado en el intervalo [0,1] mediante MinMaxScaler (previo KNN con MinMaxScaler y k=5) y por otro lado con los datos estandarizados. La varianza explicada por las 3 primeras componentes del método es mayor aplicando escalado en lugar de estandarizado.

### Datos aumentados:

a) Se enriqueció la base de datos de Melb utilizando datos de la plataforma AirBnB de la siguiente forma:

1. Se agruparon los datos de AirBnB por Zipcode; se calculó la mediana de las variables price, weekly_price y monthly_price y se generaron las siguientes variables:
   1.1 airbnb_price_median: mediana del precio diario de publicaciones de la plataforma AirBnB en el mismo código postal.
   1.2 airbnb_weekly_price_median: mediana del precio semanal de publicaciones de la plataforma AirBnB en el mismo código postal.
   1.3 airbnb_monthly_price_median: mediana del precio mensual de publicaciones de la plataforma AirBnB en el mismo código postal.
2. Se crea un nuevo dataframe con las variables 1.1, 1.2,1.3 y Zipcode.
3. Se realiza un left merge usando las variables PostCode de la base de datos de Melb y zipcode AirBnB. Se dropea a la variable zipcode y a este dataset se lo guarda como melb_data_complet.csv para trabajos siguientes.

b) Se agregan a melb_data_complet.csv las 3 primeras columnas obtenidas a través del método de PCA, aplicado sobre el conjunto de datos totalmente procesado. Estas 3 columnas se denotan por pca1, pca2 y pca3 viendose reflejadas en las 3 últimas columnas del dataset final.
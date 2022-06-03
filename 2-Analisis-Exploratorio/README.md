# Documentación del entregable de Análisis Exploratorio y Curación de Datos

## Criterios de exclusión de ejemplos
1. Se eliminan ejemplos donde el tamaño de la construcción es menor a 66,93 (percentil 1%) y es mayor a 294 (percentil 95%).
2. Se eliminan ejemplos que tengan más de 5 habitaciones (ejemplos de 6 habitaciones o más representan menos del 1% del total).

## Criterios de inclusión de ejemplos
1. Se incluyeron columnas procesadas desde el conjunto de datos de Airbnb con información sobre: la mediana del precio diario, la mediana del precio semanal, y la mediana del   precio mensual, para aquellos ejemplos de dicho conjunto de datos donde la cantidad de casos para el zipcode sea mayor a 1.

## Características seleccionadas

### Características categóricas
1. Type: tipo de propiedad. 3 valores posibles
2. Suburb: Suburbio. 314 valores posibles.
3. SellerG: Agente Inmobiliario (vendedor). 268 valores posibles.
4. CouncilArea: Consejo de gobierno de la zona. 33 valores posibles.
Todas las características categóricas fueron codificadas con un método OneHotEncoding.

### Características numéricas
1. Rooms: Cantidad de habitaciones.
2. Distance: Distancia al centro de la ciudad.
3. BuildingArea: Área construida.
4. Propertycount: Número de propiedades que existen en el suburbio.
5. Latitude: Latitud
6. Longitude: Longitud
7. YearBuilt: Año de construcción
8. airbnb_price_median: Se agrega la mediana del precio diario de publicaciones de la plataforma AirBnB en el mismo código postal.
9. airbnb_weekly_price_median: Se agrega la mediana del precio semanal de publicaciones de la plataforma AirBnB en el mismo código postal.
10. airbnb_monthly_price_median: Se agrega la mediana del precio mensual de publicaciones de la plataforma AirBnB en el mismo código postal.

### Transformaciones:
1. Todas las columnas numéricas fueron escaladas en el intervalo [0,1].
2. Las columnas 'YearBuilt', ‘BuildingArea’, ‘airbnb_price_median’, ‘airbnb_weekly_price_median’ y ‘airbnb_monthly_price_median’ fueron imputadas utilizando KNN con K=5.

### Datos aumentados
1. Se agregan las 3 primeras columnas obtenidas a través del método de PCA, aplicado sobre el conjunto de datos totalmente procesado.
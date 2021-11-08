# Informe de Segundo Proyecto
Tema:
* Mapas de covid

Integrantes:
* Jean Paul Rodriguez Flores
* Jose Mauricio Muñoz Morera

## Proceso de generacion de mapas
Pasos para la creacion de los mapas:

1. Primero se edito el archivo cantones.dbf para insertarle dos filas correspondientes a cada los casos positivos y las muertes por covid de cada canton.

2. Luego se importo el shapefile de cantones a grass

3. Se crearon 10000 puntos aleatorios retenidos por el area total de los cantones

4. Se le anadio la categoria y atributos de los cantones a los puntos creados anteriormente

5. Se edito el numero de columnas y filas de la region a 1000 para que la interpolacion no durara tanto

5. Se utilizo la interpolacion por curvas spline para crear el heatmap

6. Se eligio la tabla de color a utilizar

7. Se re-escalo el mapa para poder exportarlo en formato de 8 bits de geotiff

8. Se exporto en formato geotiff

9. Se importo en Mapbox para la representacion del mapa en web


## Criterios utilizados
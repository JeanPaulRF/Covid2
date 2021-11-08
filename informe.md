# Informe de Segundo Proyecto
Tema:
* Mapas de covid

Integrantes:
* Jean Paul Rodriguez Flores
* Jose Mauricio Muñoz Morera

Link de la pagina:
https://jeanpaulrf.github.io/Covid2/

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

9. Se importo el shp de las clinicas y hospitales (el de escuelas no funcionaba)

10. Se extrayeron los cantones con el valor de casos positivos y muertes mas altos

11. Se extrayeron los puntos de las clinicas y hospitales con relacion espacial sobre los cantones previamente obtenidos

12. Se importaron las capas en Mapbox para la representacion de los mapas en web


## Criterios utilizados

v.import

v.random restrict=geo_cantones output=puntosCovid npoints=10000 layer=1

v.category

v.surf.idw input=puntosRandomCategory  output=puntosCasosCategory npoints=5 column=geo_cantones_CASOS

r.colors

r.rescale

v.extract input=geo_cantones output=cantonesMax where="CASOS > 200"

v.extract input=geo_cantones output=cantonesMax where="MUERTES > 200"

v.select ainput=clinicas2008crtm05_WGS_84 binput=cantonesMaxMuertes output=clinicasMaxMuertes operator=overlap

v.select ainput=hospitales2008crtm05 binput=cantonesMaxMuertes output=hospitalesMaxMuertes operator=overlap


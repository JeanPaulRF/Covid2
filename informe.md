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

1. Primero se editó el archivo cantones.dbf para insertarle dos filas correspondientes a cada los casos positivos y las muertes por CoVid-19 de cada cantón.

2. Luego se importó el shapefile de cantones a grass

3. Se crearon 10 puntos por cada cantón aleatorios retenidos por el area total de los cantones

4. Se le añadio la categoria y atributos de los cantones a los puntos creados anteriormente

5. Se edito el número de columnas y filas de la region a 1000 para que la interpolación no durara tanto

5. Se utilizó la interpolacion por curvas spline para crear el heatmap

6. Se re-escaló el mapa para poder exportarlo en formato de 8 bits de geotiff

7. Se eligió la tabla de color a utilizar

8. Se exportó en formato geotiff

9. Se importo el shp de las clínicas, hospitales y escuelas.

10. Se extrajeron los cantones con el valor de casos positivos y muertes más altos

11. Se extrajeron los puntos de las clínicas, hospitales y escuelas con relacion espacial sobre los cantones previamente obtenidos

12. Se exportaron estas capas en formato de shapefile, para luego en GDAL convertirlos a geojson con el formato aceptado en MapBox (Cordenadas mayores que -360 y menores que 360)

13. Para utilizar el GeoTiff en MapBox se tuvo que comprimir usando la técnica de compresión LZW en GDAL.

14. Se creó un estilo en MapBox con el raster.


## Criterios utilizados

v.import

v.random restrict=geo_cantones output=puntosCovid npoints=10 layer=1 -a

v.category

v.surf.rst in=puntosCovid elev=CasosSpline zcolumn=geo_cantones_CASOS

v.surf.rst in=puntosCovid elev=MuerteSpline zcolumn=geo_cantones_MUERTES

r.rescale

r.colors

v.extract input=geo_cantones output=cantonesMax where="CASOS > 20000"

v.extract input=geo_cantones output=cantonesMax where="MUERTES > 300"

v.select ainput=clinicas2008crtm05_WGS_84 binput=cantonesMaxMuertes output=clinicasMaxMuertes operator=overlap

v.select ainput=hospitales2008crtm05 binput=cantonesMaxMuertes output=hospitalesMaxMuertes operator=overlap


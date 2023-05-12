# Tutorial de Simulation of Urban Mobility - SUMO

Este proyecto tiene como objetivo proporcionar un tutorial basico cómo utilizar SUMO con datos de OpenStreetMap para generar viajes tanto del transporte privado y publico.

## Estructura de carpetas

El proyecto sigue la siguiente estructura de carpetas:

- `data/`: Contiene los archivos de datos necesarios.
  - `sanjuandelurigacho.osm`: Archivo OpenStreetMap descargado para la simulación.
  - `randomtrips.py`: Archivo Python para generar viajes aleatorios con RandomTrips.
  - `pt2flow.py`: Archivo Python para generar rutas con pt2flow.
  - `results/`: Carpeta para almacenar los resultados generados.

- `sumo/`: Carpeta de archivos de SUMO.
  - `net.net.xml`: Red generada a partir de `sanjuandelurigacho.osm`.
  - `routes.rou.xml`: Viajes de vehiculo ligeros en la red generada a partir de `randomtrips.py`.
  - `pt2flow.py`: Viajes de vehiculo de transporte publico en la red generada a partir de `pt2flow.py`.
  - `configuration.sumocfg`: Archivo de configuracion de sumo.

- `README.md`: Archivo que contiene información sobre el proyecto y su uso.

- `requirements.txt`: Archivo que especifica las dependencias del proyecto.

## Requerimientos

1. Descargar el repositorio desde [https://github.com/yeltsinvc/SUMO_TUTORIAL](https://github.com/yeltsinvc/SUMO_TUTORIAL). Descomprime el repositorio.
2. Instale [SUMO](https://www.eclipse.org/sumo/).
3. Instale un editor y/o alguna plafaforma que permita trabajar con python. En el caso de editor de codigo se recomienda [Visual Studio Code](https://code.visualstudio.com/updates/v1_78) y para el caso de plataformar utilizar [Spyder de Anaconda](https://www.anaconda.com/download)

## Tutorial Basico
### 1. Conversion del archivo osm a una red en SUMO.
Una vez descargado el repositorio para crear la red sumo, utilizaremos `netconvert` en la consola. 
```
netconvert --osm-files .\datos\sanjuanlurigancho.osm -o sumo\net.net.xml --osm.stop-output.length 20 --ptstop-output sumo\additional.xml --ptline-output sumo\ptlines.xml
```

- `netconvert`: Es el nombre del programa o comando que se utiliza en SUMO para convertir datos de la red.

- `--osm-files .\datos\sanjuanlurigancho.osm`: Especifica el archivo de datos de OpenStreetMap que se utilizará para construir la red de tráfico. En este caso, el archivo se encuentra en la ruta `.\datos\sanjuanlurigancho.osm`. El prefijo `.\` indica que la ruta es relativa a la ubicación actual del comando.

- `-o sumo\net.net.xml`: Especifica el nombre y la ubicación del archivo de salida de la red generada por el comando `netconvert`. En este caso, el archivo de salida se guarda en la carpeta `sumo` con el nombre `net.net.xml`.

- `--osm.stop-output.length 20`: Esta opción define la longitud de las plataformas de parada PT en metros.

- `--ptstop-output sumo\additional.xml`: Esta opción especifica el nombre y la ubicación del archivo de salida que contiene información adicional sobre las paradas de autobús generadas. En este caso, el archivo de salida se guarda en la carpeta `sumo` con el nombre `additional.xml`.

- `--ptline-output sumo\ptlines.xml`: Esta opción especifica el nombre y la ubicación del archivo de salida que contiene información sobre las líneas de transporte público generadas. En este caso, el archivo de salida se guarda en la carpeta `sumo` con el nombre `ptlines.xml`.

Esta línea de comando te permite realizar la conversión de datos de OpenStreetMap a una red de tráfico en SUMO, y obtener información detallada sobre las paradas de autobús y las líneas de transporte público en la zona especificada por el archivo OSM.

### 2. Creacion del trafico de vehiculos ligeros
```
python .\scripts\randomTrips.py -n .\sumo\net.net.xml -r .\sumo\routes.rou.xml -e 3600 -l
```

### 3. Archivo de configuracion
```
<configuration>
    <input>
        <net-file value="tu_red.net.xml"/>
        <route-files value="tus_rutas.rou.xml"/>
    </input>
    <time>
        <begin value="0"/>
        <end value="3600"/>
    </time>
</configuration>
```
## Contribuciones

Las contribuciones son bienvenidas. Si desea contribuir a este proyecto, abra un problema o envíe una solicitud de extracción con sus mejoras.


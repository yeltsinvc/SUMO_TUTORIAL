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



### 2. Creacion de viajes del transporte privado y/o taxis
En este tutorial la creación del tráfico vehicular se realizara con el script randoñTrips.py que permite crear aleatoriamente tráfico vehicular a partir de una red SUMO. Para ello debemos ejecutar en el terminal el siguiente código:
```
python .\scripts\randomTrips.py -n .\sumo\net.net.xml -r .\sumo\routes.rou.xml -e 3600 -l
```

- `-n .\sumo\net.net.xml`: Esta opción especifica la ruta al archivo "net.net.xml" que contiene la definición de la red de transporte en SUMO. El archivo describe los nodos, las calles y las conexiones entre ellos.
- `-r .\sumo\routes.rou.xml`: Esta opción especifica la ruta al archivo `routes.rou.xml` que contiene la definición de las rutas de los vehículos en SUMO. El archivo contiene información sobre los vehículos, sus rutas y horarios.
- `-e 3600`: Esta opción indica la duración de la simulación en segundos. En este caso, se está especificando una duración de 3600 segundos, es decir, 1 hora.
- `-l`: Esta opción indica que se desea imprimir información de registro (logs) durante la simulación.


### 3. Creacion del viajes del transporte publico
Para la creacion de los viajes de transporte publico se utilizara el script `ptlines2flows.py`
```
python .\scripts\ptlines2flows.py -n .\sumo\net.net.xml -s .\sumo\additional.xml -l .\sumo\ptlines.xml -o .\sumo\flows.rou.xml -p 120 --use-osm-routes --types subway
```

- `-n .\sumo\net.net.xml`: Esta opción especifica la ruta al archivo `net.net.xml` que contiene la definición de la red de transporte en SUMO. El archivo describe los nodos, las calles y las conexiones entre ellos.
- `-s .\sumo\additional.xml`: Esta opción especifica la ruta al archivo `additional.xml` que contiene información adicional sobre la red de transporte en SUMO. Puede incluir elementos como semáforos, límites de velocidad, etc.
- `-l .\sumo\ptlines.xml`: Esta opción especifica la ruta al archivo `ptlines.xml` que contiene la definición de las líneas de transporte público. El archivo describe las paradas, las rutas y las frecuencias de los servicios de transporte público.
- `-o .\sumo\flows.rou.xml`: Esta opción especifica la ruta de salida para el archivo `flows.rou.xml`. El archivo generado contendrá los flujos de vehículos basados en las líneas de transporte público.
- `-p 120`: Esta opción especifica el intervalo de tiempo en segundos para la generación de flujos de vehículos. En este caso, se está estableciendo un intervalo de 120 segundos, es decir, 2 minutos.
- `--use-osm-routes`: Esta opción indica que se utilizarán las rutas de OpenStreetMap (OSM) en lugar de las rutas definidas en el archivo "ptlines.xml". OSM es una fuente de datos de mapas y rutas de código abierto.
- `--types subway`: Esta opción especifica el tipo de transporte público que se está procesando. En este caso, se está utilizando el tipo `subway` (metro).

### 4. Archivo de configuracion
Crear en la carpeta sumo el archivo de configuracion `configuracion.sumocfg` con el siguiente contenido
```
<configuration>
    <input>
        <net-file value="net.net.xml"/>
        <route-files value="routes.rou.xml,flows.rou.xml"/>
        <additional-files value="additional.xml"/>
    </input>
    <output>
        <fcd-output value="fcd.xml"/>
    </output>
    <time>
        <begin value="0"/>
        <end value="600"/>
    </time>
</configuration>
```

### 5. Simulacion
Exiten diferentes maneras de ejecutar la simulacion en SUMO. Una de ellas es abriendo el archivo `configuracion.sumocfg` que se encuentra en la carpeta sumo. La otra manera es desde el terminal con el siguiente codigo 
```
sumo-gui sumo\configuracion.sumocfg
```

### 6.Resultados
Existen diversas maneras de analizar los resultados de SUMO, una de ellas es con el archivo de salida `fcd.xml`. El archivo `fcd.xml` en SUMO almacena información sobre la posición, velocidad, aceleración y otras características de los vehículos en una red de tráfico simulada. La información contenida en el archivo `fcd.xml` se utiliza para analizar el flujo de tráfico, evaluar el rendimiento de las infraestructuras de transporte, estudiar los patrones de viaje y realizar diferentes tipos de análisis y simulaciones en el software SUMO. Estos datos son valiosos para comprender el comportamiento de los vehículos y optimizar la planificación urbana y el diseño de las redes de transporte.

A manera de ejemplo si deseamos visualizar la grafica de Velocidad vs Distancia del metro de Lima, podemos ejecutar el siguiente codigo en el terminal.

```
python .\scripts\plot_trajectories.py .\sumo\fcd.xml --filter-ids "subway_L1:0.0"
```

## Contacto

Para cualquier pregunta consultar con yvaleroc@uni.pe

## Referencia
[https://github.com/yeltsinvc/Sumo-Tutorial](https://github.com/yeltsinvc/Sumo-Tutorial) 
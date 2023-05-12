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
netconvert --osm-files .\datos\sanjuanlurigancho.osm -o sumo\net.net.xml
```

## Contribuciones

Las contribuciones son bienvenidas. Si desea contribuir a este proyecto, abra un problema o envíe una solicitud de extracción con sus mejoras.


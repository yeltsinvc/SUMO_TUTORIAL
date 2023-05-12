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

## Instrucciones de instalación

1. Descargar el repositorio desde [https://github.com/yeltsinvc/SUMO_TUTORIAL](https://github.com/yeltsinvc/SUMO_TUTORIAL). Descomprime el repositorio.
2. Instale [SUMO](https://www.eclipse.org/sumo/).
3. Coloque el archivo de datos de OpenStreetMap en la carpeta `data/`.
4. [Opcional] Ajuste los parámetros en el archivo `randomtrips.py` según sea necesario.
5. Ejecute el siguiente comando para generar los viajes aleatorios: `python data/randomtrips.py -n <NUM_VIAJES> -r data/map.osm`.
   - Reemplace `<NUM_VIAJES>` con el número deseado de viajes aleatorios a generar.
6. Ejecute el siguiente comando para generar rutas utilizando pt2flow: `python data/pt2flow.py`.
7. Los resultados se guardarán en la carpeta `data/results/`.

## Contribuciones

Las contribuciones son bienvenidas. Si desea contribuir a este proyecto, abra un problema o envíe una solicitud de extracción con sus mejoras.

## Lic
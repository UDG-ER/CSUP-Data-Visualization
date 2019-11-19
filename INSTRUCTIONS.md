# Instructions
In order to succesffully complete this project you will need to visualize data retrieved from RTEPMS platform. RTEPMS (Real-Time Environmental Parameters Monitoring System) represents general-purpose environmental parameters monitoring system.

### Objective
The main idea behind this project is to utilize data from RTEPMS platform and create visually attractive dashboard that will show info about current weather as well as weather forecast. Reactive dashboard will be displayed on TV at the University hall.

### Resources

RTEPMS API endpoint for fetching measurements.
```
http://rtepms.udg.edu.me:8000/api/measurement_by_date/?node_id=3&start_date=19/11/2019&end_date=19/11/2019
```
**Note: If you are not able to resolve rtepms.udg.edu.me domain use IP address: `213.149.113.86` like this `http://213.149.113.86:8000`.

**Params**
  - `node_id` - Public Node ID
  - `start_date` - Get sensor measurements from this date
  - `end_date` - Get sensor measurments till this date. (Optional - if not passed end_date will be `till today`)
  
**Available Nodes**

Node ID `3` -> `UDG Meteo Station - Air info`
  
- `sensor_1_val` -> `Air Temperature  [C]`
- `sensor_2_val` -> `Air Humidity [%]`
- `sensor_3_val` -> `Air Pressure [mbar]`

Node ID `4` -> `UDG Meteo Station - Wind info`
  
- `sensor_1_val` -> `Average Wind Speed (1min) [m/s]`
- `sensor_2_val` -> `Maximum Wind Speed (5min) [m/s]`
- `sensor_3_val` -> `Wind Direction deg°`
   
Node ID `5` -> `UDG Meteo Station - Rainfall info`
  
- `sensor_1_val` -> `Rainfall (1h) [mm]`
- `sensor_2_val` -> `Rainfall (24h) [mm]`
  
**Additional Endpoint**
You can use another API endpoint to fetch only several (`limit`) last measurements.
```
http://rtepms.udg.edu.me:8000/api/measurement_by_limit/?node_id=3&limit=5
```
**Note**

_Please note that historical data might containg testing data as platform is still in development mode._



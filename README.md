# CoAXs Modifications: Seed and GeoJSON files

CoAXs allows users to create their own transit scenarios by setting the parameters of certain pre-defined "seed" modifications.  For example, we can specify through a seed modification that Route 1 can have its speed adjusted, and the front-end interface will allow users to set the speed.
   
## Seed Modification data (required)
The seed modification is formatted as a JSON file with information that includes:
- (1) which transport route[s] you wish to modify (e.g. Route 1, Piccadilly Line...) 
- (2) what kind of change you want to make (e.g. adjust speed, frequency, dwell time)
 
***If multiple routes serve a corridor, they can be bundled together into one corridor file (see example [https://github.com/mitTransportAnalyst/Scenario-seed-data-documentation/blob/master/Mass%20Ave%20seed%20data.json](here))***

## GeoJSON (optional)
The GeoJSON allows for a map-based representation of where the modification is applied (e.g. the segment in which speed is adjusted).  For the folowing example modification types, you might want to include:

**Adjust speed/frequence/dwell time: GeoJSON for entire route/corridor**
**Remove stops: GeoJSON points for the stops you removed**
**Remove trips: GeoJSON line for for the trips you removed**
**reroute: GeoJSON line for the new route you added**

## Why does CoAXs need seed modification data for scenarios?
In our CoAXs frontend, every time you move the slider bar, it will find the corridor you select and look up the scenario seed data for that corridor and change the the value of scale parameter to the slider value for each route in this scenario seed data.   

For example, the following is one piece of seed data for Mass Ave. It defines the type of change: "adjust-dwell-time", route you want to change, and the scale (how much you want to change). Basically, CoAXs frontend just changes the scale parameter into the slider value. 

```json
    {
      "type": "adjust-dwell-time",
      "routes": [
        "MBTA:701"
      ],
      "stops": null,
      "scale": 0.6,
      "comment": "CT1-Dwell"
    },
```

## How to make scenario seed modification data?
For each corridor, we need a seperate scenario seed data. 
- For each corridor, we need to create a new scenario in [https://github.com/conveyal/analysis-ui](Scenario Editor)
- Put all the routes and all the changes you want to make under this scenario. 
- Push the download button, you will get a JSON file
- Repeat for each corridor

## How to make GeoJSON file?
For each corridor and each modification, we need a seperate Geojson file. 
- Create a shapefile including corridor or station points or new lines you want to show on the map
- convert shapefile to GeoJSON file
You can use this repo to do conversion https://github.com/substack/shp2json

## Example
### Adjust-dwell-time
```json
    {
      "type": "adjust-dwell-time",
      "routes": [
        "MBTA:701"
      ],
      "stops": null,
      "scale": 0.6,
      "comment": "CT1-Dwell"
    }
```
### adjust-frequency
```json
    {
      "type": "adjust-frequency",
      "route": "MBTA:64",
      "retainTripsOutsideFrequencyEntries": false,
      "entries": [
        {
          "monday": true,
          "tuesday": true,
          "wednesday": true,
          "thursday": true,
          "friday": true,
          "saturday": false,
          "sunday": false,
          "name": "64-OB",
          "startTime": 25200,
          "endTime": 32400,
          "headwaySecs": 900,
          "startTimes": null,
          "sourceTrip": "MBTA:28759180"
        },
        {
          "monday": true,
          "tuesday": true,
          "wednesday": true,
          "thursday": true,
          "friday": true,
          "saturday": false,
          "sunday": false,
          "name": "64-IB",
          "startTime": 25200,
          "endTime": 32400,
          "headwaySecs": 720,
          "startTimes": null,
          "sourceTrip": "MBTA:28766359"
        }
      ],
      "comment": "64-Frequency"
    }
```

### adjust-speed
```json
{
"type": "adjust-speed",
      "routes": [
        "MBTA:701"
      ],
      "hops": [
        [
          "MBTA:58",
          "MBTA:10590"
        ],
        [
          "MBTA:10590",
          "MBTA:87"
        ],
        [
          "MBTA:87",
          "MBTA:188"
        ],
        [
          "MBTA:95",
          "MBTA:97"
        ],
        [
          "MBTA:97",
          "MBTA:101"
        ],
        [
          "MBTA:101",
          "MBTA:1060"
        ],
        [
          "MBTA:1060",
          "MBTA:72"
        ],
        [
          "MBTA:72",
          "MBTA:73"
        ],
        [
          "MBTA:187",
          "MBTA:84"
        ],
        [
          "MBTA:84",
          "MBTA:59"
        ],
        [
          "MBTA:59",
          "MBTA:854"
        ]
      ],
      "scale": 1.4,
      "comment": "CT1-Speed"
    },
```




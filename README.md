# The scenario seed modification and Geojson documentation

 This documentation is going to tell you what the scenario seed modification and geojson need for CoAXs frontend

   
## What is the scenario seed modification data (required)?
Scenario seed modification data is a JSON file that includes the information that indicates 
- (1) which bus lines/subway lines you want to make changes (like Line 1, Line CT1...) 
- (2) what kind of change you want to make(like change speed, frequency, dwell time)
 
***And each corridor should have its unique JSON file which means bundle all the bus lines in one corridor into one JSON file. ***

## What is the Geojson (optional) ?
Geojson is a JSON file that includes the data to show the point, line, polygon on the map. Geojson file is optional. 

## Why CoAXs frontend need scenario seed modification data?
In our CoAXs frontend, every time you move the slider bar, it will find the corridor you select and look up the scenario seed data for that corridor and change the the value of scale parameter to the slider value for each bus lines in this scenario seed data.   

For example, the following is one piece of seed data for Mass Ave. It define the type of change: "adjust-dwell-time" and the bue line you want to change and the scale(how much you want to change). Basically, CoAXs frontend just changes the scale parameter into the slider value. 

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

## Why CoAXs frontend need the Geojson?
In CoAXs, when we select a corridor and then make some changes (like headway/speed) on that corridor, you may want show something on the map to help the user to understand what you have changed. For example, in our livable street workshop, we zoom in to that corridor when we select it and make change of it. Of course, this is optional. You can do nothing when user make some changes. 

Different modification should have different geojson to show on the map:

Adjust speed/frequence/dwell time: Geojson for each corridor

add/remove stops: Geojson for stops

reroute: Geojson for the new route you added

## How to make scenario seed modification data?
For each corridor, we need a seperate scenario seed data. 
- For each corridor, we need to create a new scenario in scenario editor
- put all the bus lines and all the changes you want to make under this scenario. 
- Push the download button, you will get a JSON file
- Do it for each corridor

## How to make Geojson file?
For each corridor and each modification, we need a seperate Geojson file. 
- Create a shapefile include corridor or station points or new lines you want to show on the map
- convert shapefile to Geojson file

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

Please see the following link to see what does scenario seed data for the whole Mass Ave corridor look like.
https://github.com/mitTransportAnalyst/Scenario-seed-data-documentation/blob/master/Mass%20Ave%20seed%20data.json


And for reroute function, I need some time to figure out how to make change of it. 

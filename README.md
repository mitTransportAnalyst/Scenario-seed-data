# The scenario seed data documentation

 This documentation is going to tell you what the scenario seed data need for CoAXs frontend

   
## What is the scenario seed data?
Scenario seed data is a JSON file that includes the information that indicates 
- (1) which bus lines/subway lines you want to make changes (like Line 1, Line CT1...) 
- (2) what kind of change you want to make(like change speed, frequency, dwell time)
 
***And each corridor should have its unique JSON file which means bundle all the bus lines in one corridor into one JSON file. ***

## Why CoAXs frontend need scenario seed data?
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

## How to make scenario seed data?
For each corridor, we need a seperate scenario seed data. 
- For each corridor, we need to create a new scenario in scenario editor
- put all the bus lines and all the changes you want to make under this scenario. 
- Push the download button, you will get a JSON file
- Do it for each corridor

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

And for reroute function, I need some time to figure out how to make change of it. 

---
authors:
  - name: MishkaNS
    avatar: /assets/mishka.jpg
icon: archive
---
# Capella Archive

## Overview

This service tracks chosen polygons from a chosen start date
in Capella's archive. As soon as a new collect that is within a
polygon being tracked becomes available in the archive, this
service automatically orders and downloads it.

!!! :zap: Installation and code :zap:
For more details about the service, please visit the github repository [here](https://github.com/Green2Moon/capella-archive)
!!!

---
The systems are automated system to use capella archive.
It divided to two parts: 
- Active archive: actively search for new products by predefined shape and params
- BDB: creating shape file that holds all capella archive items, and ordering shapes by excel file

## Active archive - How does it works?

1. The shift enters shapes and parameters for the system to search for in capella archive 
2. Every interval the system looks for new products by params
3. If we not passed contract limit for this shape and there is new available product the system order it(which called in planet syntax activate asset) and download it

## BDB - How does it works?

### BDB - save shapes

1. The system once a day asking from capella the catalog 
2. It writes to folder the catalog from capella as shape file

### BDB - ordering shapes

1. The shift fills an excel containing one column and each row a unique id of shape
2. The system do validation on file and ordering each one of id in file (which called in planet syntax activate asset)
3. Download the new products to shifts computer

## Explanation of the project

- Collections : 
    - archive-trackings : polygons that are or have been tracked in Capella's archive
    - archive-downloads : collect, order and download data on collects that have been downloaded from the archive

- routes :
    - POST /track : begins to track the polygon inserted into the request's body from the specified start date (default start date is 24 hours before current)
    - DELETE /track/cancel : stops tracking the polygon (or _id of the archive-tracking document) specified in the request's body
    - GET /track/active : returns all polygons that are currently being tracked in the archive (along with their start dates)
    - /api-docs : the server's swagger, which users can use to execute the aforementioned routes. User must authenticate the swagger using the username and password from .env.

- jobs : 
    - get order and download - check Capella API for any new collects available in the archive that fall within any of the polygons actively being tracked
    - daily update of collects ordered today - check every archive-tracking in the database whether a day passed since the last product was downloaded, and update the archive-tracking document accordingly

- apis : 
    - capella api -  https://docs.capellaspace.com/api

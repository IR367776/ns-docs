---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# planet-archive

The systems are automated system to use planet archive.
It divided to two parts: 
- Active archive: actively search for new products by predefined shape and params
- BDB: creating geo json file that holds all planet archive items, and ordering shapes by excel file

## Active archive - How does it works?

1. The shift enters shapes and parameters for the system to search for in planet archive 
2. Every interval the system looks for new products by params
3. If we not passed contract limit for this shape and there is new available product the system order it(which called in planet syntax activate asset) and download it

## BDB - How does it works?

### BDB - save shapes

1. The system every interval search for new products through planet api
2. It saves all new products in db
3. It takes all shapes exists in db and write it to file and save it shift computer

### BDB - ordering shapes

1. The shift fills an excel containing one column and each row a unique id of shape
2. The system do validation on file and ordering each one of id in file (which called in planet syntax activate asset)
3. Download the new products to shifts computer

## ENV variables

- PORT: port of server (default 3000)
- DB_URL: url to db the system uses
- DB_NAME: name of db (default 'planet-archive')
- API_KEY: api key to authenticate with planet api
- PLANET_URL: url to planet endpoint
- DOWNLOAD_PATH: the path to the folder the new products will be downloaded (default './files')
- START_DATE_OF_SEARCH: the first date the bdb will search products 
- MAX_CLOUD_COVER: max cloud coverage allowed for product (default 0.7)
- SWAGGER_USERNAME: username used by shift to use swagger
- SWAGGER_PASSWORD: password used by shift to use swagger
- ARCHIVE_FOLDER: the path to the folder the bdb geojson file will be written (default './geometries')

![Planet archive interval](/assets/planet-archive.jpg)

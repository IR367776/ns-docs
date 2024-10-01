---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# blacksky-archive

The systems are automated system to use blacksky archive.
It divided to two parts: 
- Active archive: actively search for new products by predefined shape and params
- BDB: creating geo json file that holds all planet archive items, and ordering shapes by excel file

## Active archive - How does it works?

1. The shift enters shapes and parameters for the system to search for in blacksky archive 
2. Every interval the system looks for new products by params
3. If we not passed contract limit for this shape and there is new available product the system order it 
4. The blacksky-download system download product to shift computer

## BDB - How does it works?

### BDB - save shapes

1. The system every interval search for new products through blacksky api
2. It saves all new products in db
3. It takes all shapes exists in db and write it to file and save it on shift computer

### BDB - ordering shapes

1. The shift fills an excel containing one column and each row a unique id of shape
2. The system do validation on file and ordering each one of id in file.
    - If file is valid move file to done folder and order each id and update db.
    - If file is invalid move file to errors folder and add errors.txt file to tell shift what is invalid 
3. The blacksky-download system download product to shift computer

## ENV variables

- PORT: port of server (default 3000)
- DB_URL: url to db the system uses
- DB_NAME: name of db (default 'blacksky-archive')
- API_KEY: api key to authenticate with blacksky api
- BLACKSKY_URL: url to blacksky endpoint
- MAX_CLOUD_COVER: max cloud coverage allowed for product (default 50)
- SWAGGER_USERNAME: username used by shift to use swagger
- SWAGGER_PASSWORD: password used by shift to use swagger
- ARCHIVE_FOLDER: the path to the folder the bdb geojson file will be written (default './archive')
- TIME_BETWEEN_DOWNLOAD_JOB = time between intervals of searching and ordering from db (default '120000')

![Blacksky archive interval](/assets/blacksky-archive.jpg)

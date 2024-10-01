---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# blacksky-download

This system is used for managing all products related to blacksky.
Works in interval defined by environment variable.
Each interval will ask blacksky api for new products to download and download it.
The system support for download analytics also. 

## The program does the following:

1. Req blacksky for new products available for download.
2. Search for every product without artifacts(different processing types and analytics types available) 
3. Choose and download preferred image processing available by shift priority and download every analytic available for product

## ENV variables

- DB_URL: url to db the system uses
- DB_NAME: name of db (default 'blacksky-download')
- API_KEY: api key to authenticate with blacksky api
- BLACKSKY_URL: url to blacksky endpoint
- DOWNLOAD_BDILA_PATH: the path to the folder the products will be downloaded to.
- NUMBER_OF_MINUTES_BETWEEN_JOBS = time between intervals of searching and downloading (default 1)
- START_DATE_OF_PRODUCT_SEARCH: initial date to search new products when system is booting up
- PRODUCT_LIMIT: number of products limit per req (default 100)
- NUMBER_OF_RETRIES: number of retries to download product (default 5)

![Blacksky download interval](/assets/blacksky-download.jpg)
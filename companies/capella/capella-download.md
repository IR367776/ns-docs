---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# capella-download

This system is used for managing all products related to capella.
Her job is to receive a message about a product that is available for download from collects-capella to order the product from the company and download it to a folder on the shift computer called capella-downloads.
For each product there should be 3 folders indicating the three types of processing of the product: SLC, GEO, GEC. When in each of the folders there are two files: the imagery file itself and a json file
which describes the details of the image.
The order made by the system is in order to req from the company return to us a download link.
The download is accruing from its cloud storage.
After the products have been downloaded, they are separated and distributed by an agent for Barak and Globus.

## The program does the following:

- Consumes a collectId from a RabbitMQ queue when its status is delivered(sent by capella-collects)
- Searches for the data matching the collectId via the post catalog search route
- Orders the relevant items using the post orders route
- Downloads the items from the url provided by Capella's get orderId download route
- Saves the order info and its download status to a database

## ENV variables

- CAPELLA_URI: capella api url(default 'https://api.capellaspace.com')
- CAPELLA_USERNAME: capella username
- CAPELLA_PASSWORD: capella password
- MONGO_URI: url for database 
- DB_NAME: system database name (default 'Capella')
- ORDERS_COLLECTION_NAME: name of collection used in db(default 'orders')
- DOWNLOAD_DIR: path of dir the system download files to (default './files')
- RABBIT_SERVER: url of rabbitmq server
- QUEUE_NAME: name of the queue the system reads messages from(default 'deliveredCollects')
- EXCHANGE_NAME: name of the exchange the system reads messages from (default 'deliveredCollectsExchange')
- ORDER_TRIES: number of tries to order collect(default 8)
- DOWNLOAD_TRIES: number of tries to download collect (default 8)
- CATALOG_SEARCH_TRIES: number of try searching collect in catalog (default 5)
- RETRY_ORDER_TIME_INTERVAL_MIN: number of minutes between retrying ordering collect (default 15)
- RETRY_DOWNLOAD_TIME_INTERVAL_MIN: number of minutes between retrying downloading collect (default 15)
- RETRY_CATALOG_SEARCH_INTERVAL_MIN: number of minutes between retrying searching collect in catalog (default 0.5)
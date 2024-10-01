---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---

# Blacksky Tasking

weather api: https://app.swaggerhub.com/apis-docs/WeatherAPI.com/WeatherAPI/1.0.2-oas3-oas3.1-oas3.1/#/APIs/forecast-weather
## Description

This service receives tasks from New Space Agent via a server
and orders them automatically from Blacksky through their API.

![blacksky tasking flow](/assets/blacksky-tasking-flow.png)


## Getting Started
    Installation process:
    * Clone the project 
    * Add .env file (environment variables will be described below)
    * Install dependencies
    * Run this commands for the needed docker images:
        - docker run -d -p 27017:27017 --name test-mongo mongo:latest


### Install

1. Node version

    If you are using `nvm` to manage node version, you can use `nvm` to install node version.

    ```bash
    nvm use
    ```

    If not, make sure you have node installed on version `>=18.0.0`.

    ```bash
    node -v
    ```

2. Install packages

    ```bash
    npm ci
    ```

### Test

1. Create `.env` file with the following variables:

    ```bash
    MONGO_URI = 'mongodb://localhost:27017'
    BLACKSKY_URL = 'https://api.sit.BlackSky.com'
    ```

    get authentication from microsoft teams 
    ```bash
    TEST_API_KEY
    ```

2. Run test

    ```bash
    npm test
    ```

### Production

1. Create `.env` file

2. Build dist

    ```bash
    npm build
    ```

2. Run service

    ```bash
    npm start
    ```


## Explanation of the project

* collections:
    - tasks: tasks that have been ordered from Blacksky
    - instances: instances that have been converted from New Space Agent orders that have been tasked or are awaiting tasking

* routes:
    - POST /order: takes an array of NS Agent orders in the body, converts them to instances, and saves them in the db in the instances collection
    - DELETE /order/cancel/:orderId : takes a NS Agent orderId and cancels all instances and tasks that cover that orderId (the ids in the format of BS43-124fgvsd-oiun235…)
    - DELETE /order/cancel/multiple: cancels multiple NS Agent orders and their associated tasks at once. Pass the Ids as a comma separated list in quotation marks, replacing the “orderId1, orderId2, orderId3” string in the swagger body.
    - DELETE /order/cancel-all: cancels all active instances and tasks
    - PATCH /order: takes a NS Agent order and edits all instances that match the orderId passed according to the parameters passed
    - POST /contract/initial: creates the initial contract with the number of points for the week passed in the query. Sets the end of the week to the optional date passed in the query, defaults to midnight of the current date.
    - GET /contract: gets the current contract from the db
    - PATCH /contract/set-weekly-points/next-week/:pointsForWeek : sets the weekly points for the next week (to be updated at weekEndDate)
    - PATCH /contract/set-weekly-points/now/:pointsForWeek : sets the remaining points for the current week and sets into effect immediately

* jobs: 
    - update status - check Blacksky API for any change in status in the outstanding orders and updates them in the database
    - update contract - refresh the daily and weekly points of the contract when a day and week has passed
    - task instances - grab and task the instances from the db for tomorrow that have not been tasked yet

* apis: 
    - blacksky api -  https://docs.sit.blacksky.com/



## ENV variables: 

- TEST_API_KEY = Blacksky test api key
- API_KEY = Blacksky operational api key
- BLACKSKY_URL = The url to the capella api
- PREFERRED_OFFERING_ID = Offering ID from Blacksky for preferred products
- PREFERRED_OFFERING_SKU = Offering sku from Blacksky for preferred products (default - bsg-preferred)
- ELITE_OFFERING_ID = Offering ID from Blacksky for elite products
- ELITE_OFFERING_SKU = Offering sku from Blacksky for elite products (default - bsg-elite)
- SWAGGER_USERNAME = The username used for swagger authentication
- SWAGGER_PASSWORD = The password used for swagger authentication
- MONGO_URI = The url to the mongodb database 
- DB_NAME = The database name (default - blacksky-tasking)
- TASKS_COLLECTION_NAME = The collection name for tasks (default - tasks)
- INSTANCES_COLLECTION_NAME = The collection name for instances (default - instances)
- CONTRACT_COLLECTION_NAME = The collection name for contract (default - contract)
- MINUTES_BETWEEN_UPDATE_STATUSES_CONTRACT_JOB = Number of minutes of interval for job that updates contract and task statuses (default - 10)
- MINUTES_BETWEEN_TASK_INSTANCES_JOB = Number of minutes of interval for job that tasks tomorrow's instances (default - 60)
- TASK_INSTANCES_START_HOUR = Hour of the day to start the task instance job (default - 9)
- TASK_INSTANCES_END_HOUR = Hour of the day to end the task instance job (default - 18)
- LOG_LEVEL = The logger log level (default - 'info')
- PORT = The server port  (default - 3000)
---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# NEW-SPACE-AGENT
![New space agent](/assets/007.jpg)

## In general
The system that organize all orders, plans and products metadata on civilian side.
It suppose to get all his orders from gateway(army-side) and send it to constellations tasking system through http protocol.
It also has server that uses as endpoint to all constellation for updates about order statuses(update agent when order is planned/downloaded)

<!-- ABOUT THE PROJECT -->
## About The Project

The project is about building agent for all new space constellation. 
responsible for having all new space orders and plans

Here's how:
* it has a watcher to bdila folder that have all orders
* Add all orders to db 
* send orders to the right constellation
* listen for statuses from all constellations  
* update the statuses changes according to what he get   
* get all the plans from every constellation
* get product metadata from download systems
* get automatic qa information


<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Built With

List of major frameworks/libraries used for the project.

* [![TypeScript][TypeScript]][TypeScript-url]
* [![Nodejs][Nodejs]][Nodejs-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Database

The db we use is mongodb 
* [![Nodejs][MongoDB]][Mongodb-url]

| CollectionName  | description |
| ------------- | ------------- |
| orders  | contains orders details recived from NEXT-TEAM with all their parameters |
| plans  | contains plans details recived from all constellations |

<p align="right">(<a href="#readme-top">back to top</a>)</p>




<!-- GETTING STARTED -->
## Getting Started

To get a local copy up and running follow these simple steps.

### Prerequisites

list things you need to use the software and how to install them
1. Install docker desktop

   [![Docker][Docker]][docker-url]

2. Pull mongodb and rabbitmq images from docker to use them for the tests and Dev environment 
  
### Installation

1. Clone the repo
   ```sh
   git clone https://github.com/New-Space-Dev/new-space-agent.git
   ```
2. Install NPM packages
   ```sh
   npm install
   ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- USAGE EXAMPLES -->
## Usage

scripts you can run in terminal or for debug 

1. run the development mode 
   ```sh
   npm run dev
   ```
2. run the tests 
   ```sh
   npm run test
   ```
3. run the production mode  
   ```sh
   npm run build
   npm run start
   ```



<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Environment-Variables

Set these in .env or in your environment to use the project.
- MONGO_URL = The url to the mongodb vm 
- NEW_ORDERS_PATH = path to the orders folder where all the orders waiting to send (default 'orders')
- ORDER_UPDATES_PATH = path to receive order updates(change in priority or cancel)  (default 'updates')
- PLANS_PATH = path where we should write the plans after receiving from constellations(default 'plans')
- USER_NAME = username for swagger login
- PASSWORD = password for swagger login
- CAPELLA_ORDERS_URL = capella-tasking url for requests 
- CAPELLA_TASKING_KEY = capella-tasking auth
- CAPELLA_PLANS_URL = capella-collects url for requests
- CAPELLA_COLLECTS_KEY = capella-collects auth
- CAPELLA_ORDERS_QUEUE_NAME = capella queue for statuses 
- CAPELLA_ORDERS_EXCHANGE_NAME = capella exchange name for capella order statuses
- CONSUMER_EVENT_NAME = The event name that should appear on every message (default 'capella-orders-statuses')
- RABBITMQ_URL = The url to the rabbit server: `amqp://{rabbit host}`.
- PORT = The server port
- SERVER_HOST = server host ip 


<p align="right">(<a href="#readme-top">back to top</a>)</p>


<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[TypeScript]: https://img.shields.io/badge/typescript-000000?style=for-the-badge&logo=typescript&logoColor=blue
[TypeScript-url]: https://www.typescriptlang.org/ 
[Nodejs]: https://img.shields.io/badge/Nodejs-35495E?style=for-the-badge&logo=node.js&logoColor=4FC08D
[Nodejs-url]: https://nodejs.org/en/ 
[Docker]: https://img.shields.io/badge/Docker-0769AD?style=for-the-badge&logo=docker&logoColor=white
[docker-url]: https://www.docker.com/products/docker-desktop/
[MongoDB]: https://img.shields.io/badge/MongoDB-35495E?style=for-the-badge&logo=MONGOdb&logoColor=green
[Mongodb-url]: https://www.mongodb.com/

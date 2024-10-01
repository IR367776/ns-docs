---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# NEW-SPACE-GATEWAY

## In general
The server that organize all orders, plans and products metadata on army side.
It suppose to get all his orders from NEXT(team responsible for constellation management in the unit) system which called "wolt".
It suppose to make the conversion of orders to the right format in order that agent on civilian side can send it to constellations.
After bdila he receives from civilian side updates about orders statuses, plans and products.
He updates wolt on any plan updates and serve as a endpoint to check coverage of new space products
(To check which order were fulfilled by products).

<!-- ABOUT THE PROJECT -->
## About The Project

The project is our representative on the army side.
It serve as endpoint to receive orders and send plans and products update

Here's how:
* It receive orders from wolt by rabbitmq message
* It receive order updates(change of priority or cancel) from wolt by rabbitmq message
* Has swagger that enables shift to download all orders to folder on shift computer for bdila
* It listen to folder to receive any updates on plans/products from civilian side  
* Update the statuses changes according the what he get and update wolt also (by http req)  
* Check coverage of product to orders by comparing product and order parameters
* Update next team if he can cover orders by the plans he receives from constellations

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
  


<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Environment-Variables

Look at config folder or .env file available in gitlab


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

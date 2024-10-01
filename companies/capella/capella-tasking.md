---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# capella-tasking

This system is used for managing all demands related to capella.
It automated all the tasking process and managing all demands by their priority and type(periodic/single).
Her role is to manage the bookings in front of Capella
by prioritization and the type of requirements. There are two types of orders with the company: order
repeating and single task. A single task is an order for a single image.
And a repeating task is an order over a large area of ​​time (usually about a month), in this kind of order
we need to send the company in advance for the number of frequency of images we want over a long period of time.
The system performs several functions:
- The first to receive orders from the agent and carry them out in front of the company
- The second to monitor order statuses and update according to the agent
- The third to update collects-capella when there is a collect to order (collect is plan for image)

## Intervals that are been done repeatedly by the system

- The system tasking interval: Gets all orders to task by their priority and order them by the order of their priority
- The orders update interval: It check and update statuses of orders
- The approve repeat task interval: Capella takes time to process an periodic demand. Hence we need to wait between order and approving periodic demands in front of capella api

## ENV variables

- RELEVANCE_START_TIME_IN_HOURS: The start time of relevant instances(default value 6 hours from now)
- RELEVANCE_END_TIME_IN_DAYS: The end time of relevant instances(default value 7 days from now)
- CAPELLA_URL: Capella api endpoint url
- DB_URL_URL: Data base url
- DB_NAME: The name of data base(default 'capella-tasking')
- CAPELLA_USERNAME: The user to capella api
- CAPELLA_PASSWORD: The password for capella api
- ORGANIZATION_ID: Our organization id as it saved in capella
- USER_ID: Our user id as it saved in capella
- BILLING_ENVIROMENT: Our billing env ('sandbox')
- RABBITMQ_URL: Url of rabbitmq server
- EXCHANGE_NEWSPACE_AGENT: Name of exchange in rabbit with newspace-agent
- COLLECTS_RABBIT_TOPIC: name of topic used for updates about collects with capella collects (default 'capella-tasks-statuses')
- GATEWAY_RABBIT_TOPIC: name of topic used for updates about orders with newspace-agent (default 'capella-orders-statuses')
- TASKING_JOB_INTERVAL: The time between two intervals of tasking 
- UPDATING_STATUS_JOB_INTERVAL: The time between two intervals of status updates on tasks
- APPROVE_REPEAT_TASKS_INTERVAL: The number of minutes between two intervals of approving repeat tasks after they were tasked
- SERVER_PASSWORD: api key to use for authentication with server
- PORT: The port of server used to connect with the system server(default value is 3000)


---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# capella-collects

This system is used for managing all collects related to capella.
Collects is the way in which the company makes the planning for the imagery that it has accessible
From the moment it was planned until the moment it was taken and distributed on the company's website. The system performs a number
Actions:
- Receive collect id from capella tasking to follow(receive through rabbitmq server)
- Follows Capella's statuses regarding collects and updates in db
- Sends the plans to the newspace-agent system that is, converts from a collect to a schema of
plan for the agent 
- Sending to the download system capella-download that there is a product ready for download
(collects that have reached the delivered status)

## Intervals that are been done repeatedly by the system

- The collects status update: Check the status of every collect that not reached final status and update is status in db

## ENV variables

- PORT: port used for capella collect server(default 3000)
- CAPELLA_URI: capella api url
- CAPELLA_USERNAME: capella username
- CAPELLA_PASSWORD: capella password
- MONGO_URI: url for database 
- DB_NAME: system database name (default 'Capella')
- RABBIT_SERVER: url of rabbitmq server
- PUBLISH_EXCHANGE_NAME: exchange name used for publish messages
- QUEUE_NAME: name of the queue the system reads messages from
- CONSUME_EXCHANGE_NAME: name of the exchange the system reads messages from
- DEAD_LETTER_EXCHANGE_NAME: name of exchange the system sends invalid messages
- DEAD_LETTER_QUEUE_NAME: name of queue the system sends invalid messages
- REFRESH_COLLECTS_JOB_INTERVAL: minutes between jobs (default l)
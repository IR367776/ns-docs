---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# planet-tasking

This system is used for managing all instances related to planet.
Planet works in Assured method, which means what you order is almost 100% will be taken and delivered to you.
Hence, they are providing through their api a way to search imaging windows for every task you send them.
The system are managing all the instances order by their priority, their available imaging windows , contract limitation and cloud coverage.

Army works with repeat demands that has frequency but planet works with single instances.
The system is used to take the repeat demands and divide them into single instances by their frequency and relevance time.

## Divide repeat demands to single instances

1. The system receive demand message from new space agent
2. It looks on frequency and relevance time and for every instance add the frequency to the last 
    created instance till we pass are relevance end time
3. It saves all the new created instances in instances collection in our planet database


## Intervals that are been done repeatedly by the system

- The system tasking interval: It goes through all relevant instances (6 hours from now till a week) and try to task them by their priority and contract limitation
- The contract interval: It works once a day and update contract daily points by points and days left 
- The orders update interval: It check and update statuses of orders and if order is denied by company it returns points to contract
- The cloud coverage interval: It check for all orders that are cancellable and are less than 48 hours away if their cloud coverage is over 50. It cancel orders that are most likely will be cloudy.

![Planet tasking intervals](/assets/planet-tasking-intervals.png)

## ENV variables

- RELEVANCE_START_TIME_IN_HOURS: The start time of relevant instances(default value 6 hours from now)
- RELEVANCE_END_TIME_IN_DAYS: The end time of relevant instances(default value 7 days from now)
- PLANET_URL: Planet api endpoint url
- MONGO_URL: Data base url
- DB_NAME: The name of data base
- PLANET_AUTH_TOKEN: The api token for the user to planet api
- SWAGGER_USERNAME: The user name the shift uses to do operation on systems data
- SWAGGER_PASSWORD: The user password the shift uses to do operation on systems data
- MINUTES_BETWEEN_RUN: The number of minutes between two intervals of systems (default value is 1)
- PORT: The port of server used to connect with the system server(default value is 80)


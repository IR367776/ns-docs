---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# planet-download

The systems download ready products from Planet. The products are only related to tasking and not archive. It works in intervals of few minutes.
Planet calls their products captures and every capture can contain assets(usually one but sometimes 2) which are the images themselves.

## How does it works?

1. The system ask planet for new captures since the last req (The previous interval time).
2. For every new capture it req from planet all the assets available(usually 1 or 2)
3. Download every new asset available and update db

## ENV variables

- PLANET_URL: Url to endpoint of planet api
- DB_URL: The url of the mongo instance/ server
- API_KEY: Api key for authentication to planet api

![Planet download interval](/assets/planet-download-proccess.jpg)

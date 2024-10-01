---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# talqa-eo

In attempt to make our flow as automatic as possible, we created qa systems for eo products we receive from companies(mainly blacksky and planet).


## How does it works?

1. The download systems sent all products to azure storage
2. The qa system pull the images and metadata from azure and perform set of functions to search defects
3. The qa system sends result to new-space-agent

![eo qa flow diagram](/assets/talqa-eo.png)

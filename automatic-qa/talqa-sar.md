---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# talqa-sar

In attempt to make our flow as automatic as possible, we created qa systems for sar products we receive from companies(mainly capella).


## How does it works?

1. The download systems sent all products to azure storage
2. The qa system pull the images and metadata from azure and perform set of functions to search defects
3. The qa system sends result to new-space-agent

![eo sar flow diagram](/assets/talqa-sar.png)

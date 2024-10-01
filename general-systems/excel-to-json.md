---
icon: light-bulb
authors:
  - name: SuperEE
    avatar: /assets/tal.jpg
---


# excel-to-json

Till all companies will fully integrated to prisma, the shift needs way to insert new demands to the tasking systems. This system sits in the secure web and reads excel file from specific folder and parse every line to demand json that will insert to shift internet computer(with bdila) and will sent eventually to new-space-agent that will send to tasking system

## How does it works?

1. The system opens network folder and wait till new file is added 
2. The shift satellite operator fills an excel file which every row is demand with all parameters   
    needed.
3. He takes the file after and put it in folder
4. The system parse the file line by line and do validation on parameters
5. If file is invalid it will move to errors folder with errors file which tells the operator what is wrong
6. If file is valid it will move it to done folder and put all demands json files in jsons folder

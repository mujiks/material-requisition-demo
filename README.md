# Material-requisition-demo
Material requisition demo for presentation. Spring boot + Swagger + Java 8 + Postgres.


This is a very simple application to manage internal material. It provides
  - a list of who is using which material.
  - a list of available material. 
  - a material requisition form.
  - a material devolution form.
  
  The user can request: a book, a laptop, a monitor, a video projector, etc.
  
  The application exposes a full described RESTFUL API.
  
  And the main goal is how this application can be distributed with docker.

## Create a spring boot project
The following link bootstraps your application for you:
http://start.spring.io/

## Example to run a postgres container
docker run -p 5432:5432 --name material_requisition_db -e POSTGRES_PASSWORD=admin -d postgres

## Create database
docker exec -it material_requisition_db psql -U postgres -c "CREATE DATABASE demo;"

## Example to build and push your application into docker_hub
Don't forget to docker login first
docker build  -f Dockerfile -t mujiks/material-requisition-demo .
docker push mujiks/material-requisition-demo
docker run -p 8085:8085 mujiks/material-requisition-demo --name demo

# Populate the database with some data
docker exec -it material_requisition_db psql -U postgres -f /scripts/insert_material.sql
(or just create your onwn records, you can download "pgadmin")


## Now try to perform some devolutions and requisitions

You can try with:

http://localhost:8085/swagger-ui.html (for internal) or
http://127.0.0.1:8085/swagger-ui.html 

Some of the payloads to test a devolution and a requisition:

{
  "email": "mail@rui.pt",
  "endDate": "2018-06-04T20:51:52.276Z",
  "materialType": "LAPTOP",
  "name": "devo1",
  "quantity": 2,
  "userId": "rui",
  "username": "Rui"
}

{
  "email": "mail@rui.pt",
  "materialType": "LAPTOP",
  "name": "req1",
  "numberOfDays": 10,
  "quantity": 1,
  "startDate": "2018-06-04T20:51:52.338Z",
  "userId": "rui",
  "username": "Rui"
}


  

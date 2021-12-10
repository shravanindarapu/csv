
First, created gencsv.sh file for generating random numbers as per the format.

Script for Number generation

#!/bin/bash

RANDOM=$$

for i in `seq 10`

do

echo $i, $RANDOM >> inputFile

done


Then executed docker run -d  --env CSVSERVER_BORDER=Orange -p 9393:9300   -v /home/ubuntu/csvserver/inputFile:/csvserver/inputdata infracloudio/csvserver:latest

which is used to extract docker image if not already present, run the container in detached mode, give environment variables,do manual port mapping and mount volume into the container mentioned

Then executed docker ps -a to cross check if the created container is up.

After completing PART I, now I have implemented same procedure in PART II with the help of docker-compose file using YAML.

version: "3.3"
services:
  app:
    image: infracloudio/csvserver:latest
    ports:
     - 9393:9300
    volumes:
      - /home/ubuntu/csvserver/solution/inputFile:/csvserver/inputdata
    environment:
     CSVSERVER_BORDER: Orange
  

Then using same docker compose file in the tags added prometheus image also 

version: "3.3"
services:
  app:
    image: infracloudio/csvserver:latest
    ports:
     - 9393:9300
    volumes:
      - /home/ubuntu/csvserver/solution/inputFile:/csvserver/inputdata
    environment:
     CSVSERVER_BORDER: Orange
  Prometheus:
    image: prom/prometheus:v2.22.0
    ports: 
     - 9090:9090
    volumes:
     - /home/ubuntu/csvserver/solution/prometheus.yml:/etc/prometheus/prometheus.yml

Also created prometheus.yml to add the info . 

global:
  scrape_interval:     5s
  evaluation_interval: 15s

rule_files:
  # - "first.rules"
  # - "second.rules"

scrape_configs:
  - job_name: 'prometheus'
    scrape_interval:     5s
    static_configs:
      - targets: ["54.161.234.63:9393"]
     
Screenshots of OUTPUT :

<img width="1792" alt="image" src="https://user-images.githubusercontent.com/95849201/145370268-d44d4781-1806-47fa-8234-ddf4de1af33a.png">


<img width="1792" alt="image" src="https://user-images.githubusercontent.com/95849201/145370114-454fb391-8fef-49bd-b67d-b96f93cd45ec.png">




# infracloud
# csv

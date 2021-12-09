
First, created gencsv.sh file for generating random numbers as per the format.
Then executed docker run -d  --env CSVSERVER_BORDER=Orange -p 9393:9300   -v /home/ubuntu/csvserver/inputFile:/csvserver/inputdata infracloudio/csvserver:latest

which is used to extract docker image if not already present, run the container in detached mode, give environment variables,do manual port mapping and mount volume into the container mentioned

Then executed docker ps -a to cross check if the created container is up.


# infracloud
# csv

# miniproject

## Welcome to Smiths' Brewery! 

This app allows the user to search the different breweries located by city, state and brewery name. Details inclue locations, website urls and phone numbers.


## How to run in terminal 
- enter ECS781P file 
- cd into file where test.py exists 

python test.py 

terminal will acitivate a link which will direct you to Smiths' Brewery

from the home page, user can navigate and locate different breweries depending on location 

## Running on gcp 

- Step 1: docker pull cassandra:latest

Step 2: docker run --name cassandra-test -d cassandra:latest

Step 3: wget -O brewersinfo.csv https://tinyurl.com/y6m9herz

Step 4: docker cp brewersinfo.csv cassandra-test:/home/brewersinfo.csv

Step 5: docker exec -it cassandra-test cqlsh

Step 7: CREATE TABLE brewerybeer.stats (ID int, Name text PRIMARY KEY, State text);

Step 8: COPY mydata.stats(ID, Name, State)
        FROM '/home/brewersinfo.csv'
        WITH DELIMITER=',' AND HEADER=TRUE;

Step 9: select * from brewerybeer.stats;]

## Kubernetes
Step 1: gcloud config set compute/zone europe-west2-b

Step 2: gcloud container clusters create cassandra --num-nodes=3 --machine-type "n1-standard-2"

Step 3: wget -O cassandra-peer-service.yml https://tinyurl.com/y6m9herz

Step 4: wget -O cassandra-service.yml https://tinyurl.com/y6m9herz

Step 5: wget -O cassandra-replication-controller.yml https://tinyurl.com/y6m9herz

Step 6: kubectl create -f cassandra-peer-service.yml

Step 7: kubectl scale rc cassandra --replicas=3

Step 8: kubectl create -f cassandra-replication-controller.yml

Step 9: kubectl get pods -l name=cassandra

Step 10: kubectl scale rc cassandra --replicas=3

Step 11: kubectl exec -it cassandra-2ggnn -- nodetool status

Step 12: kubectl cp brewersinfo.csv cassandra-2ggnn:/brewersinfo.csv

Step 13: kubectl exec -it cassandra-2ggnn cqlsh

Step 14: CREATE KEYSPACE mydata WITH REPLICATION =
        {'class' : 'SimpleStrategy', 'replication_factor' : 2};

Step 15: CREATE TABLE brewerybeer.stats (ID int, Name text PRIMARY KEY, State text);

Step 16: COPY brewerybeer.stats(ID, Name, State)
         FROM 'brewersinfo.csv'
         WITH DELIMITER=',' AND HEADER=TRUE;

Step 17: select * from brewerybeer.stats;



## Clean up
```
kubectl delete --all replicationcontroller
kubectl delete --all services
```

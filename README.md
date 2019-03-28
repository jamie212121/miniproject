# miniproject

Step 1: docker pull cassandra:latest

Step 2: docker run --name cassandra-test -d cassandra:latest

Step 3: wget -O brewersinfo.csv https://tinyurl.com/y6m9herz

Step 4: docker cp brewersinfo.csv cassandra-test:/home/brewersinfo.csv

Step 5: docker exec -it cassandra-test cqlsh

Step 7: CREATE TABLE brewerybeer.stats (ID int, Name text PRIMARY KEY, State text);

Step 8: COPY mydata.stats(ID, Name, State)
        FROM '/home/brewersinfo.csv'
        WITH DELIMITER=',' AND HEADER=TRUE;

Step 9: select * from brewerybeer.stats;


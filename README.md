# CSVServer Assignment

## Commands Executed

### Pull Docker Images

1.) docker pull infracloudio/csvserver:latest
2.) docker pull prom/prometheus:v2.45.2

### Run Container

---> docker run -d --name csvserver infracloudio/csvserver:latest

### Stop and Remove Container

1.) docker stop csvserver
2.) docker rm csvserver

###Generate Input File

[
#!/bin/bash
start=$1
end=$2

for i in $(seq $start $end)
do
    echo "$i, $RANDOM"
done > inputFile 
]
--->  ./gencsv.sh 2 8

###Run Container with Input File

---> docker run -d --name csvserver -v "$(pwd)/inputdata":/csvserver/inputdata -e CSVSERVER_BORDER=Orange -p 9393:9300 infracloudio/csvserver:latest

###Generate Output and Logs

---> curl -o ./part-1-output http://localhost:9393/raw

---> docker logs csvserver >& part-1-logs


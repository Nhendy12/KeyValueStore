# Shared Fault-Tolerant Key-Value Store with Casual Consistency

## Description
Sharded fault-tolerant key-value store supports three kinds of operations: view operations, shard operations, and key-value operations. The main endpoints for these operations are /key-value-store-view, /key-value-store-shard, and /key-value-store, respectively. The term view refers to the current set of nodes that are up and running. To do view operations, a node sends GET (for retrieving the view), PUT (for adding a new node to the view), and DELETE (for deleting a node from the view) requests to another node. In order to provide fault tolerance, each shard must contain atleast two nodes. Further description of the mechanisms is described in mechanism-description.txt.

To do key-value operations on key <key>, a client sends GET (for retrieving the value of key <key>), PUT (for adding the new key <key> or updating the value of the existing key <key>), and DELETE (for deleting key <key>) requests to the /key-value-store/<key> endpoint at a replica. The store returns a response in JSON format as well as the appropriate HTTP status code.
 
Test script test_assignment4.py can be ran to show accuracy.

# How to Run

## Build Docker Image
~~~bash
docker build -t KV-img .
~~~

## Run Docker Containers (replicas)
~~~bash
docker run -p 8082:8085 --net=mynet --ip=10.10.0.2 --name="node1" -e SOCKET_ADDRESS="10.10.0.2:8085" -e VIEW="10.10.0.2:8085,10.10.0.3:8085,10.10.0.4:8085,10.10.0.5:8085,10.10.0.6:8085,10.10.0.7:8085" -e SHARD_COUNT="2" KV-img

docker run -p 8083:8085 --net=mynet --ip=10.10.0.3 --name="node2" -e SOCKET_ADDRESS="10.10.0.3:8085" -e VIEW="10.10.0.2:8085,10.10.0.3:8085,10.10.0.4:8085,10.10.0.5:8085,10.10.0.6:8085,10.10.0.7:8085" -e SHARD_COUNT="2" KV-img

docker run -p 8084:8085 --net=mynet --ip=10.10.0.4 --name="node3" -e SOCKET_ADDRESS="10.10.0.4:8085" -e
VIEW="10.10.0.2:8085,10.10.0.3:8085,10.10.0.4:8085,10.10.0.5:8085,10.10.0.6:8085,10.10.0.7:8085" -e SHARD_COUNT="2" KV-img

docker run -p 8086:8085 --net=mynet --ip=10.10.0.5 --name="node4" -e SOCKET_ADDRESS="10.10.0.5:8085" -e
VIEW="10.10.0.2:8085,10.10.0.3:8085,10.10.0.4:8085,10.10.0.5:8085,10.10.0.6:8085,10.10.0.7:8085" -e SHARD_COUNT="2" KV-img

docker run -p 8087:8085 --net=mynet --ip=10.10.0.6 --name="node5" -e SOCKET_ADDRESS="10.10.0.6:8085" -e
VIEW="10.10.0.2:8085,10.10.0.3:8085,10.10.0.4:8085,10.10.0.5:8085,10.10.0.6:8085,10.10.0.7:8085" -e SHARD_COUNT="2" KV-img

docker run -p 8088:8085 --net=mynet --ip=10.10.0.7 --name="node6" -e SOCKET_ADDRESS="10.10.0.7:8085" -e
VIEW="10.10.0.2:8085,10.10.0.3:8085,10.10.0.4:8085,10.10.0.5:8085,10.10.0.6:8085,10.10.0.7:8085" -e SHARD_COUNT="2" KV-img
~~~

# Requests it supports

## GET Requests:
-$ curl --request GET --header "Content-Type: application/json" --write-out "\n%{http_code}\n" http://<node-socket-address>/key-value-store/<key>
 

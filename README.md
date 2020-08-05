# KeyValueStore

~~~bash
python ./main.py 
~~~
# Description
Sharded fault-tolerant key-value store supports three kinds of operations: view operations, shard operations, and key-value operations. The main endpoints for these operations are /key-value-store-view, /key-value-store-shard, and /key-value-store, respectively. The term view refers to the current set of nodes that are up and running. To do view operations, a node sends GET (for retrieving the view), PUT (for adding a new node to the view), and DELETE (for deleting a node from the view) requests to another node. In order to provide fault tolerance, each shard must contain atleast two nodes. Further description of the mechanisms is described in mechanism-description.txt.

To do key-value operations on key <key>, a client sends GET (for retrieving the value of key <key>), PUT (for adding the new key <key> or updating the value of the existing key <key>), and DELETE (for deleting key <key>) requests to the /key-value-store/<key> endpoint at a replica. The store returns a response in JSON format as well as the appropriate HTTP status code.

# GET Requests:
-$ curl --request GET --header "Content-Type: application/json" --write-out "\n%{http_code}\n" http://<node-socket-address>/key-value-store/<key>
 

### NATS Streaming clustering
A breef description of the NATS Streaming cluster, with references to Kafka, can be found here: [NATS Streaming Cluster](https://bravenewgeek.com/building-a-distributed-log-from-scratch-part-2-data-replication/)

NATS Streaming cluster was tested with the version 0.10.0, starting from NATS Streaming Go sources.
Three nodes (a, b, c) were configured to build a cluster on the localhost.

The configuration files for each node:
- n1.conf:
```
port: 4222
http_port: 5222  # HTTP monitoring port
cluster {
  listen: 0.0.0.0:6222
  routes: ["nats://localhost:6223", "nats://localhost:6224"]
}
streaming {
  store: file
  dir: "c:\\temp\\natss_a"
  cluster {
    node_id: "a"
    peers: ["b", "c"]
  }
}
```
 - n2.conf:
 ```
 port: 4223
 http_port: 5223  # HTTP monitoring port
 cluster {
   listen: 0.0.0.0:6223
   routes: ["nats://localhost:6224", "nats://localhost:6222"]
 }
 streaming {
   store: file
   dir: "c:\\temp\\natss_b"
   cluster {
     node_id: "b"
     peers: ["c", "a"]
   }
}
```
- n3.conf:
```
port: 4224
http_port: 5224  # HTTP monitoring port
cluster {
  listen: 0.0.0.0:6224
  routes: ["nats://localhost:6222", "nats://localhost:6223"]
}
streaming {
  store: file
  dir: "c:\\temp\\natss_c"
  cluster {
    node_id: "c"
    peers: ["a", "b"]
  }
}
```    

The start the cluster, each node should be manually started:
```
>go run nats-streaming-server.go --clustered -sc n1.conf
>go run nats-streaming-server.go --clustered -sc n2.conf
>go run nats-streaming-server.go --clustered -sc n3.conf
``` 

To test the NATS Streaming cluster, the examples from NATS Streaming repository were used:
- to publish a message to node a :
```
go run examples/stan-pub/main.go -s nats://localhost:4222 -id pub_a foo "msg 1"
```
- to subscribe to the channel "foo" on node b:
```
go run examples/stan-sub/main.go --all -s nats://localhost:4223 -c test-cluster -id sub_b foo
```
A small reliability cluster tests was done (killing one node, restart it...)
No message was lost during these tests.

NATSS implements a kind of "lazy persistence replication of data" based on RAFT log. The RAFT logs, which contains the "messages", are replicated to the "persistence storage" of the new elected leader at the first "write action" which changes the RAFT log status (publish a message to an active node in cluster). It worked.

The fail over of subscriber is also supported by NATS Sreaming cluster, so that the subscriber must not reconnect if, for  example, node b was down.

    
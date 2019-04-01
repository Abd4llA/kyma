### Overview
The monitoring port is defined as a paramater in the config file og NATS Streaming or as a command line parameter: "-m 5222" 


### Monitoring of the embedded NATS
NATS monitoring documentation: [NATS Monitoring](https://nats.io/documentation/server/gnatsd-monitoring/)

Additional tools:
- A top like tool: [nats-top](https://nats.io/documentation/server/gnatsd-top/)
- A benchmark too: [nats-bench](https://nats.io/documentation/tutorials/nats-benchmarking/)
- The Prometheus NATS Exporter: [prometheus-nats-exporter](https://github.com/nats-io/prometheus-nats-exporter) 

URLs for monitoring the local NATS (embedded in the local NATS Streaming):
- root entry point "http://localhost:5222"

- Various general NATS server statistics: "http://localhost:5222/varz"

    Sample response from node a:
```
{
  "server_id": "PhpilAKmXKSEIWqxzm7MiI",
  "version": "1.0.7",
  "git_commit": "",
  "go": "go1.9.2",
  "host": "0.0.0.0",
  "auth_required": false,
  "ssl_required": false,
  "tls_required": false,
  "tls_verify": false,
  "connect_urls": [
    "10.0.75.1:4222",
    "10.27.78.202:4222",
    "10.0.75.1:4223",
    "10.27.78.202:4223",
    "10.0.75.1:4224",
    "10.27.78.202:4224"
  ],
  "addr": "0.0.0.0",
  "max_connections": 65536,
  "ping_interval": 120000000000,
  "ping_max": 2,
  "http_host": "0.0.0.0",
  "http_port": 5222,
  "https_port": 0,
  "auth_timeout": 1,
  "max_control_line": 1024,
  "cluster": {
    "addr": "0.0.0.0",
    "cluster_port": 6222,
    "auth_timeout": 1
  },
  "tls_timeout": 0.5,
  "port": 4222,
  "max_payload": 1048576,
  "start": "2018-06-06T08:10:28.4592452+02:00",
  "now": "2018-06-06T08:36:16.4438818+02:00",
  "uptime": "25m48s",
  "mem": 23154688,
  "cores": 8,
  "cpu": 0,
  "connections": 4,
  "total_connections": 4,
  "routes": 2,
  "remotes": 2,
  "in_msgs": 101072,
  "out_msgs": 100956,
  "in_bytes": 8795680,
  "out_bytes": 8783395,
  "slow_consumers": 0,
  "subscriptions": 30,
  "http_req_stats": {
    "/": 0,
    "/connz": 1,
    "/routez": 1,
    "/subsz": 1,
    "/varz": 1
  },
  "config_load_time": "2018-06-06T08:10:28.4592452+02:00"
}
```

- Detailed information on current connections: "http://localhost:5222/connz"

    Sample response from node a:
```
{
  "server_id": "PhpilAKmXKSEIWqxzm7MiI",
  "now": "2018-06-06T08:34:33.7744145+02:00",
  "num_connections": 4,
  "total": 4,
  "offset": 0,
  "limit": 1024,
  "connections": [
    {
      "cid": 1,
      "ip": "127.0.0.1",
      "port": 50262,
      "start": "2018-06-06T08:10:28.6744436+02:00",
      "last_activity": "2018-06-06T08:10:28.6744436+02:00",
      "uptime": "24m5s",
      "idle": "24m5s",
      "pending_bytes": 0,
      "in_msgs": 0,
      "out_msgs": 0,
      "in_bytes": 0,
      "out_bytes": 0,
      "subscriptions": 0,
      "name": "_NSS-test-cluster-send",
      "lang": "go",
      "version": "1.3.1"
    },
    {
      "cid": 2,
      "ip": "127.0.0.1",
      "port": 50263,
      "start": "2018-06-06T08:10:28.6754412+02:00",
      "last_activity": "2018-06-06T08:30:04.6489055+02:00",
      "uptime": "24m5s",
      "idle": "4m29s",
      "pending_bytes": 0,
      "in_msgs": 11,
      "out_msgs": 0,
      "in_bytes": 0,
      "out_bytes": 0,
      "subscriptions": 9,
      "name": "_NSS-test-cluster-general",
      "lang": "go",
      "version": "1.3.1"
    },
    {
      "cid": 3,
      "ip": "127.0.0.1",
      "port": 50264,
      "start": "2018-06-06T08:10:28.6776379+02:00",
      "last_activity": "2018-06-06T08:34:33.7428932+02:00",
      "uptime": "24m5s",
      "idle": "0s",
      "pending_bytes": 0,
      "in_msgs": 46596,
      "out_msgs": 46485,
      "in_bytes": 5358632,
      "out_bytes": 2742788,
      "subscriptions": 8,
      "name": "_NSS-test-cluster-raft",
      "lang": "go",
      "version": "1.3.1"
    },
    {
      "cid": 4,
      "ip": "127.0.0.1",
      "port": 50265,
      "start": "2018-06-06T08:10:28.6794424+02:00",
      "last_activity": "2018-06-06T08:30:04.6484063+02:00",
      "uptime": "24m5s",
      "idle": "4m29s",
      "pending_bytes": 0,
      "in_msgs": 0,
      "out_msgs": 0,
      "in_bytes": 0,
      "out_bytes": 0,
      "subscriptions": 1,
      "name": "_NSS-test-cluster-raft_snap",
      "lang": "go",
      "version": "1.3.1"
    }
  ]
}
```

- Detailed information about the current subscriptions: "http://localhost:5222/subsz"

    Sample response from node a:
```
{
  "num_subscriptions": 30,
  "num_cache": 21,
  "num_inserts": 148,
  "num_removes": 118,
  "num_matches": 970,
  "cache_hit_rate": 0.9742268041237113,
  "max_fanout": 1,
  "avg_fanout": 0.9523809523809523
}
```

- cluster topology (routes): "http://localhost:5222/routez"

Sample response from node a of the three node cluster (a, b, c):
```
{
  "server_id": "PhpilAKmXKSEIWqxzm7MiI",
  "now": "2018-06-06T08:28:33.8462742+02:00",
  "num_routes": 2,
  "routes": [
    {
      "rid": 5,
      "remote_id": "pvtV66EqmWLIg6C0wJDu7q",
      "did_solicit": true,
      "is_configured": true,
      "ip": "::1",
      "port": 50271,
      "pending_size": 0,
      "in_msgs": 21353,
      "out_msgs": 21353,
      "in_bytes": 1259855,
      "out_bytes": 2455663,
      "subscriptions": 5
    },
    {
      "rid": 7,
      "remote_id": "394BZw7jzkrEpZrogE82rN",
      "did_solicit": true,
      "is_configured": true,
      "ip": "::1",
      "port": 63940,
      "pending_size": 0,
      "in_msgs": 11205,
      "out_msgs": 11205,
      "in_bytes": 661230,
      "out_bytes": 1288561,
      "subscriptions": 7
    }
  ]
}
```


### Monitoring of NATS Streaming
NATS Streaming monitoring documentation: [NATS Streaming Monitoring]()

URL for monitoring the local NATS Streaming: "http://localhost:5222/streaming"

NATS Streaming exposes in addition to the NATS monitoring endpoints:
- Describes the NATS Streaming Server "http://localhost:5222/streaming/serverz"

    Sample response from node a:
```
{
  "cluster_id": "test-cluster",
  "server_id": "8fACJ34LGvkmlEn7VBrcfL",
  "version": "0.10.0",
  "go": "go1.9.2",
  "state": "CLUSTERED",
  "now": "2018-06-06T08:39:28.6833895+02:00",
  "start_time": "2018-06-06T08:10:28.4512446+02:00",
  "uptime": "29m0s",
  "clients": 0,
  "subscriptions": 3,
  "channels": 1,
  "total_msgs": 7,
  "total_bytes": 448
}
```

- Describes the NATS Streaming Store: "http://localhost:5222/streaming/storez"

    Sample response from node a:
```
{
  "cluster_id": "test-cluster",
  "server_id": "8fACJ34LGvkmlEn7VBrcfL",
  "now": "2018-06-06T08:41:20.8266252+02:00",
  "type": "RAFT_FILE",
  "limits": {
    "max_channels": 100,
    "max_msgs": 1000000,
    "max_bytes": 1024000000,
    "max_age": 0,
    "max_subscriptions": 1000,
    "MaxInactivity": 0
  },
  "total_msgs": 7,
  "total_bytes": 448
}
```

- Describes a NATS Streaming Client connections: "http://localhost:5222/streaming/clientsz"

    Sample response from node a:
```
{
  "cluster_id": "test-cluster",
  "server_id": "8fACJ34LGvkmlEn7VBrcfL",
  "now": "2018-06-06T08:43:43.2011417+02:00",
  "offset": 0,
  "limit": 1024,
  "count": 0,
  "total": 0,
  "clients": []
}
```
- Describes NATS Streaming Channels: "http://localhost:5222/streaming/channelsz"

    Sample response from node a:
```
{
  "cluster_id": "test-cluster",
  "server_id": "8fACJ34LGvkmlEn7VBrcfL",
  "now": "2018-06-06T08:44:47.9606064+02:00",
  "offset": 0,
  "limit": 1024,
  "count": 1,
  "total": 1,
  "names": [
    "foo"
  ]
}
```
 - Describe a channel: "http://localhost:5222/streaming/channelsz?channel=foo&subs=1"
 
    Sample response from node a:
    
```
{
  "name": "foo",
  "msgs": 7,
  "bytes": 448,
  "first_seq": 1,
  "last_seq": 7
}
```    

The "monitoring" part of NATS Streaming is a work in progress. 

The Prometheus NATS Exporter could be extended to export information from NATS-Streaming monitoring endpoints too.


The monitoring of NATS Streaming cluster status can be obtained using NATS "routez" endpoint.
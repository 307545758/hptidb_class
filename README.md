# hptidb_class


## 安装配置步骤
pd-server配置文件  
```
client-urls="http://0.0.0.0:4205"
name="pd1"
data-dir="/home/work/opdir/chenliang/go/data/pd1"
peer-urls="http://0.0.0.0:4206"
initial-cluster="pd1=http://0.0.0.0:4206"
log-file="/home/work/opdir/chenliang/go/logs/pd1.log"
```

3份tikv-server配置文件
```
work@hostname:~/opdir/chenliang/go/conf$ more tikv1.conf
log-level = "info"
log-file = "/home/work/opdir/chenliang/go/logs/tikv1.log"
[server]
addr = "127.0.0.1:4402"
[storage]
data-dir = "/home/work/opdir/chenliang/go/data/tikv1"
scheduler-concurrency = 1024000
scheduler-worker-pool-size = 100
[pd]
endpoints = ["0.0.0.0:4205"]
[metric]
interval = "15s"
address = ""
job = "tikv"
[raftstore]
sync-log = false
region-max-size = "384MB"
region-split-size = "256MB"
[rocksdb]
max-background-jobs = 28
max-open-files = 409600
max-manifest-file-size = "20MB"
compaction-readahead-size = "20MB"
[rocksdb.defaultcf]
block-size = "64KB"
compression-per-level = ["no", "no", "lz4", "lz4", "lz4", "zstd", "zstd"]
write-buffer-size = "128MB"
max-write-buffer-number = 10
level0-slowdown-writes-trigger = 20
level0-stop-writes-trigger = 36
max-bytes-for-level-base = "512MB"
target-file-size-base = "32MB"
[rocksdb.writecf]
compression-per-level = ["no", "no", "lz4", "lz4", "lz4", "zstd", "zstd"]
write-buffer-size = "128MB"
max-write-buffer-number = 5
min-write-buffer-number-to-merge = 1
max-bytes-for-level-base = "512MB"
target-file-size-base = "32MB"
[raftdb]
max-open-files = 409600
compaction-readahead-size = "20MB"
[raftdb.defaultcf]
compression-per-level = ["no", "no", "lz4", "lz4", "lz4", "zstd", "zstd"]
write-buffer-size = "128MB"
max-write-buffer-number = 5
min-write-buffer-number-to-merge = 1
max-bytes-for-level-base = "512MB"
target-file-size-base = "32MB"
block-cache-size = "10G"
```

```
work@hostname:~/opdir/chenliang/go/conf$ more tikv2.conf
log-level = "info"
log-file = "/home/work/opdir/chenliang/go/logs/tikv2.log"
[server]
addr = "127.0.0.1:4403"
[storage]
data-dir = "/home/work/opdir/chenliang/go/data/tikv2"
scheduler-concurrency = 1024000
scheduler-worker-pool-size = 100
[pd]
endpoints = ["0.0.0.0:4205"]
[metric]
interval = "15s"
address = ""
job = "tikv"
[raftstore]
sync-log = false
region-max-size = "384MB"
region-split-size = "256MB"
[rocksdb]
max-background-jobs = 28
max-open-files = 409600
max-manifest-file-size = "20MB"
compaction-readahead-size = "20MB"
[rocksdb.defaultcf]
block-size = "64KB"
compression-per-level = ["no", "no", "lz4", "lz4", "lz4", "zstd", "zstd"]
write-buffer-size = "128MB"
max-write-buffer-number = 10
level0-slowdown-writes-trigger = 20
level0-stop-writes-trigger = 36
max-bytes-for-level-base = "512MB"
target-file-size-base = "32MB"
[rocksdb.writecf]
compression-per-level = ["no", "no", "lz4", "lz4", "lz4", "zstd", "zstd"]
write-buffer-size = "128MB"
max-write-buffer-number = 5
min-write-buffer-number-to-merge = 1
max-bytes-for-level-base = "512MB"
target-file-size-base = "32MB"
[raftdb]
max-open-files = 409600
compaction-readahead-size = "20MB"
[raftdb.defaultcf]
compression-per-level = ["no", "no", "lz4", "lz4", "lz4", "zstd", "zstd"]
write-buffer-size = "128MB"
max-write-buffer-number = 5
min-write-buffer-number-to-merge = 1
max-bytes-for-level-base = "512MB"
target-file-size-base = "32MB"
block-cache-size = "10G"
```

```
work@hostname:~/opdir/chenliang/go/conf$ more tikv3.conf
log-level = "info"
log-file = "/home/work/opdir/chenliang/go/logs/tikv3.log"
[server]
addr = "127.0.0.1:4404"
[storage]
data-dir = "/home/work/opdir/chenliang/go/data/tikv3"
scheduler-concurrency = 1024000
scheduler-worker-pool-size = 100
[pd]
endpoints = ["0.0.0.0:4205"]
[metric]
interval = "15s"
address = ""
job = "tikv"
[raftstore]
sync-log = false
region-max-size = "384MB"
region-split-size = "256MB"
[rocksdb]
max-background-jobs = 28
max-open-files = 409600
max-manifest-file-size = "20MB"
compaction-readahead-size = "20MB"
[rocksdb.defaultcf]
block-size = "64KB"
compression-per-level = ["no", "no", "lz4", "lz4", "lz4", "zstd", "zstd"]
write-buffer-size = "128MB"
max-write-buffer-number = 10
level0-slowdown-writes-trigger = 20
level0-stop-writes-trigger = 36
max-bytes-for-level-base = "512MB"
target-file-size-base = "32MB"
[rocksdb.writecf]
compression-per-level = ["no", "no", "lz4", "lz4", "lz4", "zstd", "zstd"]
write-buffer-size = "128MB"
max-write-buffer-number = 5
min-write-buffer-number-to-merge = 1
max-bytes-for-level-base = "512MB"
target-file-size-base = "32MB"
[raftdb]
max-open-files = 409600
compaction-readahead-size = "20MB"
[raftdb.defaultcf]
compression-per-level = ["no", "no", "lz4", "lz4", "lz4", "zstd", "zstd"]
write-buffer-size = "128MB"
max-write-buffer-number = 5
min-write-buffer-number-to-merge = 1
max-bytes-for-level-base = "512MB"
target-file-size-base = "32MB"
block-cache-size = "10G"
```

tidb-server配置文件
```
work@hostname:~/opdir/chenliang/go/conf$ more tidb.conf
host = "0.0.0.0"
port = 4000
store = "tikv"
path = "127.0.0.1:4205"
socket = ""
run-ddl = true
lease = "45s"
split-table = true
token-limit = 1000
oom-action = "log"
enable-streaming = false
lower-case-table-names = 2
[log]
level = "info"
format = "text"
disable-timestamp = false
slow-query-file = ""
slow-threshold = 300
expensive-threshold = 10000
query-log-max-len = 2048
[log.file]
filename = "/home/work/opdir/chenliang/go/logs/tidb.log"
max-size = 300
max-days = 0
max-backups = 0
log-rotate = true
[security]
ssl-ca = ""
ssl-cert = ""
ssl-key = ""
cluster-ssl-ca = ""
cluster-ssl-cert = ""
cluster-ssl-key = ""
[status]
report-status = true
status-port = 10080  #报告tidb状态的通讯端口
metrics-addr = ""
metrics-interval = 15
[performance]
max-procs = 0
stmt-count-limit = 5000
tcp-keep-alive = true
cross-join = true
stats-lease = "3s"
run-auto-analyze = true
feedback-probability = 0.05
query-feedback-limit = 1024
pseudo-estimate-ratio = 0.8
[proxy-protocol]
networks = ""
header-timeout = 5
[plan-cache]
enabled = false
capacity = 2560
shards = 256
[prepared-plan-cache]
enabled = false
capacity = 100
[opentracing]
enable = false
rpc-metrics = false
[opentracing.sampler]
type = "const"
param = 1.0
sampling-server-url = ""
max-operations = 0
sampling-refresh-interval = 0
[opentracing.reporter]
queue-size = 0
buffer-flush-interval = 0
log-spans = false
local-agent-host-port = ""
[tikv-client]
grpc-connection-count = 16
commit-timeout = "41s"
[txn-local-latches]
enabled = false
capacity = 1024000
[binlog]
binlog-socket = ""

```

按顺序启动pd-server tikv-server tidb-server
```
/home/work/opdir/chenliang/go/bin/pd-server  --config=/home/work/opdir/chenliang/go/conf/tipd.conf  &
/home/work/opdir/chenliang/go/bin/tikv-server  --config=/home/work/opdir/chenliang/go/conf/tikv1.conf &
/home/work/opdir/chenliang/go/bin/tikv-server  --config=/home/work/opdir/chenliang/go/conf/tikv2.conf &
/home/work/opdir/chenliang/go/bin/tikv-server  --config=/home/work/opdir/chenliang/go/conf/tikv3.conf &
/home/work/opdir/chenliang/go/bin/tidb-server --config=/home/work/opdir/chenliang/go/conf/tidb.conf &
```

检查状态
```
[root@hostname2 ~]# /home/work/tidb-ansible/resources/bin/pd-ctl -u http://10.162.38.50:4205 member
{
  "header": {
    "cluster_id": 6861491347362968738
  },
  "members": [
    {
      "name": "pd1",
      "member_id": 9536465514685824554,
      "peer_urls": [
        "http://0.0.0.0:4206"
      ],
      "client_urls": [
        "http://0.0.0.0:4205"
      ]
    }
  ],
  "leader": {
    "name": "pd1",
    "member_id": 9536465514685824554,
    "peer_urls": [
      "http://0.0.0.0:4206"
    ],
    "client_urls": [
      "http://0.0.0.0:4205"
    ]
  },
  "etcd_leader": {
    "name": "pd1",
    "member_id": 9536465514685824554,
    "peer_urls": [
      "http://0.0.0.0:4206"
    ],
    "client_urls": [
      "http://0.0.0.0:4205"
    ]
  }
}

[root@hostname2 ~]# /home/work/tidb-ansible/resources/bin/pd-ctl -u http://10.162.38.50:4205 store
{
  "count": 3,
  "stores": [
    {
      "store": {
        "id": 1,
        "address": "127.0.0.1:4402",
        "version": "3.0.2",
        "state_name": "Up"
      },
      "status": {
        "capacity": "2.1 TiB",
        "available": "2.0 TiB",
        "leader_count": 7,
        "leader_weight": 1,
        "leader_score": 7,
        "leader_size": 7,
        "region_count": 19,
        "region_weight": 1,
        "region_score": 19,
        "region_size": 19,
        "start_ts": "2020-08-16T21:01:27+08:00",
        "last_heartbeat_ts": "2020-08-16T21:02:37.264335734+08:00",
        "uptime": "1m10.264335734s"
      }
    },
    {
      "store": {
        "id": 4,
        "address": "127.0.0.1:4403",
        "version": "3.0.2",
        "state_name": "Up"
      },
      "status": {
        "capacity": "2.1 TiB",
        "available": "2.0 TiB",
        "leader_count": 7,
        "leader_weight": 1,
        "leader_score": 7,
        "leader_size": 7,
        "region_count": 19,
        "region_weight": 1,
        "region_score": 19,
        "region_size": 19,
        "start_ts": "2020-08-16T21:01:34+08:00",
        "last_heartbeat_ts": "2020-08-16T21:02:34.397455954+08:00",
        "uptime": "1m0.397455954s"
      }
    },
    {
      "store": {
        "id": 6,
        "address": "127.0.0.1:4404",
        "version": "3.0.2",
        "state_name": "Up"
      },
      "status": {
        "capacity": "2.1 TiB",
        "available": "2.0 TiB",
        "leader_count": 5,
        "leader_weight": 1,
        "leader_score": 5,
        "leader_size": 5,
        "region_count": 19,
        "region_weight": 1,
        "region_score": 19,
        "region_size": 19,
        "start_ts": "2020-08-16T21:01:41+08:00",
        "last_heartbeat_ts": "2020-08-16T21:02:41.069024284+08:00",
        "uptime": "1m0.069024284s"
      }
    }
  ]
}
```

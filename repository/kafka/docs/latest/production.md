![kudo-kafka](./resources/images/kudo-kafka.png)

# Running KUDO Kafka in production



## Kubernetes checks

- Verify the storage class features





## Durability over performance

This document 

### Replication Factor

Change the default replication factor from the default 1 to 3

```
DEFAULT_REPLICATION_FACTOR=3
```

### Minimum Insync Replicas

When a producer sets acks to `all` (or `-1`) `MIN_INSYNC_REPLICAS` is the minimum number of replicas that must acknowledge a write for the write to be considered successful.
When used together, `min.insync.replicas` and `acks` allow Apache Kafka users to enforce greater durability guarantees.

To guarantee the messages durability a recommended practice would be to create a topic with a replication factor of `3`, set `MIN_INSYNC_REPLICAS` to `2`, and produce messages with acks of `all`.

```
MIN_INSYNC_REPLICAS=2
```

### Graceful rolling restarts

KUDO Kafka enables by default the option `CONTROLLED_SHUTDOWN_ENABLE` to true. To ensure a faster flush during shutdown and faster recovery during the bootstrap `num.recovery.threads.per.data.dir` should be increased from default `1` thread.

```
NUM_RECOVERY_THREADS_PER_DATA_DIR=3
```
# Subutai Minio Blueprint 

**Subutai Minio Blueprint** to install MinIO in distributed mode.

**How to enable https:**

Add port mapping to all containers: external port is https **443** and internal port is **9199**, **ssl_backend** should be enabled,  provide **custom SSL certificate** in format with one file: 
```
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----

-----BEGIN PRIVATE KEY-----
...
-----END PRIVATE KEY-----
```

### NOTE:
```
1) Minio designed to deploy once and forget. You can not add new disks to an existing setup.
2) Minio does not support adding new nodes
3) Cluster will work while (nodes_count/2+1) is up 
```

## Useful
MinIO Client (mc) provides a modern alternative to UNIX commands like ls, cat, cp, mirror, diff, find etc.

Add node to mc client 
```
mc config host add minio http://node-ip:9199 accessKey secretKey
```

Info about cluster

```
mc admin info minio
```

Sync minio node
```
mc admin heal -r minio

```
Add bucket
```
mc mb minio/mybucket
```

### How to fix died node: 

1) Fix corrupted disk
2) Make sure that minio service started
3) Sync minio node with cmd: `mc admin heal -r minio`


---
sidebar: auto
sidebarDepth: 1
---

# Config

The Finders configuration file does not use JSON or YAML, but a more readable configuration file format [TOML](https://github.com/toml-lang/toml). The configuration file is named [finders.toml](https://github.com/dxx/finders/blob/main/distribution/conf/finders.toml).

## Basic Config

The basic service configuration uses `server` as the key name.

### port

* Type: `integer`
* Default: `9080`

Specify the port on which the service runs.

### backlog

* Type: `integer`
* Default: `128`

The TCP client connection queue size.

### rcvBufSize

* Type: `integer`
* Default: `131072`

The TCP receive buffer size. The unit is bytes.

### sndBufSize

* Type: `integer`
* Default: `131072`

The TCP send buffer size. The unit is bytes.

## Cluster Config

The cluster configuration uses `cluster` as the key name.

```toml
[cluster]
selfId = "n0"
nodes = ["n0-127.0.0.1:9080", "n1-127.0.0.1:9081", "n2-127.0.0.1:9082"]
```

### selfId

* Type: `string`
* Default: `null`

Specifies the id of the node. The ID must be unique in the cluster.

### nodes
* Type: `array`
* Default: `null`

Configure information about all nodes in the cluster, including node id, IP addresse and port. Format: selId-host :port, for example:

```toml
nodes = ["n0-127.0.0.1:9080", "n1-127.0.0.1:9081", "n2-127.0.0.1:9082"]
```

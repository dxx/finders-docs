---
sidebar: auto
sidebarDepth: 1
---

# 配置

Finders 的配置文件没有使用 JSON 或者 YAML ，而是使用更加易读的配置文件格式 [TOML](https://github.com/toml-lang/toml)。配置文件名为 [finders.toml](https://github.com/dxx/finders/blob/main/distribution/conf/finders.toml)。

## 基本配置

服务基本配置以 `server` 作为键名。

### port

* 类型：`integer`
* 默认值：`9080`

指定服务运行的端口。

### backlog

* 类型：`integer`
* 默认值：`128`

TCP 客户端连接队列大小。

### rcvBufSize

* 类型：`integer`
* 默认值：`131072`

TCP 接收缓冲区大小。以字节为单位。

### sndBufSize

* 类型：`integer`
* 默认值：`131072`

TCP 发送缓冲区大小。以字节为单位。

## 集群配置

集群配置以 `cluster` 作为键名。

```toml
[cluster]
selfId = "n0"
nodes = ["n0-127.0.0.1:9080", "n1-127.0.0.1:9081", "n2-127.0.0.1:9082"]
```

### selfId

* 类型：`string`
* 默认值：`空`

指定节点的 id，id 必须在集群中唯一。

### nodes
* 类型：`array`
* 默认值：`空`

配置集群中所有节点信息，包含节点 id、IP 地址和端口。格式：selfId-host:port，如：

```toml
nodes = ["n0-127.0.0.1:9080", "n1-127.0.0.1:9081", "n2-127.0.0.1:9082"]
```

# Instance API

## Query Instance List

### Description

Query for all instances of the specified service.

### Request Method

GET

### Request Path

```
/api/instance/list
```

### Request Parameter

Parameter Type: Query

Parameter List:

| Name        | Type   | Required | Description                                                  |
| ----------- | ------ | -------- | ------------------------------------------------------------ |
| namespace   | string | no       | Namespace. Default is `default`                              |
| clusters    | string | no       | Cluster name. Multiple clusters were segmented using `, `. Default is empty |
| serviceName | string | yes      | Service name                                                 |
| healthy     | boolean | no      | Health status. Default is all status                         |

### Request Example

```shell
GET http://localhost:9080/api/instance/list?namespace=&clusters=&serviceName=serviceTest&healthy=
```

Response:

```json
{
  "serviceName": "serviceTest",
  "clusters": [
    "DEFAULT_CLUSTER"
  ],
  "instances": [
    {
      "instanceId": "DEFAULT_CLUSTER#serviceTest@127.0.0.1:8080",
      "cluster": "DEFAULT_CLUSTER",
      "serviceName": "serviceTest",
      "ip": "127.0.0.1",
      "port": 8080,
      "status": "HEALTHY"
    }
  ]
}
```



## Query Instance

### Description

Query specified instance.

### Request Method

GET

### Request Path

```
/api/instance
```

### Request Parameter

Parameter Type: Query

Parameter List:

| Name        | Type   | Required | Description                                    |
| ----------- | ------ | -------- | ---------------------------------------------- |
| namespace   | string | no       | Namespace. Default is `default`                |
| cluster     | string | no       | Cluster name. Default is `DEFAULT_CLUSTER`     |
| serviceName | string | yes      | Service name                                   |
| ip          | string | yes      | IP of Instance                                 |
| port        | int    | yes      | Port of Instance                               |

### Request Example

```shell
GET http://localhost:9080/api/instance?namespace=&cluster=&serviceName=serviceTest&ip=127.0.0.1&port=8080
```

Response: 

```json
{
  "instanceId": "DEFAULT_CLUSTER#serviceTest@127.0.0.1:8080",
  "cluster": "DEFAULT_CLUSTER",
  "serviceName": "serviceTest",
  "ip": "127.0.0.1",
  "port": 8080,
  "status": "HEALTHY"
}
```



## Register Instance

### Description

Register a service instance, it is automatically created when the service does not exist.

### Request Method

POST

### Request Path

```
/api/instance
```

### Request Parameter

Parameter Type: `Content-Type: application/json`

Parameter List:

| Name        | Type   | Required | Description                                    |
| ----------- | ------ | -------- | ---------------------------------------------- |
| namespace   | string | no       | Namespace. Default is `default`                |
| cluster     | string | no       | Cluster name. Default is `DEFAULT_CLUSTER`     |
| serviceName | string | yes      | Service name                                   |
| ip          | string | yes      | IP of Instance                                 |
| port        | int    | yes      | Port of Instance                               |

### Request Example

```shell
POST http://localhost:9080/api/instance
Content-Type: application/json

{
  "namespace": "default",
  "cluster": "DEFAULT_CLUSTER",
  "serviceName": "serviceTest",
  "ip": "127.0.0.1",
  "port": 8080
}
```

Response:

```
success
```



## Deregister Instance

### Description

Deregister a service instance.

### Request Method

DELETE

### Request Path

```
/api/instance
```

### Request Parameter

Parameter Type: `Content-Type: application/json`

Parameter List:

| Name        | Type   | Required  | Description                                    |
| ----------- | ------ | --------- | ---------------------------------------------- |
| namespace   | string | no        | Namespace. Default is `default`                |
| cluster     | string | no        | Cluster name. Default is `DEFAULT_CLUSTER`     |
| serviceName | string | yes       | Service name                                   |
| ip          | string | yes       | IP of Instance                                 |
| port        | int    | yes       | Port of Instance                               |

### Request Example

```shell
DELETE http://localhost:9080/api/instance
Content-Type: application/json

{
  "namespace": "default",
  "cluster": "DEFAULT_CLUSTER",
  "serviceName": "serviceTest",
  "ip": "127.0.0.1",
  "port": 8080
}
```

Response:

```
success
```



## Send Instance Heartbeat

### Description

Send a heartbeat to the specified instance.

> Note: The heartbeat request is invalid when the instance is disable.

### Request Method

PUT

### Request Path

```
/api/instance/beat
```

### Request Parameter

Parameter Type: `Content-Type: application/json`

Parameter List:

| Name        | Type   | Required  | Description                                    |
| ----------- | ------ | --------- | ---------------------------------------------- |
| namespace   | string | no        | Namespace. Default is `default`                |
| cluster     | string | no        | Cluster name. Default is `DEFAULT_CLUSTER`     |
| serviceName | string | yes       | Service name                                   |
| ip          | string | yes       | IP of Instance                                 |
| port        | int    | yes       | Port of Instance                               |

### Request Example

```shell
PUT http://localhost:9080/api/instance/beat
Content-Type: application/json

{
  "namespace": "default",
  "cluster": "DEFAULT_CLUSTER",
  "serviceName": "serviceTest",
  "ip": "127.0.0.1",
  "port": 8080
}
```

Response:

```
success
```



## Modify instance status

### Description

Modify the status of the specified instance.

### Request Method

PUT

### Request Path

```
/api/instance/status
```

### Request Parameter

Parameter Type: `Content-Type: application/json`

Parameter List:

| Name        | Type   | Required  | Description                                      |
| ----------- | ------ | --------- | ------------------------------------------------ |
| namespace   | string | no        | Namespace. Default is `default`                  |
| cluster     | string | no        | Cluster name. Default is `DEFAULT_CLUSTER`       |
| serviceName | string | yes       | Service name                                     |
| ip          | string | yes       | IP of Instance                                   |
| port        | int    | yes       | Port of Instance                                 |
| status      | string | yes       | Status of Instance. `HEALTHY`, `UN_HEALTHY`, `DISABLE`|

### Request Example

```shell
PUT http://localhost:9080/api/instance/status
Content-Type: application/json

{
  "namespace": "default",
  "cluster": "DEFAULT_CLUSTER",
  "serviceName": "serviceTest",
  "ip": "127.0.0.1",
  "port": 8080,
  "status": "DISABLE"
}
```

Response:

```
success
```

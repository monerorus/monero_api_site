## **get_connections**

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_connections"}' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "connections": [{
      "address": "173.90.69.136:62950",
      "avg_download": 0,
      "avg_upload": 2,
      "connection_id": "083c301a3030329a487adb12ad981d2c",
      "current_download": 0,
      "current_upload": 2,
      "height": 1562127,
      "host": "173.90.69.136",
      "incoming": true,
      "ip": "173.90.69.136",
      "live_time": 8,
      "local_ip": false,
      "localhost": false,
      "peer_id": "c959fbfbed9e44fb",
      "port": "62950",
      "recv_count": 259,
      "recv_idle_time": 8,
      "send_count": 24342,
      "send_idle_time": 8,
      "state": "state_normal",
      "support_flags": 0
    },{
    ...
    }],
    "status": "OK"
  }
}
```
Retrieve information about incoming and outgoing connections to your node.  
Alias: None.  

|             | Parameter          | Type         | Description
| ---         | ---                | ---          | ---
|**Inputs:**  | *None*.            |              |
|**Outputs:** | connections        |              | List of all connections and their info:
|             | ..address          | string       | The peer's address, actually IPv4 & port
|             | ..avg_download     | unsigned int | Average bytes of data downloaded by node.
|             | ..avg_upload       | unsigned int | Average bytes of data uploaded by node.
|             | ..connection_id    | string       | The connection ID
|             | ..current_download | unsigned int | Current bytes downloaded by node.
|             | ..current_upload   | unsigned int | Current bytes uploaded by node.
|             | ..height           | unsigned int | The peer height
|             | ..host             | string       | The peer host
|             | ..incoming         | boolean      | Is the node getting information from your node?
|             | ..ip               | string       | The node's IP address.
|             | ..live_time        | unsigned int |
|             | ..local_ip         | boolean      |
|             | ..localhost        | boolean      |
|             | ..peer_id          | string       | The node's ID on the network.
|             | ..port             | string       | The port that the node is using to connect to the network.
|             | ..recv_count       | unsigned int |
|             | ..recv_idle_time   | unsigned int |
|             | ..send_count       | unsigned int |
|             | ..send_idle_time   | unsigned int |
|             | ..state            | string       |
|             | ..support_flags    | unsigned int |

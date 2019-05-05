---
weight: 205
---

## **sync_info**


```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sync_info"}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "sync_info",
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  rpc_connection.sync_info()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "height": 1563543,
    "peers": [{
      "info": {
        "address": "70.109.53.128:60064",
        "avg_download": 0,
        "avg_upload": 5,
        "connection_id": "204067223b9b3415c265dd25ad29ee48",
        "current_download": 0,
        "current_upload": 1,
        "height": 1559975,
        "host": "70.109.53.128",
        "incoming": true,
        "ip": "70.109.53.128",
        "live_time": 38,
        "local_ip": false,
        "localhost": false,
        "peer_id": "96b8545dbc7a8866",
        "port": "60064",
        "recv_count": 1580,
        "recv_idle_time": 28,
        "send_count": 203603,
        "send_idle_time": 8,
        "state": "state_normal",
        "support_flags": 1
      }
    },{
      "info": {
        ...
      }
    },{
      ...
    },{
      ...
    },{
      ...
    }],
    "status": "OK",
    "target_height": 1564067
  }
}
```
Get synchronisation informations  
Alias: None.  

|             | Parameter            | Type         | Description
| ---         | ---                  | ---          | ---
|**Inputs:**  | *None*.              |              |
|**Outputs:** | height               | unsigned int |
|             | peers                |              | array of peer structure, defined as follows:
|             | ..info               |              | structure of connection info, as defined in [get_connections](#get-connections)
|             | spans                |              | array of span structure, defined as follows (optional, absent if node is fully synced):
|             | ..connection_id      | string       | Id of connection
|             | ..nblocks            | unsigned int | number of blocks in that span
|             | ..rate               | unsigned int | connection rate
|             | ..remote_address     | string       | peer address the node is downloading (or has downloaded) than span from
|             | ..size               | unsigned int |  total number of bytes in that span's blocks (including txes)
|             | ..speed              | unsigned int |  connection speed
|             | ..start_block_height | unsigned int |  block height of the first block in that span
|             | status               | string       |  General RPC error code. "OK" means everything looks good.
|             | target_height        | unsigned int |  target height the node is syncing from (optional, absent if node is fully synced)

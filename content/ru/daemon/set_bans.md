---
weight: 205
---

## **set_bans**

> banning by host
> In the following example, host is banned with its IP address string-formatted as A.B.C.D:  

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"set_bans","params":{"bans":[{"host":"192.168.1.51","ban":true,"seconds":30}]}}' -H  'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "set_bans",
      "params": {"bans": [{"host": "192.168.1.51", "ban": True, "seconds": 30}]},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"bans": [{"host": "192.168.1.51", "ban": True, "seconds": 30}]}
  rpc_connection.set_bans(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "status": "OK"
  }
}
```

> banning by ip
> In the following example, integer-formatted IP is banned:  

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"set_bans","params":{"bans":[{"ip":838969536,"ban":true,"seconds":30}]}}' -H  'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "status": "OK"
  }
}
```

Ban another node by IP.  
Alias: None.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *bans*    |              | A list of nodes to ban:
|             | *host*    | string       | Host to ban (IP in A.B.C.D form - will support I2P address in the future).
|             | *ip*      | unsigned int | IP address to ban, in Int format.
|             | *ban*     | boolean      |  Set `true` to ban.
|             | *seconds* | unsigned int |  Number of seconds to ban node.
|**Outputs:** | status    | string       | General RPC error code. "OK" means everything looks good.

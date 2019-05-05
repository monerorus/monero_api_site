---
weight: 205
---

## **get_bans**

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_bans"}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_bans",
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  rpc_connection.get_bans()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "bans": [{
      "host": "102.168.1.51",
      "ip": 855746662,
      "seconds": 22
    },{
      "host": "192.168.1.50",
      "ip": 838969536,
      "seconds": 28
    }],
    "status": "OK"
  }
}
```
Get list of banned IPs.  
Alias: None.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *None*.   |              |
|**Outputs:** | bans      |              | List of banned nodes:
|             | ..host    | string       | Banned host (IP in A.B.C.D form).
|             | ..ip      | unsigned int | Banned IP address, in Int format.
|             | ..seconds | unsigned int | Local Unix time that IP is banned until.
|             | status    | string       | General RPC error code. "OK" means everything looks good.

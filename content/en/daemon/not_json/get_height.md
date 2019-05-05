---
weight: 305
---

## **/get_height**

```shell
$ curl -X POST http://127.0.0.1:18081/get_height -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  url = "http://127.0.0.1:18081/get_height"
  #...^ see introduction
```
```json
{
  "height": 1564055,
  "status": "OK",
  "untrusted": false
}
```
Get the node's current height.  
Alias: **/getheight**.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *None*.   |              |
|**Outputs:** | height    | unsigned int | Current length of longest chain known to daemon.
|             | status    | string       | General RPC error code. "OK" means everything looks good.
|             | untrusted | boolean      | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).
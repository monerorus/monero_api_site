---
weight: 305
---

## **/out_peers**

```shell
$ curl -X POST http://127.0.0.1:18081/out_peers -d '{"out_peers": 3232235535}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  url = "http://127.0.0.1:18081/out_peers"
  data = {"out_peers": 3232235535}
  #...^ see introduction
```
```json
{
  "status": "OK"
}
```
Limit number of Outgoing peers.  
Alias: None.  

|             | Parameter   | Type         | Description
| ---         | ---         | ---          | ---
|**Inputs:**  | *out_peers* | unsigned int | Max number of outgoing peers
|**Outputs:** | status      | string       | General RPC error code. "OK" means everything looks good.
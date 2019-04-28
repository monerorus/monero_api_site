---
weight: 305
---

## **/in_peers**

```shell
$ curl -X POST http://127.0.0.1:18081/out_peers -d '{"in_peers": 3232235535}' -H 'Content-Type: application/json'
```
```json
{
  "status": "OK"
}
```
Limit number of Incoming peers.  
Alias: None.  

|             | Parameter  | Type         | Description
| ---         | ---        | ---          | ---
|**Inputs:**  | *in_peers* | unsigned int | Max number of incoming peers
|**Outputs:** | status     | string       | General RPC error code. "OK" means everything looks good.
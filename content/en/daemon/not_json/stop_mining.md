---
weight: 305
---

## **/stop_mining**

```shell
$ curl -X POST http://127.0.0.1:18081/stop_mining -H 'Content-Type: application/json'
```
```json
{
  "status": "OK"
}
```
Stop mining on the daemon.  
Alias: *None*.  

|             | Parameter | Type    | Description
| ---         | ---       | ---     | ---
|**Inputs:**  | *None*.   |         |
|**Outputs:** | status    | string  | General RPC error code. "OK" means everything looks good. Any other value means that something went wrong.
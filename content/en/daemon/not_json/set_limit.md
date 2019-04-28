---
weight: 305
---

## **/set_limit**

```shell
$ curl -X POST http://127.0.0.1:18081/set_limit -d '{"limit_down": 1024}' -H 'Content-Type: application/json'
```
```json
{
  "limit_down": 1024,
  "limit_up": 128,
  "status": "OK"
}
```
Set daemon bandwidth limits.  
Alias: None.  

|             | Parameter    | Type         | Description
| ---         | ---          | ---          | ---
|**Inputs:**  | *limit_down* | signed int   | Download limit in kBytes per second (-1 reset to default, 0 don't change the current limit)
|             | *limit_up*   | signed int   | Upload limit in kBytes per second (-1 reset to default, 0 don't change the current limit)
|**Outputs:** | limit_down   | unsigned int | Download limit in kBytes per second
|             | limit_up     | unsigned int | Upload limit in kBytes per second
|             | status       | string       | General RPC error code. "OK" means everything looks good.
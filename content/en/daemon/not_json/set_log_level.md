## **/set_log_level**


```shell
$ curl -X POST http://127.0.0.1:18081/set_log_level -d '{"level":1}' -H 'Content-Type: application/json'
```
```json
{
  "status": "OK"
}
```
Set the daemon log level.
By default, log level is set to `0`.  
Alias: None.  

|             | Parameter | Type    | Description
| ---         | ---       | ---     | ---
|**Inputs:**  | *level*   | integer | daemon log level to set from `0` (less verbose) to `4` (most verbose)
|**Outputs:** | status    | string  | General RPC error code. "OK" means everything looks good. Any other value means that something went wrong.


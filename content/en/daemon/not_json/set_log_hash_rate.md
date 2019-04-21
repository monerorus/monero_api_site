## **/set_log_hash_rate**


> Mining

```shel
$ curl -X POST http://127.0.0.1:18081/set_log_hash_rate -d '{"visible":true}' -H 'Content-Type: application/json'
```
```json
{
  "status": "OK"
}
```

> Not mining

```shell
$ curl -X POST http://127.0.0.1:18081/set_log_hash_rate -d '{"visible":true}' -H 'Content-Type: application/json'
```
```json
{
  "status": "NOT MINING"
}
```

Set the log hash rate display mode.  
Alias: None.  

|             | Parameter | Type    | Description
| ---         | ---       | ---     | ---
|**Inputs:**  | *visible* | boolean | States if hash rate logs should be visible (`true`) or hidden (`false`)
|**Outputs:** | status    | string  | General RPC error code. "OK" means everything looks good. Any other value means that something went wrong.

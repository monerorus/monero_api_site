---
weight: 305
---

## **/update**

```shell
$ curl -X POST http://127.0.0.1:18081/update -d '{"command":"check"}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  url = "http://127.0.0.1:18081/update"
  data = {"command": "check"}
  ...^ see introduction
```
```json
{
  "auto_uri": "",
  "hash": "",
  "path": "",
  "status": "OK",
  "update": false,
  "user_uri": "",
  "version": ""
}
```
Update daemon.  
Alias: None.  

|             | Parameter | Type    | Description
| ---         | ---       | ---     | ---
|**Inputs:**  | *command* | string  | command to use, either `check` or `download`
|             | *path*    | string  | Optional, path where to download the update.
|**Outputs:** | auto_uri  | string  |
|             | hash      | string  |
|             | path      | String  | path to download the update
|             | status    | string  | General RPC error code. "OK" means everything looks good.
|             | update    | boolean | States if an update is available to download (`true`) or not (`false`)
|             | user_uri  | string  |
|             | version   | string  | Version available for download.
---
weight: 305
---

## **/mining_status**

> Mining

```shell
$ curl -X POST http://127.0.0.1:18081/mining_status -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  url = "http://127.0.0.1:18081/mining_status"
  ...^ see introduction
```
```json
{
  "active": true,
  "address": "47xu3gQpF569au9C2ajo5SSMrWji6xnoE5vhr94EzFRaKAGw6hEGFXYAwVADKuRpzsjiU1PtmaVgcjUJF89ghGPhUXkndHc",
  "is_background_mining_enabled": false,
  "speed": 20,
  "status": "OK",
  "threads_count": 1
}
```

> Not Mining

```
$ curl -X POST http://127.0.0.1:18081/mining_status -H 'Content-Type: application/json'
```
```json
{
  "active": false,
  "address": "",
  "is_background_mining_enabled": false,
  "speed": 0,
  "status": "OK",
  "threads_count": 0
}
```

Get the mining status of the daemon.  
Alias: None.  

|             | Parameter                    | Type         | Description
| ---         | ---                          | ---          | ---
|**Inputs:**  | *None*.                      |              |
|**Outputs:** | active                       | boolean      | States if mining is enabled (`true`) or disabled (`false`).
|             | address                      | string       | Account address daemon is mining to. Empty if not mining.
|             | is_background_mining_enabled | boolean      | States if the mining is running in background (`true`) or foreground (`false`).
|             | speed                        | unsigned int | Mining power in hashes per seconds.
|             | status                       | string       | General RPC error code. "OK" means everything looks good. Any other value means that something went wrong.
|             | threads_count                | unsigned int | Number of running mining threads.
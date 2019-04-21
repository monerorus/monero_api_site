## **/stop_daemon**


```shell
$ curl -X POST http://127.0.0.1:18081/stop_daemon -H 'Content-Type: application/json'
```
```json
{
  "status": "OK"
}
```
Send a command to the daemon to safely disconnect and shut down.  
Alias: None.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *None*.   |        |
|**Outputs:** | status    | string | General RPC error code. "OK" means everything looks good.


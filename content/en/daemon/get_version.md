## **get_version**


```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_version"}' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "status": "OK",
    "untrusted": false,
    "version": 65555
  }
}
```
Give the node current version  
Alias: None.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *None*.   |              |
|**Outputs:** | status    | string       | General RPC error code. "OK" means everything looks good.
|             | untrusted | boolean      | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).
|             | version   | unsigned int |

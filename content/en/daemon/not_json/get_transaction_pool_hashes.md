## **/get_transaction_pool_hashes.bin**


```shell
$ curl -X POST http://127.0.0.1:18081/get_transaction_pool_hashes.bin -H 'Content-Type: application/json'
```
```json
{
  "status": "OK",
  "tx_hashes": " ... ",
  "untrusted": false
}
```
Get hashes from transaction pool. Binary request.  
Alias: None.  


|             | Parameter | Type    | Description
| ---         | ---       | ---     | ---
|**Inputs:**  |*None*.    |         |
|**Outputs:** | status    | string  | General RPC error code. "OK" means everything looks good.
|             | tx_hashes |         | binary array of transaction hashes.
|             | untrusted | boolean | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).

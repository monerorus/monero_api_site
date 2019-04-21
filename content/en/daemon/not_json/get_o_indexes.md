## **/get_o_indexes.bin**

Get global outputs of transactions. Binary request.  
Alias: *None*.  

|             | Parameter | Type                  | Description
| ---         | ---       | ---                   | ---
|**Inputs:**  | *txid*    | binary txid           |
|**Outputs:** | o_indexes | array of unsigned int | List of output indexes
|             | status    | string                | General RPC error code. "OK" means everything looks good.
|             | untrusted | boolean               | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).

<!-- Cannot get this working
```shell
$ curl -X POST http://127.0.0.1:18081/get_o_indexes.bin --data-binary '{"txid":"d6e48158472848e6687173a91ae6eebfa3e1d778e65252ee99d7515d63090408"}'
```
--->

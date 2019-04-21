## **/get_outs.bin**

Get outputs. Binary request.  
Alias: None.  

|             | Parameter  | Type         | Description
| ---         | ---        | ---          | ---
|**Inputs:**  | outputs    |              | array of structure *get_outputs_out* as follows:
|             | ..amount   | unsigned int |     
|             | ..index    | unsigned int |
|**Outputs:** | outs       |              | array of structure *outkey* as follows:
|             | ..amount   | unsigned int |
|             | ..height   | unsigned int | block height of the output
|             | ..key      |              | the public key of the output
|             | ..mask     |              |
|             | ..txid     |              | transaction id
|             | ..unlocked | boolean      | States if output is locked (`false`) or not (`true`)
|             | status     | string       | General RPC error code. "OK" means everything looks good.
|             | untrusted  | boolean      | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).

<!-- Cannot get this working
```shell
$ curl -X POST http://127.0.0.1:18081/get_o_indexes.bin --data-binary '{"txid":"d6e48158472848e6687173a91ae6eebfa3e1d778e65252ee99d7515d63090408"}'
```
--->

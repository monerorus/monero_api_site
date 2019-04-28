---
weight: 205
---

## **on_get_block_hash**


```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"on_get_block_hash","params":[912345]}' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": "e22cf75f39ae720e8b71b3d120a5ac03f0db50bba6379e2850975b4859190bc6"
}
```
Look up a block's hash by its height.  
Alias: **on_getblockhash**.  

|             | Parameter | Type                  | Description
| ---         | ---       | ----                  | ---
|**Inputs:**  |           | int array of length 1 | block height 
|**Outputs:** |           | string                | block hash 

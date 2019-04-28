---
weight: 205
---

## **flush_txpool**

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"flush_txpool","params":{"txids":["dc16fa8eaffe1484ca9014ea050e13131d3acf23b419f33bb4cc0b32b6c49308",""]}}' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "status": "OK"
  }
}
```
Flush tx ids from transaction pool  
Alias: None.  

|             | Parameter | Type             | Description
| ---         | ---       | ---              | ---
|**Inputs:**  | *txids*   | array of strings | Optional, list of transactions IDs to flush from pool (all tx ids flushed if empty).
|**Outputs:** | status    | string           | General RPC error code. "OK" means everything looks good.


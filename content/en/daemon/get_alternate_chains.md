---
weight: 205
---

## **get_alternate_chains**

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_alternate_chains"}' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "chains": [{
      "block_hash": "697cf03c89a9b118f7bdf11b1b3a6a028d7b3617d2d0ed91322c5709acf75625",
      "difficulty": 14114729638300280,
      "height": 1562062,
      "length": 2
    }],
    "status": "OK"
  }
}
```
Display alternative chains seen by the node.  
Alias: None.  

|             | Parameter    | Type         | Description
| ---         | ---          | ---          | ---
|**Inputs:**  | *None*.      |              |
|**Outputs:** | chains       |              | array of chains, the following structure:
|             | ..block_hash | string       | the block hash of the first diverging block of this alternative chain.
|             | ..difficulty | unsigned int | the cumulative difficulty of all blocks in the alternative chain.
|             | ..height     | unsigned int | the block height of the first diverging block of this alternative chain.
|             | ..length     | unsigned int | the length in blocks of this alternative chain, after divergence.
|             | status       | string       | General RPC error code. "OK" means everything looks good.

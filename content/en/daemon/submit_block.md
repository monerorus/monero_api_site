---
weight: 205
---

## **submit_block**

> In this example, a block blob which has not been mined is submitted:

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"submit_block","params":["0707e6bdfedc053771512f1bc27c62731ae9e8f2443db64ce742f4e57f5cf8d393de28551e441a0000000002fb830a01ffbf830a018cfe88bee283060274c0aae2ef5730e680308d9c00b6da59187ad0352efe3c71d36eeeb28782f29f2501bd56b952c3ddc3e350c2631d3a5086cac172c56893831228b17de296ff4669de020200000000"]' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "error": {
    "code": -7,
    "message": "Block not accepted"
  }
}
```
Submit a mined block to the network.  
Alias: **submitblock**.  

|             | Parameter | Type                               | Description
| ---         | ---       | ---                                | ---
|**Inputs:**  |           | Block blob data - array of strings | list of block blobs which have been mined.  See [get_block_template](#get-block-template) to get a blob on which to mine.
|**Outputs:** | status    | string                             | Block submit status.

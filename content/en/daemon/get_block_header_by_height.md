---
weight: 205
---

## **get_block_header_by_height**

> In this example, block 912345 is looked up by its height (notice that the returned information is the same as in the previous example):

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_block_header_by_height","params":{"height":912345}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_block_header_by_height",
      "params": {"height": 912345},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"height": 912345}
  rpc_connection.get_block_header_by_height(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "block_header": {
      "block_size": 210,
      "depth": 649721,
      "difficulty": 815625611,
      "hash": "e22cf75f39ae720e8b71b3d120a5ac03f0db50bba6379e2850975b4859190bc6",
      "height": 912345,
      "major_version": 1,
      "minor_version": 2,
      "nonce": 1646,
      "num_txes": 0,
      "orphan_status": false,
      "prev_hash": "b61c58b2e0be53fad5ef9d9731a55e8a81d972b8d90ed07c04fd37ca6403ff78",
      "reward": 7388968946286,
      "timestamp": 1452793716
    },
    "status": "OK",
    "untrusted": false
  }
}
```
Similar to [get_block_header_by_hash](#get-block-header-by-hash) above, this method includes a block's height as an input parameter to retrieve basic information about the block.  
Alias: **getblockheaderbyheight**.  

|             | Parameter      | Type         | Description
| ---         | ---            | ---          | ---
|**Inputs:**  | *height*       | unsigned int | The block's height.
|**Outputs:** | block_header   |              | A structure containing block header information. See [get_last_block_header](#get-last-block-header).
|             | status         | string       | General RPC error code. "OK" means everything looks good.
|             | untrusted      | boolean      | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).

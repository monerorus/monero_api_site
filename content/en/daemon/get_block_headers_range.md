---
weight: 205
---

## **get_block_headers_range**

> In this example, blocks range from height 1545999 to 1546000 is looked up (notice that the returned informations are ascending order and that it is at the April 2018 network upgrade time):

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_block_headers_range","params":{"start_height":1545999,"end_height":1546000}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_block_headers_range",
      "params": {"start_height": 1545999, "end_height": 1546000},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"start_height": 1545999, "end_height": 1546000}
  rpc_connection.get_block_headers_range(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "headers": [{
      "block_size": 301413,
      "depth": 16085,
      "difficulty": 134636057921,
      "hash": "86d1d20a40cefcf3dd410ff6967e0491613b77bf73ea8f1bf2e335cf9cf7d57a",
      "height": 1545999,
      "major_version": 6,
      "minor_version": 6,
      "nonce": 3246403956,
      "num_txes": 20,
      "orphan_status": false,
      "prev_hash": "0ef6e948f77b8f8806621003f5de24b1bcbea150bc0e376835aea099674a5db5",
      "reward": 5025593029981,
      "timestamp": 1523002893
    },{
      "block_size": 13322,
      "depth": 16084,
      "difficulty": 134716086238,
      "hash": "b408bf4cfcd7de13e7e370c84b8314c85b24f0ba4093ca1d6eeb30b35e34e91a",
      "height": 1546000,
      "major_version": 7,
      "minor_version": 7,
      "nonce": 3737164176,
      "num_txes": 1,
      "orphan_status": false,
      "prev_hash": "86d1d20a40cefcf3dd410ff6967e0491613b77bf73ea8f1bf2e335cf9cf7d57a",
      "reward": 4851952181070,
      "timestamp": 1523002931
    }],
    "status": "OK",
    "untrusted": false
  }
}
```
Similar to [get_block_header_by_height](#get-block-header-by-height) above, but for a range of blocks. This method includes a starting block height and an ending block height as parameters to retrieve basic information about the range of blocks.  
Alias: **getblockheadersrange**  

|             | Parameter      | Type         | Description
| ---         | ---            | ---          | ---
|**Inputs:**  | *start_height* | unsigned int | The starting block's height.
|             | *end_height*   | unsigned int | The ending block's height.
|**Outputs:** | headers        |              | array of `block_header` (a structure containing block header information. See [get_last_block_header](#get-last-block-header)).
|             | status         | string       | General RPC error code. "OK" means everything looks good.
|             | untrusted      | boolean      | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).

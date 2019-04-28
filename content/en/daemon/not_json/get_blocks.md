---
weight: 305
---

## **/get_blocks.bin**

Get all blocks info. Binary request.  
Alias: **/getblocks.bin**.  

|             | Parameter      | Type                   | Description
| ---         | ---            | ---                    | ---
|**Inputs:**  | *block_ids*    | binary array of hashes | first 10 blocks id goes sequential, next goes in pow(2,n) offset, like 2, 4, 8, 16, 32, 64 and so on, and the last one is always genesis block
|             | *start_height* | unsigned int           |
|             | *prune*        | boolean                |
|**Outputs:** | blocks         |                        | array of block complete entries
|             | current_height | unsigned int           |
|             | output_indices |                        | structure as follows:
|             | ..indices      |                        | array of tx output indices, structure as follows:
|             | ....indices    | array of unsigned int  |
|             | start_height   | unsigned int           |
|             | status         | string                 | General RPC error code. "OK" means everything looks good.
|             | untrusted      | boolean                | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).

<!-- Cannot get this working
```shell
$ curl -X POST http://127.0.0.1:18081/get_blocks.bin -d '{"block_ids":["d109a406528a7b44fef8bc03e75eaabb0f919f852884b43b550b8b3be80a49e7"],"start_height":1562062}' -H 'Content-Type: application/json'
```
--->
---
weight: 305
---

## **/get_blocks_by_height.bin**

Get blocks by height. Binary request.

Alias: **/getblocks_by_height.bin**.

|             | Parameter | Type                  | Description
| ---         | ---       | ---                   | ---
|**Inputs:**  | *heights* | array of unsigned int | list of block heights
|**Outputs:** | blocks    |                       | array of block complete entries
|             | status    | string                | General RPC error code. "OK" means everything looks good.
|             | untrusted | boolean               | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).

<!-- Cannot get this working
```shell
$ echo -e '\x7B\x22\x68\x65\x69\x67\x68\x74\x73\x22\x3A\x5B\x31\x35\x36\x34\x32\x34\x36\x5D\x7D\x' | curl -X POST --data-binary @- http://127.0.0.1:18081/get_blocks_by_height.bin
$ echo -e '1564246' | curl -X POST --data-binary @- http://127.0.0.1:18081/get_blocks_by_height.bin
curl -X POST http://127.0.0.1:18081/get_blocks_by_height.bin --data-binary '{"heights":[1564246]}'
```
--->
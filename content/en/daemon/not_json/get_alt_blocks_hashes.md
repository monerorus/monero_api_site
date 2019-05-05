---
weight: 305
---

## **/get_alt_blocks_hashes**


```shell
$ curl -X POST http://127.0.0.1:18081/get_alt_blocks_hashes -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  url = "http://127.0.0.1:18081/get_alt_blocks_hashes"
  #...^ see introduction
```
```json
{
  "blks_hashes": ["9c2277c5470234be8b32382cdf8094a103aba4fcd5e875a6fc159dc2ec00e011","637c0e0f0558e284493f38a5fcca3615db59458d90d3a5eff0a18ff59b83f46f","6f3adc174a2e8082819ebb965c96a095e3e8b63929ad9be2d705ad9c086a6b1c","697cf03c89a9b118f7bdf11b1b3a6a028d7b3617d2d0ed91322c5709acf75625","d99b3cf3ac6f17157ac7526782a3c3b9537f89d07e069f9ce7821d74bd9cad0e","e97b62109a6303233dcd697fa8545c9fcbc0bf8ed2268fede57ddfc36d8c939c","70ff822066a53ad64b04885c89bbe5ce3e537cdc1f7fa0dc55317986f01d1788","b0d36b209bd0d4442b55ea2f66b5c633f522401f921f5a85ea6f113fd2988866"],
  "status": "OK",
  "untrusted": false
}
```
Get the known blocks hashes which are not on the main chain.  
Alias: None.  


|             | Parameter   | Type             | Description
| ---         | ---         | ---              | ---
|**Inputs:**  | *None*      |                  |
|**Outputs:** | blks_hashes | array of strings | list of alternative blocks hashes to main chain
|             | status      | string           | General RPC error code. "OK" means everything looks good.
|             | untrusted   | boolean          | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).


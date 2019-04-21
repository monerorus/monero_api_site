## **get_version**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_version"}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_version",
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  rpc_connection.get_version()
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "version": 65539
    }
  }
```
Get RPC version Major & Minor integer-format, where Major is the first 16 bits and Minor the last 16 bits.  
Alias: *None*.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *None*.   |              |
|**Outputs:** | version   | unsigned int | RPC version, formatted with `Major  2^16 + Minor` (Major encoded over the first 16 bits, and Minor over the last 16 bits).
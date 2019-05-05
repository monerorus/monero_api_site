---
weight: 805
---

## **sign**     

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sign","params":{"data":"This is sample data to be signed"}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "sign",
      "params": {"data": "This is sample data to be signed"},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"data": "This is sample data to be signed"}
  rpc_connection.sign(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "signature": "SigV14K6G151gycjiGxjQ74tKX6A2LwwghvuHjcDeuRFQio5LS6Gb27BNxjYQY1dPuUvXkEbGQUkiHSVLPj4nJAHRrrw3"
    }
  }
```
Sign a string.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *data*    | string | Anything you need to sign.
|**Outputs:** | signature | string | Signature generated against the "data" and the account public address.
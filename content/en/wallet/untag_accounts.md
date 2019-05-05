---
weight: 805
---

## **untag_accounts**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"untag_accounts","params":{"accounts":[1]}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "untag_accounts",
      "params": {"accounts":[1]},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"accounts":[1]}
  rpc_connection.untag_accounts(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Remove filtering tag from a list of accounts.  
Alias: *None*.  

|             | Parameter  | Type                  | Description
| ---         | ---        | ---                   | ---
|**Inputs:**  | *accounts* | array of unsigned int | Remove tag from this list of accounts.
|**Outputs:** | *None*.    |                       |
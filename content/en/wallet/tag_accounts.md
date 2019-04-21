## **tag_accounts**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"tag_accounts","params":{"tag":"myTag","accounts":[0,1]}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "tag_accounts",
      "params": {"tag": "myTag", "accounts": [0, 1]},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"tag": "myTag", "accounts": [0, 1]}
  rpc_connection.tag_accounts(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Apply a filtering tag to a list of accounts.  
Alias: *None*.  

|             | Parameter  | Type                  | Description
| ---         | ---        | ---                   | ---
|**Inputs:**  | *tag*      | string                | Tag for the accounts.
|             | *accounts* | array of unsigned int | Tag this list of accounts.
|**Outputs:** | *None*.    |                       |

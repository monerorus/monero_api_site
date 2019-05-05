---
weight: 805
---

## **create_account**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"create_account","params":{"label":"Secondary account"}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "create_account",
      "params": {"label": "Secondary account"},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"label": "Secondary account"}
  rpc_connection.create_account(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "account_index": 1,
      "address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp"
    }
  }
```
Create a new account with an optional label.  
Alias: *None*.  

|             | Parameter     | Type         | Description
| ---         | ---           | ---          | ---
|**Inputs:**  | *label*       | string       | (Optional) Label for the account.
|**Outputs:** | account_index | unsigned int | Index of the new account.
|             | address       | string       | Address for this account. Base58 representation of the public keys.
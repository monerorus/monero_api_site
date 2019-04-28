---
weight: 805
---

## **label_account**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"label_account","params":{"account_index":0,"label":"Primary account"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "label_account",
      "params": {"account_index": 0, "label": "Primary account"},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"account_index": 0, "label": "Primary account"}
  rpc_connection.label_account(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "account_tags": [{
        "accounts": [0,1],
        "label": "",
        "tag": "myTag"
      }]
    }
  }
```
Label an account.  
Alias: *None*.  

|             | Parameter       | Type         | Description
| ---         | ---             | ---          | ---
|**Inputs:**  | *account_index* | unsigned int | Apply label to account at this index.
|             | *label*         | string       | Label for the account.
|**Outputs:** | *None*.         |              | 
---
weight: 805
---

## **create_address**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"create_address","params":{"account_index":0,"label":"new-sub"}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "create_address",
      "params": {"account_index": 0, "label": "new-sub"},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"account_index": 0, "label": "new-sub"}
  rpc_connection.create_address(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "address": "7BG5jr9QS5sGMdpbBrZEwVLZjSKJGJBsXdZLt8wiXyhhLjy7x2LZxsrAnHTgD8oG46ZtLjUGic2pWc96GFkGNPQQDA3Dt7Q",
      "address_index": 5
    }
  }
```
Create a new address for an account. Optionally, label the new address.  
Alias: *None*.  

|             | Parameter       | Type         | Description
| ---         | ---             | ---          | ---
|**Inputs:**  | *account_index* | unsigned int | Create a new address for this account.
|             | *label*         | string       | (Optional) Label for the new address.
|**Outputs:** | address         | string       | Newly created address. Base58 representation of the public keys.
|             | address_index   | unsigned int | Index of the new address under the input account.
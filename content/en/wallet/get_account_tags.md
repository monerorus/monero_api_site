---
weight: 805
---

## **get_account_tags**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_account_tags","params":""}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_account_tags",
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  rpc_connection.get_account_tags()
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "account_tags": [{
        "accounts": [0],
        "label": "Test tag",
        "tag": "myTag"
      }]
    }
  }
```
Get a list of user-defined account tags.  
Alias: *None*.  

|             | Parameter    | Type         | Description
| ---         | ---          | ---          | ---
|**Inputs:**  | *None*.      |              |  
|**Outputs:** | account_tags |              | array of account tag information:
|             | tag          | string       | Filter tag.
|             | label        | string       | Label for the tag.
|             | accounts     | array of int | List of tagged account indices.
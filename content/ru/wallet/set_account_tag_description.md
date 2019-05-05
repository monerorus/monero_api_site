---
weight: 805
---

## **set_account_tag_description**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"set_account_tag_description","params":{"tag":"myTag","description":"Test tag"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "set_account_tag_description",
      "params": {"tag": "myTag", "description": "Test tag"},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"tag": "myTag", "description": "Test tag"}
  rpc_connection.set_account_tag_description(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Set description for an account tag.  
Alias: *None*.  

|             | Parameter     | Type   | Description
| ---         | ---           | ---    | ---
|**Inputs:**  | *tag*         | string | Set a description for this tag.
|             | *description* | string | Description for the tag.
|**Outputs:** | *None*.       |        |
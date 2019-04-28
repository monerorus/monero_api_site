---
weight: 805
---

## **get_attribute**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_attribute","params":{"key":"my_attribute"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_attribute",
      "params": {"key": "my_attribute"},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"key": "my_attribute"}
  rpc_connection.get_attribute(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "value": "my_value"
    }
  }
```
Get attribute value by name.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *key*     | string | attribute name
|**Outputs:** | value     | string | attribute value
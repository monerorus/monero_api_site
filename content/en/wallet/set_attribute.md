---
weight: 805
---

## **set_attribute**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"set_attribute","params":{"key":"my_attribute","value":"my_value"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "set_attribute",
      "params": {"key": "my_attribute", "value": "my_value"},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"key": "my_attribute", "value": "my_value"}
  rpc_connection.set_attribute(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Set arbitrary attribute.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *key*     | string | attribute name
|             | *value*   | string | attribute value
|**Outputs:** | *None*.   |        |
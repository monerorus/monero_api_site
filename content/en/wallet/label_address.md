---
weight: 805
---

## **label_address**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"label_address","params":{"index":{"major":0,"minor":5},"label":"myLabel"}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "label_address",
      "params": {"index": {"major": 0, "minor": 5}, "label": "myLabel"},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"index": {"major": 0, "minor": 5}, "label": "myLabel"}
  rpc_connection.label_address(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Label an address.  
Alias: *None*.  

|             | Parameter | Type             | Description
| ---         | ---       | ---              | ---
|**Inputs:**  | *index*   | subaddress index | JSON Object containing the major & minor address index:
|             | ..*major* | unsigned int     | Account index for the subaddress.
|             | ..*minor* | unsigned int     | Index of the subaddress in the account.
|             | *label*   | string           | Label for the address.
|**Outputs:** | None.     |                  |
---
weight: 805
---

## **rescan_spent**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"rescan_spent"}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "rescan_spent",
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  rpc_connection.rescan_spent()
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {}
  }
```
Rescan the blockchain for spent outputs.  
Alias: *None*.  

|             | Parameter | Type | Description
| ---         | ---       | ---  | ---
|**Inputs:**  | *None*.   |      |
|**Outputs:** | *None*.   |      |
---
weight: 805
---

## **stop_mining**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"stop_mining"}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "stop_mining",
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  rpc_connection.stop_mining()
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Stop mining in the Monero daemon.  
Alias: *None*.  

|             | Parameter | Type | Description
| ---         | ---       | ---  | ---
|**Inputs:**  | *None*.   |      |
|**Outputs:** | *None*.   |      |
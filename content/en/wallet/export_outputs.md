---
weight: 805
---

## **export_outputs**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"export_outputs"}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "export_outputs",
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  rpc_connection.export_outputs()
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "outputs_data_hex": "#...^ see introductionoutputs#...^ see introduction"
    }
  }
```
Export all outputs in hex format.  
Alias: *None*.  

|             | Parameter        | Type   | Description
| ---         | ---              | ---    | ---
|**Inputs:**  | *None*.          |        |
|**Outputs:** | outputs_data_hex | string | wallet outputs in hex format.
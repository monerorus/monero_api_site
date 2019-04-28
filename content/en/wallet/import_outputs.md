---
weight: 805
---

## **import_outputs**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"import_outputs","params":{"outputs_data_hex":"...^ see introductionoutputs...^ see introduction"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "import_outputs",
      "params": {"outputs_data_hex": "...^ see introductionoutputs...^ see introduction"},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"outputs_data_hex": "...^ see introductionoutputs...^ see introduction"}
  rpc_connection.import_outputs(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "num_imported": 6400
    }
  }
```
Import outputs in hex format.  
Alias: *None*.  

|             | Parameter          | Type         | Description
| ---         | ---                | ---          | ---
|**Inputs:**  | *outputs_data_hex* | string       | wallet outputs in hex format.
|**Outputs:** | num_imported       | unsigned int | number of outputs imported.
---
weight: 805
---

## **submit_multisig**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"submit_multisig","params":{"tx_data_hex":"#...^ see introductiontx_data_hex#...^ see introduction"}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "submit_multisig",
      "params": {"tx_data_hex": "#...^ see introductiontx_data_hex#...^ see introduction"},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"tx_data_hex": "#...^ see introductiontx_data_hex#...^ see introduction"}
  rpc_connection.submit_multisig(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "tx_hash_list": ["4996091b61c1be112c1097fd5e97d8ff8b28f0e5e62e1137a8c831bacf034f2d"]
    }
  }
```
Submit a signed multisig transaction.  
Alias: *None*.  

|             | Parameter     | Type            | Description
| ---         | ---           | ---             | ---
|**Inputs:**  | *tx_data_hex* | string          | Multisig transaction in hex format, as returned by `sign_multisig` under `tx_data_hex`.
|**Outputs:** | tx_hash_list  | array of string | List of transaction Hash.
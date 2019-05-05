---
weight: 805
---

## **sign_multisig**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sign_multisig","params":{"tx_data_hex":"#...^ see introductionmultisig_txset#...^ see introduction"}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "sign_multisig",
      "params": {"tx_data_hex": "#...^ see introductionmultisig_txset#...^ see introduction"},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"tx_data_hex": "#...^ see introductionmultisig_txset#...^ see introduction"}
  rpc_connection.sign_multisig(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "tx_data_hex": "#...^ see introductionmultisig_txset#...^ see introduction",
      "tx_hash_list": ["4996091b61c1be112c1097fd5e97d8ff8b28f0e5e62e1137a8c831bacf034f2d"]
    }
  }
```
Sign a transaction in multisig.  
Alias: *None*.  

|             | Parameter     | Type            | Description
| ---         | ---           | ---             | ---
|**Inputs:**  | *tx_data_hex* | string          | Multisig transaction in hex format, as returned by `transfer` under `multisig_txset`.
|**Outputs:** | tx_data_hex   | string          | Multisig transaction in hex format.
|             | tx_hash_list  | array of string | List of transaction Hash.
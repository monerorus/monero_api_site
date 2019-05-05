---
weight: 805
---

## **submit_transfer**

> In the example below, we submit the transfer using the signed_txset generated above:

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"submit_transfer","params":{"tx_data_hex":...^ see introductionlong_hex...^ see introduction"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "submit_transfer",
      "params": {"tx_data_hex": "...^ see introductionlong_hex...^ see introduction"},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"tx_data_hex": "...^ see introductionlong_hex...^ see introduction"}
  rpc_connection.submit_transfer(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "tx_hash_list": ["40fad7c828bb383ac02648732f7afce9adc520ba5629e1f5d9c03f584ac53d74"]
    }
  }
```
Submit a previously signed transaction on a read-only wallet (in cold-signing process).  
Alias: *None*.  

|             | Parameter     | Type            | Description
| ---         | ---           | ---             | ---
|**Inputs:**  | *tx_data_hex* | string          | Set of signed tx returned by "sign_transfer"
|**Outputs:** | tx_hash_list  | array of string | The tx hashes of every transaction.
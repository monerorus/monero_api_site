---
weight: 805
---

## **get_tx_key**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_tx_key","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be"}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_tx_key",
      "params": {"txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be"},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be"}
  rpc_connection.get_tx_key(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "tx_key": "feba662cf8fb6d0d0da18fc9b70ab28e01cc76311278fdd7fe7ab16360762b06"
    }
  }
```
Get transaction secret key from transaction id.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *txid*    | string | transaction id.
|**Outputs:** | tx_key    | string | transaction secret key.
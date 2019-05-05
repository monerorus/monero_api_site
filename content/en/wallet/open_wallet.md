---
weight: 805
---

## **open_wallet**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"open_wallet","params":{"filename":"mytestwallet","password":"mytestpassword"}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "open_wallet",
      "params": {"filename": "mytestwallet", "password": "mytestpassword"},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"filename": "mytestwallet", "password": "mytestpassword"}
  rpc_connection.open_wallet(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Open a wallet. You need to have set the argument "--wallet-dir" when launching monero-wallet-rpc to make this work.  
Alias: *None*.  

|             | Parameter  | Type   | Description
| ---         | ---        | ---    | ---
|**Inputs:**  | *filename* | string | wallet name stored in --wallet-dir.
|             | *password* | string | (Optional) only needed if the wallet has a password defined.
|**Outputs:** | *None*.    |        |
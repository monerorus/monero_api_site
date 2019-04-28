---
weight: 805
---

## **create_wallet**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"create_wallet","params":{"filename":"mytestwallet","password":"mytestpassword","language":"English"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "create_wallet",
      "params": {
          "filename": "mytestwallet",
          "password": "mytestpassword",
          "language": "English",
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "filename": "mytestwallet",
      "password": "mytestpassword",
      "language": "English",
  }
  rpc_connection.create_wallet(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Create a new wallet. You need to have set the argument "--wallet-dir" when launching monero-wallet-rpc to make this work.  
Alias: *None*.  

|             | Parameter  | Type   | Description
| ---         | ---        | ---    | ---
|**Inputs:**  | *filename* | string | Wallet file name.
|             | *password* | string | (Optional) password to protect the wallet.
|             | *language* | string | Language for your wallets' seed.
|**Outputs:** | *None*.    |        |
## **change_wallet_password**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"change_wallet_password","params":{"old_password":"theCurrentSecretPassPhrase","new_password":"theNewSecretPassPhrase"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "change_wallet_password",
      "params": {
          "old_password": "theCurrentSecretPassPhrase",
          "new_password": "theNewSecretPassPhrase",
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "old_password": "theCurrentSecretPassPhrase",
      "new_password": "theNewSecretPassPhrase",
  }
  rpc_connection.change_wallet_password(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Change a wallet password.  
Alias: *None*.  

|             | Parameter      | Type   | Description
| ---         | ---            | ---    | ---
|**Inputs:**  | *old_password* | string | (Optional) Current wallet password, if defined.
|             | *new_password* | string | (Optional) New wallet password, if not blank.
|**Outputs:   | *None*.        |        |

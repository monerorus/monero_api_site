## **get_accounts**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_accounts","params":{"tag":"myTag"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_accounts",
      "params": {"tag": "myTag"},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"tag": "myTag"}
  rpc_connection.get_accounts(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "subaddress_accounts": [{
        "account_index": 0,
        "balance": 157663195572433688,
        "base_address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
        "label": "Primary account",
        "tag": "myTag",
        "unlocked_balance": 157443303037455077
      },{
        "account_index": 1,
        "balance": 0,
        "base_address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp",
        "label": "Secondary account",
        "tag": "myTag",
        "unlocked_balance": 0
      }],
      "total_balance": 157663195572433688,
      "total_unlocked_balance": 157443303037455077
    }
  }
```
Get all accounts for a wallet. Optionally filter accounts by tag.  
Alias: *None*.  

|             | Parameter              | Type         | Description
| ---         | ---                    | ---          | ---
|**Inputs:**  | *tag*                  | string       | (Optional) Tag for filtering accounts.
|**Outputs:** | subaddress_accounts    |              |array of subaddress account information:
|             | ..account_index        | unsigned int | Index of the account.
|             | ..balance              | unsigned int | Balance of the account (locked or unlocked).
|             | ..base_address         | string       | Base64 representation of the first subaddress in the account.
|             | ..label                | string       | (Optional) Label of the account.
|             | ..tag                  | string       | (Optional) Tag for filtering accounts.
|             | ..unlocked_balance     | unsigned int | Unlocked balance for the account.
|             | total_balance          | unsigned int | Total balance of the selected accounts (locked or unlocked).
|             | total_unlocked_balance | unsigned int | Total unlocked balance of the selected accounts.

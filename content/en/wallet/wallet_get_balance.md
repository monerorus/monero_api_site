---
weight: 805
---

## **get_balance**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_balance","params":{"account_index":0,"address_indices":[0,1]}}' -H 'Content-Type: application/json'
```

```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_balance",
      "params": {"account_index": 0, "address_indices": [0, 1]},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"account_index": 0, "address_indices": [0, 1]}
  rpc_connection.get_balance(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "balance": 157443303037455077,
      "multisig_import_needed": false,
      "per_subaddress": [{
        "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
        "address_index": 0,
        "balance": 157360317826255077,
        "label": "Primary account",
        "num_unspent_outputs": 5281,
        "unlocked_balance": 157360317826255077
      },{
        "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
        "address_index": 1,
        "balance": 59985211200000,
        "label": "",
        "num_unspent_outputs": 1,
        "unlocked_balance": 59985211200000
      }],
      "unlocked_balance": 157443303037455077
    }
  }
```
Return the wallet's balance.  
Alias: *getbalance*.  

|             | Parameter              | Type                            | Description
| ---         | ---                    | ---                             | ---
|**Inputs:**  | *account_index*        | unsigned int                    | Return balance for this account.
|             | *address_indices*      | array of unsigned int           | (Optional) Return balance detail for those subaddresses.
|**Outputs:** | balance                | unsigned int                    | The total balance of the current monero|wallet|rpc in session.
|             | unlocked_balance       | unsigned int                    | Unlocked funds are those funds that are sufficiently deep enough in the Monero blockchain to be considered safe to spend.
|             | multisig_import_needed | boolean                         | True if importing multisig data is needed for returning a correct balance.
|             | per_subaddress         | array of subaddress information | Balance information for each subaddress in an account.
|             | ..address_index        | unsigned int                    | Index of the subaddress in the account.
|             | ..address              | string                          | Address at this index. Base58 representation of the public keys.
|             | ..balance              | unsigned int                    | Balance for the subaddress (locked or unlocked).
|             | ..unlocked_balance     | unsigned int                    | Unlocked balance for the subaddress.
|             | ..label                | string                          | Label for the subaddress.
|             | ..num_unspent_outputs  | unsigned int                    | Number of unspent outputs available for the subaddress.
---
weight: 810
---

## **get_address**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_address","params":{"account_index":0,"address_index":[0,1,4]}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_address",
      "params": {"account_index": 0, "address_index": [0, 1, 4]},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"account_index": 0, "address_index": [0, 1, 4]}
  rpc_connection.get_address(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "addresses": [{
        "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
        "address_index": 0,
        "label": "Primary account",
        "used": true
      },{
        "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
        "address_index": 1,
        "label": "",
        "used": true
      },{
        "address": "77xa6Dha7kzCQuvmd8iB5VYoMkdenwCNRU9khGhExXQ8KLL3z1N1ZATBD1sFPenyHWT9cm4fVFnCAUApY53peuoZFtwZiw5",
        "address_index": 4,
        "label": "test2",
        "used": true
      }]
    }
  }
```
Return the wallet's addresses for an account. Optionally filter for specific set of subaddresses.  
Alias: *getaddress*.  

|             | Parameter       | Type                  | Description
| ---         | ---             | ---                   | ---
|**Inputs:**  | *account_index* | unsigned int          | Return subaddresses for this account.
|             | *address_index* | array of unsigned int | (Optional) List of subaddresses to return from an account.
|**Outputs:** | address         | string                | The 95|character hex address string of the monero|wallet|rpc in session.
|             | addresses       |                       | array of addresses informations
|             | ..address       | string                | The 95-character hex (sub)address string.
|             | ..label         | string                | Label of the (sub)address
|             | ..address_index | unsigned int          | index of the subaddress
|             | ..used          | boolean               | states if the (sub)address has already received funds

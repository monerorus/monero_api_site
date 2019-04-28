
---
weight: 805
---

## **make_integrated_address**

> Example (Payment ID is empty, use a random ID):

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"make_integrated_address","params":{"standard_address":"55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "make_integrated_address",
      "params": {
          "standard_address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt"
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "standard_address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt"
  }
  rpc_connection.make_integrated_address(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "integrated_address": "5F38Rw9HKeaLQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZXCkbHUXdPHyiUeRyokn",
      "payment_id": "420fa29b2d9a49f5"
    }
  }
```
Make an integrated address from the wallet address and a payment id.  
Alias: *None*.  

|             | Parameter           | Type   | Description
| ---         | ---                 | ---    | ---
|**Inputs:**  | *standard_address*  | string | (Optional, defaults to primary address) Destination public address.
|             | *payment_id*        | string | (Optional, defaults to a random ID) 16 characters hex encoded.
|**Outputs:** | integrated_address* | string |
|             | payment_id*         | string | hex encoded;
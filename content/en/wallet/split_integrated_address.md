## **split_integrated_address**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"split_integrated_address","params":{"integrated_address": "5F38Rw9HKeaLQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZXCkbHUXdPHyiUeRyokn"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "split_integrated_address",
      "params": {
          "integrated_address": "5F38Rw9HKeaLQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZXCkbHUXdPHyiUeRyokn"
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "integrated_address": "5F38Rw9HKeaLQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZXCkbHUXdPHyiUeRyokn"
  }
  rpc_connection.split_integrated_address(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "is_subaddress": false,
      "payment_id": "420fa29b2d9a49f5",
      "standard_address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt"
    }
  }
```
Retrieve the standard address and payment id corresponding to an integrated address.  
Alias: *None*.  

|             | Parameter            | Type    | Description
| ---         | ---                  | ---     | ---
|**Inputs:**  | *integrated_address* | string  |
|**Outputs:** | is_subaddress        | boolean | States if the address is a subaddress
|             | payment              | string  | hex encoded
|             | standard_address     | string  |

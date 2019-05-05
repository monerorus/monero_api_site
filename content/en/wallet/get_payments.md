---
weight: 805
---

## **get_payments**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_payments","params":{"payment_id":"60900e5603bf96e3"}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_payments",
      "params": {"payment_id": "60900e5603bf96e3"},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"payment_id": "60900e5603bf96e3"}
  rpc_connection.get_payments(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "payments": [{
        "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
        "amount": 1000000000000,
        "block_height": 127606,
        "payment_id": "60900e5603bf96e3",
        "subaddr_index": {
          "major": 0,
          "minor": 0
        },
        "tx_hash": "3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f",
        "unlock_time": 0
      }]
    }
  }
```
Get a list of incoming payments using a given payment id.  
Alias: *None*.  

|             | Parameter       | Type         | Description
| ---         | ---             | ---          | ---
|**Inputs:**  | *payment_id*    | string       | Payment ID used to find the payments (16 characters hex).
|**Outputs:** | payments        |              | list of:
|             | ..payment_id    | string       | Payment ID matching the input parameter.
|             | ..tx_hash       | string       | Transaction hash used as the transaction ID.
|             | ..amount        | unsigned int | Amount for this payment.
|             | ..block_height  | unsigned int | Height of the block that first confirmed this payment.
|             | ..unlock_time   | unsigned int | Time (in block height) until this payment is safe to spend.
|             | ..subaddr_index |              | subaddress index:
|             | #...^ see introduction.major       | unsigned int | Account index for the subaddress.
|             | #...^ see introduction.minor       | unsigned int | Index of the subaddress in the account.
|             | ..address       | string       | Address receiving the payment | Base58 representation of the public keys.
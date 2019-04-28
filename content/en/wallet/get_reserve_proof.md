---
weight: 805
---

## **get_reserve_proof**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_reserve_proof","params":{"all":false,"account_index":0,"amount":100000000000}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_reserve_proof",
      "params": {"all": False, "account_index": 0, "amount": 100000000000},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"all": False, "account_index": 0, "amount": 100000000000}
  rpc_connection.get_reserve_proof(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "signature": "ReserveProofV11BZ23sBt9sZJeGccf84mzyAmNCP3KzYbE1111112VKmH111118NfCYJQjZ6c46gT2kXgcHCaSSZeL8sRdzqjqx7i1e7FQfQGu2o113UYFVdwzHQi3iENDPa76Kn1BvywbKz3bMkXdZkBEEhBSF4kjjGaiMJ1ucKb6wvMVC4A8sA4nZEdL2Mk3wBucJCYTZwKqA8i1M113kqakDkG25FrjiDqdQTCYz2wDBmfKxF3eQiV5FWzZ6HmAyxnqTWUiMWukP9A3Edy3ZXqjP1b23dhz7Mbj39bBxe3ZeDNu9HnTSqYvHNRyqCkeUMJpHyQweqjGUJ1DSfFYr33J1E7MkhMnEi1o7trqWjVix32XLetYfePG73yvHbS24837L7Q64i5n1LSpd9yMiQZ3Dyaysi5y6jPx7TpAvnSqBFtuCciKoNzaXoA3dqt9cuVFZTXzdXKqdt3cXcVJMNxY8RvKPVQHhUur94Lpo1nSpxf7BN5a5rHrbZFqoZszsZmiWikYPkLX72XUdw6NWjLrTBxSy7KuPYH86c6udPEXLo2xgN6XHMBMBJzt8FqqK7EcpNUBkuHm2AtpGkf9CABY3oSjDQoRF5n4vNLd3qUaxNsG4XJ12L9gJ7GrK273BxkfEA8fDdxPrb1gpespbgEnCTuZHqj1A"
    }
  }
```
Generate a signature to prove of an available amount in a wallet.  
Alias: *None*.  

|             | Parameter       | Type         | Description
| ---         | ---             | ---          | ---
|**Inputs:**  | *all*           | boolean      | Proves all wallet balance to be disposable.
|             | *account_index* | unsigned int | Specify the account from witch to prove reserve. (ignored if `all` is set to true)
|             | *amount*        | unsigned int | Amount (in @atomic-units) to prove the account has for reserve. (ignored if `all` is set to true)
|             | *message*       | string       | (Optional) add a message to the signature to further authenticate the prooving process.
|**Outputs:** | signature       | string       | reserve signature.
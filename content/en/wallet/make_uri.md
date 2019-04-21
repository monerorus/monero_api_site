## **make_uri**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"make_uri","params":{"address":"55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt","amount":10,"payment_id":"420fa29b2d9a49f5","tx_description":"Testing out the make_uri function.","recipient_name":"el00ruobuob Stagenet wallet"}}'  -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "make_uri",
      "params": {
          "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
          "amount": 10,
          "payment_id": "420fa29b2d9a49f5",
          "tx_description": "Testing out the make_uri function.",
          "recipient_name": "el00ruobuob Stagenet wallet",
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "amount": 10,
      "payment_id": "420fa29b2d9a49f5",
      "tx_description": "Testing out the make_uri function.",
      "recipient_name": "el00ruobuob Stagenet wallet",
  }
  rpc_connection.make_uri(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "uri": "monero:55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt?tx_payment_id=420fa29b2d9a49f5&tx_amount=0.000000000010&recipient_name=el00ruobuob%20Stagenet%20wallet&tx_description=Testing%20out%20the%20make_uri%20function."
    }
  }
```
Create a payment URI using the official URI spec.  
Alias: *None*.  

|             | Parameter        | Type         | Description
| ---         | ---              | ---          | ---
|**Inputs:**  | *address*        | string       | Wallet address
|             | *amount*         | unsigned int | (optional) the integer amount to receive, in **@atomic-units**
|             | *payment_id*     | string       | (optional) 16 or 64 character hexadecimal payment id
|             | *recipient_name* | string       | (optional) name of the payment recipient
|             | *tx_description* | string       | (optional) Description of the reason for the tx
|**Outputs:** | uri              | string       | This contains all the payment input information as a properly formatted payment URI

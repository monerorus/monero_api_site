---
weight: 805
---

## **parse_uri**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"parse_uri","params":{"uri":"monero:55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt?tx_payment_id=420fa29b2d9a49f5&tx_amount=0.000000000010&recipient_name=el00ruobuob%20Stagenet%20wallet&tx_description=Testing%20out%20the%20make_uri%20function."}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "parse_uri",
      "params": {
          "uri": "monero:55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt?tx_payment_id=420fa29b2d9a49f5&tx_amount=0.000000000010&recipient_name=el00ruobuob%20Stagenet%20wallet&tx_description=Testing%20out%20the%20make_uri%20function."
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "uri": "monero:55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt?tx_payment_id=420fa29b2d9a49f5&tx_amount=0.000000000010&recipient_name=el00ruobuob%20Stagenet%20wallet&tx_description=Testing%20out%20the%20make_uri%20function."
  }
  rpc_connection.parse_uri(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "uri": {
        "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
        "amount": 10,
        "payment_id": "420fa29b2d9a49f5",
        "recipient_name": "el00ruobuob Stagenet wallet",
        "tx_description": "Testing out the make_uri function."
      }
    }
  }
```
Parse a payment URI to get payment information.  
Alias: *None*.  

|             | Parameter        | Type         | Description
| ---         | ---              | ---          | ---
|**Inputs:**  | *uri*            | string       | This contains all the payment input information as a properly formatted payment URI
|**Outputs:** | uri              |              | JSON object containing payment information:
|             | ..address        | string       | Wallet address
|             | ..amount         | unsigned int | Integer amount to receive, in @atomic|units (0 if not provided)
|             | ..payment_id     | string       | 16 or 64 character hexadecimal payment id (empty if not provided)
|             | ..recipient_name | string       | Name of the payment recipient (empty if not provided)
|             | ..tx_description | string       | Description of the reason for the tx (empty if not provided)
## **get_transfer_by_txid**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_transfer_by_txid","params":{"txid":"c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_transfer_by_txid",
      "params": {"txid": "c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a"},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"txid": "c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a"}
  rpc_connection.get_transfer_by_txid(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "transfer": {
        "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
        "amount": 300000000000,
        "confirmations": 1,
        "destinations": [{
          "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
          "amount": 100000000000
        },{
          "address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp",
          "amount": 200000000000
        }],
        "double_spend_seen": false,
        "fee": 21650200000,
        "height": 153624,
        "note": "",
        "payment_id": "0000000000000000",
        "subaddr_index": {
          "major": 0,
          "minor": 0
        },
        "suggested_confirmations_threshold": 1,
        "timestamp": 1535918400,
        "txid": "c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a",
        "type": "out",
        "unlock_time": 0
      }
    }
  }
```
Show information about a transfer to/from this address.  
Alias: *None*.  


|             | Parameter                         | Type         | Description
| ---         | ---                               | ---          | ---
|**Inputs:**  | *txid*                            | string       | Transaction ID used to find the transfer.
|             | *account_index*                   | unsigned int | (Optional) Index of the account to query for the transfer.
|**Outputs:** | transfer                          |              | JSON object containing payment information:
|             | address                           | string       | Address that transferred the funds. Base58 representation of the public keys.
|             | amount                            | unsigned int | Amount of this transfer.
|             | confirmations                     | unsigned int | Number of block mined since the block containing this transaction (or block height at which the transaction should be added to a block if not yet confirmed).
|             | destinations                      |              | array of JSON objects containing transfer destinations:
|             | ..amount                          | unsigned int | Amount transferred to this destination.
|             | ..address                         | string       | Address for this destination. Base58 representation of the public keys.
|             | double_spend_seen                 | boolean      | True if the key image(s) for the transfer have been seen before.
|             | fee                               | unsigned int | Transaction fee for this transfer.
|             | height                            | unsigned int | Height of the first block that confirmed this transfer.
|             | note                              | string       | Note about this transfer.
|             | payment_id                        | string       | Payment ID for this transfer.
|             | subaddr_index                     |              | JSON object containing the major & minor subaddress index:
|             | ..major                           | unsigned int | Account index for the subaddress.
|             | ..minor                           | unsigned int | Index of the subaddress under the account.
|             | suggested_confirmations_threshold | unsigned int | Estimation of the confirmations needed for the transaction to be included in a block.
|             | timestamp                         | unsigned int | POSIX timestamp for the block that confirmed this transfer (or timestamp submission if not mined yet).
|             | txid                              | string       | Transaction ID of this transfer (same as input TXID).
|             | type                              | string       | Type of transfer, one of the following: "in", "out", "pending", "failed", "pool"
|             | unlock_time                       | unsigned int | Number of blocks until transfer is safely spendable.

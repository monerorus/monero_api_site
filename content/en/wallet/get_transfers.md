---
weight: 805
---

## **get_transfers**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_transfers","params":{"in":true,"account_index":1}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_transfers",
      "params": {"in": True, "account_index": 1},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"in": True, "account_index": 1}
  rpc_connection.get_transfers(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "in": [{
        "address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp",
        "amount": 200000000000,
        "confirmations": 1,
        "double_spend_seen": false,
        "fee": 21650200000,
        "height": 153624,
        "note": "",
        "payment_id": "0000000000000000",
        "subaddr_index": {
          "major": 1,
          "minor": 0
        },
        "suggested_confirmations_threshold": 1,
        "timestamp": 1535918400,
        "txid": "c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a",
        "type": "in",
        "unlock_time": 0
      }]
    }
  }
```
Returns a list of transfers.  
Alias: *None*.  

|             | Parameter                            | Type                  | Description
| ---         | ---                                  | ---                   | ---
|**Inputs:**  | *in*                                 | boolean               | (Optional) Include incoming transfers.
|             | *out*                                | boolean               | (Optional) Include outgoing transfers.
|             | *pending*                            | boolean               | (Optional) Include pending transfers.
|             | *failed*                             | boolean               | (Optional) Include failed transfers.
|             | *pool*                               | boolean               | (Optional) Include transfers from the daemon's transaction pool.
|             | *filter_by_height*                   | boolean               | (Optional) Filter transfers by block height.
|             | *min_height*                         | unsigned int          | (Optional) Minimum block height to scan for transfers, if filtering by height is enabled.
|             | *max_height*                         | unsigned int          | (Opional) Maximum block height to scan for transfers, if filtering by height is enabled (defaults to max block height).
|             | *account_index*                      | unsigned int          | (Optional) Index of the account to query for transfers. (defaults to 0)
|             | *subaddr_indices*                    | array of unsigned int | (Optional) List of subaddress indices to query for transfers. (defaults to 0)
|**Outputs:** | in                                   |                       | array of transfers:
|             | .. address                           | string                | Public address of the transfer.
|             | .. amount                            | unsigned int          | Amount transferred.
|             | .. confirmations                     | unsigned int          | Number of block mined since the block containing this transaction (or block height at which the transaction should be added to a block if not yet confirmed).
|             | .. double_spend_seen                 | boolean               | True if the key image(s) for the transfer have been seen before.
|             | .. fee                               | unsigned int          | Transaction fee for this transfer.
|             | .. height                            | unsigned int          | Height of the first block that confirmed this transfer (0 if not mined yet).
|             | .. note                              | string                | Note about this transfer.
|             | .. payment_id                        | string                | Payment ID for this transfer.
|             | .. subaddr_index                     |                       | JSON object containing the major & minor subaddress index:
|             | ..  major                            | unsigned int          | Account index for the subaddress.
|             | ..  minor                            | unsigned int          | Index of the subaddress under the account.
|             | .. suggested_confirmations_threshold | unsigned int          | Estimation of the confirmations needed for the transaction to be included in a block.
|             | .. timestamp                         | unsigned int          | POSIX timestamp for when this transfer was first confirmed in a block (or timestamp submission if not mined yet).
|             | .. txid                              | string                | Transaction ID for this transfer.
|             | .. type                              | string                | Transfer type: "in"
|             | .. unlock_time                       | unsigned int          | Number of blocks until transfer is safely spendable.
|             | out                                  |                       | array of transfers (see above).
|             | pending                              |                       | array of transfers (see above).
|             | failed                               |                       | array of transfers (see above).
|             | pool                                 |                       | array of transfers (see above).
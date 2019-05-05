---
weight: 805
---

## **sweep_all**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sweep_all","params":{"address":"55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt","subaddr_indices":[4],"ring_size":7,"unlock_time":0,"get_tx_keys":true}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "sweep_all",
      "params": {
          "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
          "subaddr_indices": [4],
          "ring_size": 7,
          "unlock_time": 0,
          "get_tx_keys": True,
      },
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {
      "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "subaddr_indices": [4],
      "ring_size": 7,
      "unlock_time": 0,
      "get_tx_keys": True,
  }
  rpc_connection.sweep_all(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "amount_list": [9985885770000],
      "fee_list": [14114230000],
      "multisig_txset": "",
      "tx_hash_list": ["ab4b6b65cc8cd8c9dd317d0b90d97582d68d0aa1637b0065b05b61f9a66ea5c5"],
      "tx_key_list": ["b9b4b39d3bb3062ddb85ec0266d4df39058f4c86077d99309f218ce4d76af607"],
      "unsigned_txset": ""
    }
  }
```
Send all unlocked balance to an address.  
Alias: *None*.  

|             | Parameter         | Type                  | Description
| ---         | ---               | ---                   | ---
|**Inputs:**  | *address*         | string                | Destination public address.
|             | *account_index*   | unsigned int          | Sweep transactions from this account.
|             | *subaddr_indices* | array of unsigned int | (Optional) Sweep from this set of subaddresses in the account.
|             | *priority*        | unsigned int          | (Optional) Priority for sending the sweep transfer, partially determines fee.
|             | *mixin*           | unsigned int          | Number of outputs from the blockchain to mix with (0 means no mixing).
|             | *ring_size*       | unsigned int          | Sets ringsize to n (mixin + 1).
|             | *unlock_time*     | unsigned int          | Number of blocks before the monero can be spent (0 to not add a lock).
|             | *payment_id*      | string                | (Optional) Random 32-byte/64-character hex string to identify a transaction.
|             | *get_tx_keys*     | boolean               | (Optional) Return the transaction keys after sending.
|             | *below_amount*    | unsigned int          | (Optional) Include outputs below this amount.
|             | *do_not_relay*    | boolean               | (Optional) If true, do not relay this sweep transfer. (Defaults to false)
|             | *get_tx_hex*      | boolean               | (Optional) return the transactions as hex encoded string. (Defaults to false)
|             | *get_tx_metadata* | boolean               | (Optional) return the transaction metadata as a string. (Defaults to false)
|**Outputs:** | tx_hash_list      | array of string       | The tx hashes of every transaction.
|             | tx_key_list       | array of string       | The transaction keys for every transaction.
|             | amount_list       | array of integer      | The amount transferred for every transaction.
|             | fee_list          | array of integer      | The amount of fees paid for every transaction.
|             | tx_blob_list      | array of string       | The tx as hex string for every transaction.
|             | tx_metadata_list  | array of string       | List of transaction metadata needed to relay the transactions later.
|             | multisig_txset    | string                | The set of signing keys used in a multisig transaction (empty for non|multisig).
|             | unsigned_txset    | string                | Set of unsigned tx for cold-signing purposes.
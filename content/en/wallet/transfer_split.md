---
weight: 805
---

## **transfer_split**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"transfer_split","params":{"destinations":[{"amount":1000000000000,"address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"},{"amount":2000000000000,"address":"75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv"}],"account_index":0,"subaddr_indices":[0],"priority":0,"ring_size":7,"get_tx_key": true}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "transfer_split",
      "params": {
          "destinations": [
              {
                  "amount": 1000000000000,
                  "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
              },
              {
                  "amount": 2000000000000,
                  "address": "75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv",
              },
          ],
          "account_index": 0,
          "subaddr_indices": [0],
          "priority": 0,
          "ring_size": 7,
          "get_tx_key": True,
      },
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {
      "destinations": [
          {
              "amount": 1000000000000,
              "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
          },
          {
              "amount": 2000000000000,
              "address": "75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv",
          },
      ],
      "account_index": 0,
      "subaddr_indices": [0],
      "priority": 0,
      "ring_size": 7,
      "get_tx_key": True,
  }
  rpc_connection.transfer_split(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "amount_list": [3000000000000],
      "fee_list": [85106400000],
      "multisig_txset": "",
      "tx_hash_list": ["c8d815f48f27d53fdaf198a74b292a91bfaf87529a9a9a9ee66079a890b3b58b"],
      "unsigned_txset": ""
    }
  }
```
Same as transfer, but can split into more than one tx if necessary.  
Alias: *None*.  

|             | Parameter         | Type                  | Description
| ---         | ---               | ---                   | ---
|**Inputs:**  | *destinations*    |                       | array of destinations to receive XMR:
|             | ..*amount*        | unsigned int          | Amount to send to each destination, in @atomic|units.
|             | ..*address*       | string                | Destination public address.
|             | *account_index*   | unsigned int          | (Optional) Transfer from this account index. (Defaults to 0)
|             | *subaddr_indices* | array of unsigned int | (Optional) Transfer from this set of subaddresses. (Defaults to 0)
|             | *mixin*           | unsigned int          | Number of outputs from the blockchain to mix with (0 means no mixing).
|             | *ring_size*       | unsigned int          | Sets ringsize to n (mixin + 1).
|             | *unlock_time*     | unsigned int          | Number of blocks before the monero can be spent (0 to not add a lock).
|             | *payment_id*      | string                | (Optional) Random 32|byte/64|character hex string to identify a transaction.
|             | *get_tx_keys*     | boolean               | (Optional) Return the transaction keys after sending.
|             | *priority*        | unsigned int          | Set a priority for the transactions. Accepted Values are: 0|3 for: default, unimportant, normal, elevated, priority.
|             | *do_not_relay*    | boolean               | (Optional) If true, the newly created transaction will not be relayed to the monero network. (Defaults to false)
|             | *get_tx_hex*      | boolean               | Return the transactions as hex string after sending
|             | *new_algorithm*   | boolean               | True to use the new transaction construction algorithm, defaults to false.
|             | *get_tx_metadata* | boolean               | Return list of transaction metadata needed to relay the transfer later.
|**Outputs:** | tx_hash_list      | array of string       | The tx hashes of every transaction.
|             | tx_key_list       | array of string       | The transaction keys for every transaction.
|             | amount_list       | array of integer      | The amount transferred for every transaction.
|             | fee_list          | array of integer      | The amount of fees paid for every transaction.
|             | tx_blob_list      | array of string       | The tx as hex string for every transaction.
|             | tx_metadata_list  | array of string       | List of transaction metadata needed to relay the transactions later.
|             | multisig_txset    | string                | The set of signing keys used in a multisig transaction (empty for non|multisig).
|             | unsigned_txset    | string                | Set of unsigned tx for cold|signing purposes.
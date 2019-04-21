## **transfer**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"transfer","params":{"destinations":[{"amount":100000000000,"address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"},{"amount":200000000000,"address":"75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv"}],"account_index":0,"subaddr_indices":[0],"priority":0,"ring_size":7,"get_tx_key": true}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "transfer",
      "params": {
          "destinations": [
              {
                  "amount": 100000000000,
                  "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
              },
              {
                  "amount": 200000000000,
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
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "destinations": [
          {
              "amount": 100000000000,
              "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
          },
          {
              "amount": 200000000000,
              "address": "75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv",
          },
      ],
      "account_index": 0,
      "subaddr_indices": [0],
      "priority": 0,
      "ring_size": 7,
      "get_tx_key": True,
  }
  rpc_connection.transfer(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "amount": 300000000000,
      "fee": 86897600000,
      "multisig_txset": "",
      "tx_blob": "",
      "tx_hash": "7663438de4f72b25a0e395b770ea9ecf7108cd2f0c4b75be0b14a103d3362be9",
      "tx_key": "25c9d8ec20045c80c93d665c9d3684aab7335f8b2cd02e1ba2638485afd1c70e236c4bdd7a2f1cb511dbf466f13421bdf8df988b7b969c448ca6239d7251490e4bf1bbf9f6ffacffdcdc93b9d1648ec499eada4d6b4e02ce92d4a1c0452e5d009fbbbf15b549df8856205a4c7bda6338d82c823f911acd00cb75850b198c5803",
      "tx_metadata": "",
      "unsigned_txset": ""
    }
  }
```
Send monero to a number of recipients.  
Alias: *None*.  

|             | Parameter         | Type                  | Description
| ---         | ---               | ---                   | ---
|**Inputs:**  | *destinations*    |                       | array of destinations to receive XMR:
|             | ..*amount*        | unsigned int          | Amount to send to each destination, in @atomic|units.
|             | ..*address*       | string                | Destination public address.
|             | *account_index*   | unsigned int          | (Optional) Transfer from this account index. (Defaults to 0)
|             | *subaddr_indices* | array of unsigned int | (Optional) Transfer from this set of subaddresses. (Defaults to 0)
|             | *priority*        | unsigned int          | Set a priority for the transaction. Accepted Values are: 0|3 for: default, unimportant, normal, elevated, priority.
|             | *mixin*           | unsigned int          | Number of outputs from the blockchain to mix with (0 means no mixing).
|             | *ring_size*       | unsigned int          | Number of outputs to mix in the transaction (this output + N decoys from the blockchain).
|             | *unlock_time*     | unsigned int          | Number of blocks before the monero can be spent (0 to not add a lock).
|             | *payment_id*      | string                | (Optional) Random 32|byte/64|character hex string to identify a transaction.
|             | *get_tx_key*      | boolean               | (Optional) Return the transaction key after sending.
|             | *do_not_relay*    | boolean               | (Optional) If true, the newly created transaction will not be relayed to the monero network. (Defaults to false)
|             | *get_tx_hex*      | boolean               | Return the transaction as hex string after sending (Defaults to false)
|             | *get_tx_metadata* | boolean               | Return the metadata needed to relay the transaction. (Defaults to false)
|**Outputs:** | amount            |                       | Amount transferred for the transaction.
|             | fee               | int                   | Integer value of the fee charged for the txn.
|             | multisig_txset    |                       | Set of multisig transactions in the process of being signed (empty for non|multisig).
|             | tx_blob           |                       | Raw transaction represented as hex string, if get_tx_hex is true.
|             | tx_hash           | string                | String for the publically searchable transaction hash.
|             | tx_key            | string                | String for the transaction key if get_tx_key is true, otherwise, blank string.
|             | tx_metadata       |                       | Set of transaction metadata needed to relay this transfer later, if get_tx_metadata is true.
|             | unsigned_txset    | string                | Set of unsigned tx for cold-signing purposes.

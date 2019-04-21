## **sweep_single**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sweep_single","params":{"address":"74Jsocx8xbpTBEjm3ncKE5LBQbiJouyCDaGhgSiebpvNDXZnTAbW2CmUR5SsBeae2pNk9WMVuz6jegkC4krUyqRjA6VjoLD","ring_size":7,"unlock_time":0,"key_image":"a7834459ef795d2efb6f665d2fd758c8d9288989d8d4c712a68f8023f7804a5e","get_tx_keys":true}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "sweep_single",
      "params": {
          "address": "74Jsocx8xbpTBEjm3ncKE5LBQbiJouyCDaGhgSiebpvNDXZnTAbW2CmUR5SsBeae2pNk9WMVuz6jegkC4krUyqRjA6VjoLD",
          "ring_size": 7,
          "unlock_time": 0,
          "key_image": "a7834459ef795d2efb6f665d2fd758c8d9288989d8d4c712a68f8023f7804a5e",
          "get_tx_keys": True,
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "address": "74Jsocx8xbpTBEjm3ncKE5LBQbiJouyCDaGhgSiebpvNDXZnTAbW2CmUR5SsBeae2pNk9WMVuz6jegkC4krUyqRjA6VjoLD",
      "ring_size": 7,
      "unlock_time": 0,
      "key_image": "a7834459ef795d2efb6f665d2fd758c8d9288989d8d4c712a68f8023f7804a5e",
      "get_tx_keys": True,
  }
  rpc_connection.sweep_single(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "amount": 27126892247503,
      "fee": 14111630000,
      "multisig_txset": "",
      "tx_blob": "",
      "tx_hash": "106d4391a031e5b735ded555862fec63233e34e5fa4fc7edcfdbe461c275ae5b",
      "tx_key": "",
      "tx_metadata": "",
      "unsigned_txset": ""
    }
  }
```
Send all of a specific unlocked output to an address.  
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
|             | *payment_id*      | string                | (Optional) Random 32|byte/64|character hex string to identify a transaction.
|             | *get_tx_keys*     | boolean               | (Optional) Return the transaction keys after sending.
|             | *key_image*       | string                | Key image of specific output to sweep.
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
|             | unsigned_txset    | string                | Set of unsigned tx for cold|signing purposes.

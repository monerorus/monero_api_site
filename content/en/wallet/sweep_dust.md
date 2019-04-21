## **sweep_dust**

> In this example, `sweep_dust` returns nothing because there are no funds to sweep:  

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sweep_dust","params":{"get_tx_keys":true}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "sweep_dust",
      "params": {"get_tx_keys": True},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"get_tx_keys": True}
  rpc_connection.sweep_dust(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "multisig_txset": "",
      "unsigned_txset": ""
    }
  }
```
Send all dust outputs back to the wallet's, to make them easier to spend (and mix).  
Alias: *sweep_unmixable*.  

|             | Parameter         | Type             | Description
| ---         | ---               | ---              | ---
|**Inputs:**  | *get_tx_keys*     | boolean          | (Optional) Return the transaction keys after sending.
|             | *do_not_relay*    | boolean          | (Optional) If true, the newly created transaction will not be relayed to the monero network. (Defaults to false)
|             | *get_tx_hex*      | boolean          | (Optional) Return the transactions as hex string after sending. (Defaults to false)
|             | *get_tx_metadata* | boolean          | (Optional) Return list of transaction metadata needed to relay the transfer later. (Defaults to false)
|**Outputs:** | tx_hash_list      | array of string  | The tx hashes of every transaction.
|             | tx_key_list       | array of string  | The transaction keys for every transaction.
|             | amount_list       | array of integer | The amount transferred for every transaction.
|             | fee_list          | array of integer | The amount of fees paid for every transaction.
|             | tx_blob_list      | array of string  | The tx as hex string for every transaction.
|             | tx_metadata_list  | array of string  | List of transaction metadata needed to relay the transactions later.
|             | multisig_txset    | string           | The set of signing keys used in a multisig transaction (empty for non|multisig).
|             | unsigned_txset    | string           | Set of unsigned tx for cold|signing purposes.

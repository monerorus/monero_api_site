---
weight: 805
---

## **sign_transfer**

> In the example below, we first generate an unsigned_txset on a read only wallet before signing it:
> Generate unsigned_txset using the above "transfer" method on read-only wallet:

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"transfer","params":{"destinations":[{"amount":1000000000000,"address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"}],"account_index":0,"subaddr_indices":[0],"priority":0,"ring_size":7,"do_not_relay":true,"get_tx_hex":true}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "sign_transfer",
      "params": {
          "destinations": [
              {
                  "amount": 1000000000000,
                  "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
              }
          ],
          "account_index": 0,
          "subaddr_indices": [0],
          "priority": 0,
          "ring_size": 7,
          "do_not_relay": True,
          "get_tx_hex": True,
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
          }
      ],
      "account_index": 0,
      "subaddr_indices": [0],
      "priority": 0,
      "ring_size": 7,
      "do_not_relay": True,
      "get_tx_hex": True,
  }
  rpc_connection.sign_transfer(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "amount": 1000000000000,
      "fee": 15202740000,
      "multisig_txset": "",
      "tx_blob": "#...^ see introductionlong_hex#...^ see introduction",
      "tx_hash": "c648ba0a049e5ce4ec21361dbf6e4b21eac0f828eea9090215de86c76b31d0a4",
      "tx_key": "",
      "tx_metadata": "",
      "unsigned_txset": "#...^ see introductionlong_hex#...^ see introduction"
    }
  }
```

> Sign tx using the previously generated unsigned_txset

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sign_transfer","params":{"unsigned_txset": "#...^ see introductionlong_hex#...^ see introduction"}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "sign_transfer",
      "params": {"unsigned_txset": "#...^ see introductionlong_hex#...^ see introduction"},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"unsigned_txset": "#...^ see introductionlong_hex#...^ see introduction"}
  rpc_connection.sign_transfer(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "signed_txset": "#...^ see introductionlong_hex#...^ see introduction",
      "tx_hash_list": ["ff2e2d49fbfb1c9a55754f786576e171c8bf21b463a74438df604b7fa6cebc6d"]
    }
  }
```
Sign a transaction created on a read-only wallet (in cold-signing process)  
Alias: *None*.  

|             | Parameter        | Type            | Description
| ---         | ---              | ---             | ---
|**Inputs:**  | *unsigned_txset* | string          | Set of unsigned tx returned by "transfer" or "transfer_split" methods.
|             | *export_raw*     | boolean         | (Optional) If true, return the raw transaction data. (Defaults to false)
|**Outputs:** | signed_txset     | string          | Set of signed tx to be used for submitting transfer.
|             | tx_hash_list     | array of string | The tx hashes of every transaction.
|             | tx_raw_list      | array of string | The tx raw data of every transaction.
---
weight: 805
---

## **check_tx_key**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_tx_key","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","tx_key":"feba662cf8fb6d0d0da18fc9b70ab28e01cc76311278fdd7fe7ab16360762b06","address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "check_tx_key",
      "params": {
          "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
          "tx_key": "feba662cf8fb6d0d0da18fc9b70ab28e01cc76311278fdd7fe7ab16360762b06",
          "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
      "tx_key": "feba662cf8fb6d0d0da18fc9b70ab28e01cc76311278fdd7fe7ab16360762b06",
      "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
  }
  rpc_connection.check_tx_key(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "confirmations": 0,
      "in_pool": false,
      "received": 1000000000000
    }
  }
```
Check a transaction in the blockchain with its secret key.  
Alias: *None*.  

|             | Parameter     | Type         | Description
| ---         | ---           | ---          | ---
|**Inputs:**  | *txid*        | string       | transaction id.
|             | *tx_key*      | string       | transaction secret key.
|             | *address*     | string       | destination public address of the transaction.
|**Outputs:** | confirmations | unsigned int | Number of block mined after the one with the transaction.
|             | in_pool       | boolean      | States if the transaction is still in pool or has been added to a block.
|             | received      | unsigned int | Amount of the transaction.
## **check_tx_proof**

> In the example below, the transaction has been proven:

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_tx_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o","message":"this is my transaction","signature":"InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "check_tx_proof",
      "params": {
          "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
          "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
          "message": "this is my transaction",
          "signature": "InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ",
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
      "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
      "message": "this is my transaction",
      "signature": "InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ",
  }
  rpc_connection.check_tx_proof(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "confirmations": 482,
      "good": true,
      "in_pool": false,
      "received": 1000000000000
    }
  }
```

> In the example below, the wrong message is used, avoiding the transaction to be proved:

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_tx_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o","message":"wrong message","signature":"InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "check_tx_proof",
      "params": {
          "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
          "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
          "message": "wrong message",
          "signature": "InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ",
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
      "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
      "message": "wrong message",
      "signature": "InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ",
  }
  rpc_connection.check_tx_proof(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "confirmations": 0,
      "good": false,
      "in_pool": false,
      "received": 0
    }
  }
```
Prove a transaction by checking its signature.  
Alias: *None*.  

|             | Parameter     | Type         | Description
| ---         | ---           | ---          | ---
|**Inputs:**  | *txid*        | string       | transaction id.
|             | *address*     | string       | destination public address of the transaction.
|             | *message*     | string       | (Optional) Should be the same message used in `get_tx_proof`.
|             | *signature*   | string       | transaction signature to confirm.
|**Outputs:** | confirmations | unsigned int | Number of block mined after the one with the transaction.
|             | good          | boolean      | States if the inputs proves the transaction.
|             | in_pool       | boolean      | States if the transaction is still in pool or has been added to a block.
|             | received      | unsigned int | Amount of the transaction.

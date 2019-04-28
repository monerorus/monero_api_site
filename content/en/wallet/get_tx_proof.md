---
weight: 805
---

## **get_tx_proof**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_tx_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o","message":"this is my transaction"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_tx_proof",
      "params": {
          "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
          "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
          "message": "this is my transaction",
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
  }
  rpc_connection.get_tx_proof(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "signature": "InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ"
    }
  }
```
Get transaction signature to prove it.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *txid*    | string | transaction id.
|             | *address* | string | destination public address of the transaction.
|             | *message* | string | (Optional) add a message to the signature to further authenticate the prooving process.
|**Outputs:** | signature | string | transaction signature.
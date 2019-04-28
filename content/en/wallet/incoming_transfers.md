---
weight: 805
---

## **incoming_transfers**

> get all transfers:

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"incoming_transfers","params":{"transfer_type":"all","account_index":0,"subaddr_indices":[3],"verbose":true}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "incoming_transfers",
      "params": {
          "transfer_type": "all",
          "account_index": 0,
          "subaddr_indices": [3],
          "verbose": True,
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "transfer_type": "all",
      "account_index": 0,
      "subaddr_indices": [3],
      "verbose": True,
  }
  rpc_connection.incoming_transfers(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "transfers": [{
        "amount": 60000000000000,
        "global_index": 122405,
        "key_image": "768f5144777eb23477ab7acf83562581d690abaf98ca897c03a9d2b900eb479b",
        "spent": true,
        "subaddr_index": 3,
        "tx_hash": "f53401f21c6a43e44d5dd7a90eba5cf580012ad0e15d050059136f8a0da34f6b",
        "tx_size": 159
      },{
        "amount": 27126892247503,
        "global_index": 594994,
        "key_image": "7e561394806afd1be61980cc3431f6ef3569fa9151cd8d234f8ec13aa145695e",
        "spent": false,
        "subaddr_index": 3,
        "tx_hash": "106d4391a031e5b735ded555862fec63233e34e5fa4fc7edcfdbe461c275ae5b",
        "tx_size": 157
      },{
        "amount": 27169374733655,
        "global_index": 594997,
        "key_image": "e76c0a3bfeaae35e4173712f782eb34011198e26b990225b71aa787c8ba8a157",
        "spent": false,
        "subaddr_index": 3,
        "tx_hash": "0bd959b59117ee1254bd8e5aa8e77ec04ef744144a1ffb2d5c1eb9380a719621",
        "tx_size": 158
      }]
    }
  }
```

> get available transfers:

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"incoming_transfers","params":{"transfer_type":"available","account_index":0,"subaddr_indices":[3],"verbose":true}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "incoming_transfers",
      "params": {
          "transfer_type": "available",
          "account_index": 0,
          "subaddr_indices": [3],
          "verbose": True,
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "transfer_type": "available",
      "account_index": 0,
      "subaddr_indices": [3],
      "verbose": True,
  }
  rpc_connection.incoming_transfers(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "transfers": [{
        "amount": 27126892247503,
        "global_index": 594994,
        "key_image": "7e561394806afd1be61980cc3431f6ef3569fa9151cd8d234f8ec13aa145695e",
        "spent": false,
        "subaddr_index": 3,
        "tx_hash": "106d4391a031e5b735ded555862fec63233e34e5fa4fc7edcfdbe461c275ae5b",
        "tx_size": 157
      },{
        "amount": 27169374733655,
        "global_index": 594997,
        "key_image": "e76c0a3bfeaae35e4173712f782eb34011198e26b990225b71aa787c8ba8a157",
        "spent": false,
        "subaddr_index": 3,
        "tx_hash": "0bd959b59117ee1254bd8e5aa8e77ec04ef744144a1ffb2d5c1eb9380a719621",
        "tx_size": 158
      }]
    }
  }
```

> get unavailable transfers:

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"incoming_transfers","params":{"transfer_type":"unavailable","account_index":0,"subaddr_indices":[3],"verbose":true}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "incoming_transfers",
      "params": {
          "transfer_type": "unavailable",
          "account_index": 0,
          "subaddr_indices": [3],
          "verbose": True,
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "transfer_type": "unavailable",
      "account_index": 0,
      "subaddr_indices": [3],
      "verbose": True,
  }
  rpc_connection.incoming_transfers(params)
```
```json
  {
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "transfers": [{
      "amount": 60000000000000,
      "global_index": 122405,
      "key_image": "768f5144777eb23477ab7acf83562581d690abaf98ca897c03a9d2b900eb479b",
      "spent": true,
      "subaddr_index": 3,
      "tx_hash": "f53401f21c6a43e44d5dd7a90eba5cf580012ad0e15d050059136f8a0da34f6b",
      "tx_size": 159
    }]
  }
  }
```
Return a list of incoming transfers to the wallet.  

|             | Parameter         | Type                  | Description
| ---         | ---               | ---                   | ---
|**Inputs:**  | *transfer_type*   | string                | "all": all the transfers, "available": only transfers which are not yet spent, OR "unavailable": only transfers which are already spent.
|             | *account_index*   | unsigned int          | (Optional) Return transfers for this account. (defaults to 0)
|             | *subaddr_indices* | array of unsigned int | (Optional) Return transfers sent to these subaddresses.
|             | *verbose*         | boolean               | (Optional) Enable verbose output, return key image if true.
|**Outputs:** | transfers         |                       | list of:
|             | ..amount          | unsigned int          | Amount of this transfer.
|             | ..global_index    | unsigned int          | Mostly internal use, can be ignored by most users.
|             | ..key_image       | string                | Key image for the incoming transfer's unspent output (empty unless verbose is true).
|             | ..spent           | boolean               | Indicates if this transfer has been spent.
|             | ..subaddr_index   | unsigned int          | Subaddress index for incoming transfer.
|             | ..tx_hash         | string                | Several incoming transfers may share the same hash if they were in the same transaction.
|             | ..tx_size         | unsigned int          | Size of transaction in bytes.
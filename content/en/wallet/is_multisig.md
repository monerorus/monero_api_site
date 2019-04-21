## **is_multisig**

> Example for a non-multisig wallet:

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"is_multisig"}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "is_multisig",
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  rpc_connection.is_multisig()
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "multisig": false,
      "ready": false,
      "threshold": 0,
      "total": 0
    }
  }
```

> Example for a multisig wallet:

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"is_multisig"}' -H 'Content-Type: application/json'                  
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "is_multisig",
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  rpc_connection.is_multisig()
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "multisig": true,
      "ready": true,
      "threshold": 2,
      "total": 2
    }
  }
```
Check if a wallet is a multisig one.  
Alias: *None*.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *None*.   |              |
|**Outputs:** | multisig  | boolean      | States if the wallet is multisig
|             | ready     | boolean      | 
|             | threshold | unsigned int | Amount of signature needed to sign a transfer.
|             | total     | unsigned int | Total amount of signature in the multisig wallet.

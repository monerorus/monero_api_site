## **prepare_multisig**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"prepare_multisig"}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "prepare_multisig",
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  rpc_connection.prepare_multisig()
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "multisig_info": "MultisigV1BFdxQ653cQHB8wsj9WJQd2VdnjxK89g5M94dKPBNw22reJnyJYKrz6rJeXdjFwJ3Mz6n4qNQLd6eqUZKLiNzJFi3UPNVcTjtkG2aeSys9sYkvYYKMZ7chCxvoEXVgm74KKUcUu4V8xveCBFadFuZs8shnxBWHbcwFr5AziLr2mE7KHJT"
    }
  }
```
Prepare a wallet for multisig by generating a multisig string to share with peers.  
Alias: *None*.  

|             | Parameter     | Type   | Description
| ---         | ---           | ---    | ---
|**Inputs:**  | *None*.       |        |
|**Outputs:** | multisig_info | string | Multisig string to share with peers to create the multisig wallet.

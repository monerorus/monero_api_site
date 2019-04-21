## **import_multisig_info**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"import_multisig_info","params":{"info":["...^ see introductionmultisig_info...^ see introduction"]}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "import_multisig_info",
      "params": {"info": ["...^ see introductionmultisig_info...^ see introduction"]},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"info": ["...^ see introductionmultisig_info...^ see introduction"]}
  rpc_connection.import_multisig_info(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "n_outputs": 35
    }
  }
```
Import multisig info from other participants.  
Alias: *None*.  

|             | Parameter  | Type            | Description
| ---         | ---        | ---             | ---
|**Inputs:**  | *info*     | array of string | List of multisig info in hex format from other participants.
|**Outputs:** | n_outputs  | unsigned int    | Number of outputs signed with those multisig info.

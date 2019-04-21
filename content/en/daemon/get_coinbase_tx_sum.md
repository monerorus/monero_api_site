## **get_coinbase_tx_sum**


```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_coinbase_tx_sum","params":{"height":1563078,"count":2}}' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "emission_amount": 9387854817320,
    "fee_amount": 83981380000,
    "status": "OK"
  }
}
```
Get the coinbase ammount and the fees ammount for n last blocks starting at particular height  
Alias: None.  

|             | Parameter       | Type         | Description
| ---         | ---             | ---          | ---
|**Inputs:**  | *height*        | unsigned int | Block height from which getting the amounts
|             | *count*         | unsigned int | number of blocks to include in the sum
|**Outputs:** | emission_amount | unsigned int | amount of coinbase reward in @atomic-units
|             | fee_amount      | unsigned int | amount of fees in @atomic-units
|             | status          | string       | General RPC error code. "OK" means everything looks good.

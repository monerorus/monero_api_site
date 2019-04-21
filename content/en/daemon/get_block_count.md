## **get_block_count**



```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_block_count"}' -H 'Content-Type: application/json'
```
```json
{  
  "id": "0",  
  "jsonrpc": "2.0",  
  "result": {  
    "count": 993163,  
    "status": "OK"  
  }  
}  
```
Look up how many blocks are in the longest chain known to the node.  
Alias: **getblockcount**.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *None*    |              |
|**Outputs:** | count     | unsigned int | Number of blocks in longest chain seen by the node.
|             | status    | string       | General RPC error code. "OK" means everything looks good.

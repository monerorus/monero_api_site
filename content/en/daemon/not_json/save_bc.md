## **/save_bc**

```shell
$ curl -X POST http://127.0.0.1:18081/save_bc -H 'Content-Type: application/json'
```
```json
{
  "status": "OK"
}
```
Save the blockchain. The blockchain does not need saving and is always saved when modified, however it does a sync to flush the filesystem cache onto the disk for safety purposes against Operating System or Harware crashes.  
Alias: None.  

|             | Parameter | Type    | Description
| ---         | ---       | ---     | ---
|**Inputs:**  | *None*.   |         | 
|**Outputs:** | status    | string  | General RPC error code. "OK" means everything looks good. Any other value means that something went wrong.

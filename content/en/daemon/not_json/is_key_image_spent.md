## **/is_key_image_spent**

```shell
$ curl -X POST http://127.0.0.1:18081/is_key_image_spent -d '{"key_images":["8d1bd8181bf7d857bdb281e0153d84cd55a3fcaa57c3e570f4a49f935850b5e3","7319134bfc50668251f5b899c66b005805ee255c136f0e1cecbb0f3a912e09d4"]}' -H 'Content-Type: application/json'
```
```json
{
  "spent_status": [1,2],
  "status": "OK"
  "untrusted": false
}
```
Check if outputs have been spent using the key image associated with the output.  
Alias: None.  
|             | Parameter    | Type              | Description
| ---         | ---          | ---               | ---
|**Inputs:**  | *key_images* | string list       | List of key image hex strings to check.
|**Outputs:** | spent_status | unsigned int list | List of statuses for each image checked. Statuses are follows: 0 = unspent, 1 = spent in blockchain, 2 = spent in transaction pool
|             | status       | string            | General RPC error code. "OK" means everything looks good.
|             | untrusted    | boolean           | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).

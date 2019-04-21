## **/start_mining**

```shell
$ curl -X POST http://127.0.0.1:18081/start_mining -d '{"do_background_mining":false,"ignore_battery":true,"miner_address":"47xu3gQpF569au9C2ajo5SSMrWji6xnoE5vhr94EzFRaKAGw6hEGFXYAwVADKuRpzsjiU1PtmaVgcjUJF89ghGPhUXkndHc","threads_count":1}' -H 'Content-Type: application/json'
```
```json
{
  "status": "OK"
}
```
Start mining on the daemon.  
Alias: None.  

|             | Parameter              | Type         | Description
| ---         | ---                    | ---          | ---
|**Inputs:**  | *do_background_mining* | boolean      | States if the mining should run in background (`true`) or foreground (`false`).
|             | *ignore_battery*       | boolean      | States if batery state (on laptop) should be ignored (`true`) or not (`false`).
|             | *miner_address*        | string       | Account address to mine to.
|             | *threads_count*        | unsigned int | Number of mining thread to run.
|**Outputs:** | status                 | string       | General RPC error code. "OK" means everything looks good. Any other value means that something went wrong.

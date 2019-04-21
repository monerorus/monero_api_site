## **/send_raw_transaction**

> Example (No return information included here.):

```shell
$ curl -X POST http://127.0.0.1:18081/send_raw_transaction -d '{"tx_as_hex":"de6a3...", "do_not_relay":false}' -H 'Content-Type: application/json'
```

Broadcast a raw transaction to the network.  
Alias: **/sendrawtransaction**.  

|             | Parameter      | Type    | Description
| ---         | ---            | ---     | ---
|**Inputs:**  | *tx_as_hex*    | string  | Full transaction information as hexidecimal string.
|             | *do_not_relay* | boolean | Stop relaying transaction to other nodes (default is `false`).
|**Outputs:** | double_spend   | boolean | Transaction is a double spend (`true`) or not (`false`).
|             | fee_too_low    | boolean | Fee is too low (`true`) or OK (`false`).
|             | invalid_input  | boolean | Input is invalid (`true`) or valid (`false`).
|             | invalid_output | boolean | Output is invalid (`true`) or valid (`false`).
|             | low_mixin      | boolean | Mixin count is too low (`true`) or OK (`false`).
|             | not_rct        | boolean | Transaction is a standard ring transaction (`true`) or a ring confidential transaction (`false`).
|             | not_relayed    | boolean | Transaction was not relayed (`true`) or relayed (`false`).
|             | overspend      | boolean | Transaction uses more money than available (`true`) or not (`false`).
|             | reason         | string  | Additional information. Currently empty or "Not relayed" if transaction was accepted but not relayed.
|             | status         | string  | General RPC error code. "OK" means everything looks good. Any other value means that something went wrong.
|             | too_big        | boolean | Transaction size is too big (`true`) or OK (`false`).
|             | untrusted      | boolean | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).

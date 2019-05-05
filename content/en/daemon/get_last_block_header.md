---
weight: 205
---

## **get_last_block_header**

> In this example, the most recent block (1562023 at the time) is returned:

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_last_block_header"}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_last_block_header",
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  rpc_connection.get_last_block_header()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "block_header": {
      "block_size": 62774,
      "depth": 0,
      "difficulty": 60097900840,
      "hash": "3a289b8fa88b10e2163826c230b45d79f2be37d14fa3153ee58ff8a427782d14",
      "height": 1562023,
      "major_version": 7,
      "minor_version": 7,
      "nonce": 3789681204,
      "num_txes": 5,
      "orphan_status": false,
      "prev_hash": "743e5d0a26849efe27b96086f2c4ecc39a0bc744bf21473dad6710221aff6ac3",
      "reward": 4724029079703,
      "timestamp": 1525029411
    },
    "status": "OK",
    "untrusted": false
  }
}
```
Block header information for the most recent block is easily retrieved with this method. No inputs are needed.  
Alias: **getlastblockheader**.  


|             | Parameter       | Type         | Description
| ---         | ---             | ---          | ---
|**Inputs:**  | *None*.         |              |
|**Outputs:** |  block_header   |              | A structure containing block header information.
|             | ..block_size    | unsigned int | The block size in bytes.
|             | ..depth         | unsigned int | The number of blocks succeeding this block on the blockchain. A larger number means an older block.
|             | ..difficulty    | unsigned int | The strength of the Monero network based on mining power.
|             | ..hash          | string       | The hash of this block.
|             | ..height        | unsigned int | The number of blocks preceding this block on the blockchain.
|             | ..major_version | unsigned int | The major version of the monero protocol at this block height.
|             | ..minor_version | unsigned int | The minor version of the monero protocol at this block height.
|             | ..nonce         | unsigned int | a cryptographic random one-time number used in mining a Monero block.
|             | ..num_txes      | unsigned int | Number of transactions in the block, not counting the coinbase tx.
|             | ..orphan_status | boolean      | Usually `false`. If `true`, this block is not part of the longest chain.
|             | ..prev_hash     | string       | The hash of the block immediately preceding this block in the chain.
|             | ..reward        | unsigned int | The amount of new @atomic-units generated in this block and rewarded to the miner. Note: 1 XMR = 1e12 @atomic-units.
|             | ..timestamp     | unsigned int | The unix time at which the block was recorded into the blockchain.
|             | status          | string       | General RPC error code. "OK" means everything looks good.
|             | untrusted       | boolean      | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).

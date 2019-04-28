---
weight: 205
---

## **get_info**


```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_info"}' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "alt_blocks_count": 6,
    "block_size_limit": 600000,
    "block_size_median": 129017,
    "bootstrap_daemon_address": "",
    "cumulative_difficulty": 14121125493385685,
    "difficulty": 60580751777,
    "free_space": 138758750208,
    "grey_peerlist_size": 4998,
    "height": 1562168,
    "height_without_bootstrap": 1562168,
    "incoming_connections_count": 2,
    "mainnet": true,
    "offline": false,
    "outgoing_connections_count": 8,
    "rpc_connections_count": 2,
    "stagenet": false,
    "start_time": 1524751757,
    "status": "OK",
    "target": 120,
    "target_height": 1562063,
    "testnet": false,
    "top_block_hash": "7a7ba647080844073fdd8e3a069e00554c773d6e6863354dba1dec45a43f5592",
    "tx_count": 2759894,
    "tx_pool_size": 755,
    "untrusted": false,
    "was_bootstrap_ever_used": false,
    "white_peerlist_size": 1000
  }
}
```
Retrieve general information about the state of your node and the network.  
Alias:  

* **/get_info**
* **/getinfo**

See other RPC Methods [/get_info (not JSON)](#get-info-not-json)  

|             | Parameter                  | Type         | Description
| ---         | ---                        | ---          | ---
|**Inputs:**  | *None*.                    |              | 
|**Outputs:** | alt_blocks_count           | unsigned int | Number of alternative blocks to main chain.
|             | block_size_limit           | unsigned int | Maximum allowed block size
|             | block_size_median          | unsigned int | Median block size of latest 100 blocks
|             | bootstrap_daemon_address   | string       | @Bootstrap-node to give immediate usability to wallets while syncing by proxying RPC to it. (Note: the replies may be untrustworthy).
|             | cumulative_difficulty      | unsigned int | Cumulative difficulty of all blocks in the blockchain.
|             | difficulty                 | unsigned int | Network difficulty (analogous to the strength of the network)
|             | free_space                 | unsigned int | Available disk space on the node.
|             | grey_peerlist_size         | unsigned int | Grey Peerlist Size
|             | height                     | unsigned int | Current length of longest chain known to daemon.
|             | height_without_bootstrap   | unsigned int | Current length of the local chain of the daemon.
|             | incoming_connections_count | unsigned int | Number of peers connected to and pulling from your node.
|             | mainnet                    | boolean      | States if the node is on the mainnet (`true`) or not (`false`).
|             | offline                    | boolean      | States if the node is offline (`true`) or online (`false`).
|             | outgoing_connections_count | unsigned int | Number of peers that you are connected to and getting information from.
|             | rpc_connections_count      | unsigned int | Number of RPC client connected to the daemon (Including this RPC request).
|             | stagenet                   | boolean      | States if the node is on the stagenet (`true`) or not (`false`).
|             | start_time                 | unsigned int | Start time of the daemon, as UNIX time.
|             | status                     | string       | General RPC error code. "OK" means everything looks good.
|             | target                     | unsigned int | Current target for next proof of work.
|             | target_height              | unsigned int | The height of the next block in the chain.
|             | testnet                    | boolean      | States if the node is on the testnet (`true`) or not (`false`).
|             | top_block_hash             | string       | Hash of the highest block in the chain.
|             | tx_count                   | unsigned int | Total number of non-coinbase transaction in the chain.
|             | tx_pool_size               | unsigned int | Number of transactions that have been broadcast but not included in a block.
|             | untrusted                  | boolean      | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).
|             | was_bootstrap_ever_used    | boolean      | States if a bootstrap node has ever been used since the daemon started.
|             | white_peerlist_size        | unsigned int | White Peerlist Size

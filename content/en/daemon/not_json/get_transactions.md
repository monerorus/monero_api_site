---
weight: 305
---

## **/get_transactions**

> Example 1: Return transaction information in binary format.

```shell
$ curl -X POST http://127.0.0.1:18081/get_transactions -d '{"txs_hashes":["d6e48158472848e6687173a91ae6eebfa3e1d778e65252ee99d7515d63090408"]}' -H 'Content-Type: application/json'
```
```json
{
  "status": "OK",
  "txs": [{
    "as_hex": "...",
    "as_json": "",
    "block_height": 993442,
    "block_timestamp": 1457749396,
    "double_spend_seen": false,
    "in_pool": false,
    "output_indices": [198769,418598,176616,50345,509],
    "tx_hash": "d6e48158472848e6687173a91ae6eebfa3e1d778e65252ee99d7515d63090408"
  }],
  "txs_as_hex": ["..."],
  "untrusted": false
}
```

> Example 2: Decode returned transaction information in JSON format. Note: the "vin", "vout" and "signatures" list have been truncated in the displayed return for space considerations.

```shell
$ curl -X POST http://127.0.0.1:18081/get_transactions -d '{"txs_hashes":["d6e48158472848e6687173a91ae6eebfa3e1d778e65252ee99d7515d63090408"],"decode_as_json":true}' -H 'Content-Type: application/json'
```
```json
{
  "status": "OK",
  "txs": [{
    "as_hex": "...",
    "as_json": "{\n  \"version\": 1, \n  \"unlock_time\": 0, \n  \"vin\": [ {\n      \"key\": {\n        \"amount\": 9999999999, \n        \"key_offsets\": [ 691\n        ], \n        \"k_image\": \"6ebee1b651a8da723462b4891d471b990ddc226049a0866d3029b8e2f75b7012\"\n      }\n    }, {\n      \"key\": {\n        \"amount\": 9000000000000, \n        \"key_offsets\": [ 175760\n        ], \n        \"k_image\": \"200bd02b70ee707441a8863c5279b4e4d9f376dc97a140b1e5bc7d72bc508069\"\n      }\n    }, ... \n  ], \n  \"vout\": [ {\n      \"amount\": 60000000000, \n      \"target\": {\n        \"key\": \"8c792dea94dab48160e067fb681edd6247ba375281fbcfedc03cb970f3b98e2d\"\n      }\n    }, {\n      \"amount\": 700000000000, \n      \"target\": {\n        \"key\": \"1ab33e69737e157d23e33274c42793be06a8711670e73fa10ecebc604f87cc71\"\n      }\n    }, ... \n  ], \n  \"extra\": [ 1, 3, 140, 109, 156, 205, 47, 148, 153, 9, 17, 93, 83, 33, 162, 110, 152, 1, 139, 70, 121, 19, 138, 10, 44, 6, 55, 140, 242, 124, 143, 219, 172\n  ], \n  \"signatures\": [ \"fd82214a59c99d9251fa00126d353f9cf502a80d8993a6c223e3c802a40ab405555637f495903d3ba558312881e586d452e6e95826d8e128345f6c0a8f9f350e\", \"8c04ef50cf34afa3a9ec19c457143496f8cf7045ed869b581f9efa2f1d65e30f1cec5272b00e9c61a34bdd3c78cf82ae8ef4df3132f70861391069b9c255cd08\", ... ]\n}",
    "block_height": 993442,
    "block_timestamp": 1457749396,
    "double_spend_seen": false,
    "in_pool": false,
    "output_indices": [198769,418598,176616,50345,509],
    "tx_hash": "d6e48158472848e6687173a91ae6eebfa3e1d778e65252ee99d7515d63090408"
  }],
  "txs_as_hex": ["..."],
  "txs_as_json": ["{\n  \"version\": 1, \n  \"unlock_time\": 0, \n  \"vin\": [ {\n      \"key\": {\n        \"amount\": 9999999999, \n        \"key_offsets\": [ 691\n        ], \n        \"k_image\": \"6ebee1b651a8da723462b4891d471b990ddc226049a0866d3029b8e2f75b7012\"\n      }\n    }, {\n      \"key\": {\n        \"amount\": 9000000000000, \n        \"key_offsets\": [ 175760\n        ], \n        \"k_image\": \"200bd02b70ee707441a8863c5279b4e4d9f376dc97a140b1e5bc7d72bc508069\"\n      }\n    }, ... \n  ], \n  \"vout\": [ {\n      \"amount\": 60000000000, \n      \"target\": {\n        \"key\": \"8c792dea94dab48160e067fb681edd6247ba375281fbcfedc03cb970f3b98e2d\"\n      }\n    }, {\n      \"amount\": 700000000000, \n      \"target\": {\n        \"key\": \"1ab33e69737e157d23e33274c42793be06a8711670e73fa10ecebc604f87cc71\"\n      }\n    }, ... \n  ], \n  \"extra\": [ 1, 3, 140, 109, 156, 205, 47, 148, 153, 9, 17, 93, 83, 33, 162, 110, 152, 1, 139, 70, 121, 19, 138, 10, 44, 6, 55, 140, 242, 124, 143, 219, 172\n  ], \n  \"signatures\": [ \"fd82214a59c99d9251fa00126d353f9cf502a80d8993a6c223e3c802a40ab405555637f495903d3ba558312881e586d452e6e95826d8e128345f6c0a8f9f350e\", \"8c04ef50cf34afa3a9ec19c457143496f8cf7045ed869b581f9efa2f1d65e30f1cec5272b00e9c61a34bdd3c78cf82ae8ef4df3132f70861391069b9c255cd08\", ... ]\n}"],
  "untrusted": false
}
```
> Example 3: Returned a missed (unexisting) transaction.

```shell
curl -X POST http://127.0.0.1:18081/get_transactions -d '{"txs_hashes":["d6e48158472848e6687173a91ae6eebfa3e1d778e65252ee99d7515d63090409"]}' -H 'Content-Type: application/json'
```
```json
{
  "missed_tx": ["d6e48158472848e6687173a91ae6eebfa3e1d778e65252ee99d7515d63090409"],
  "status": "OK",
  "untrusted": false
}
```

Look up one or more transactions by hash.  
Alias: **/gettransactions**.  


|             | Parameter           | Type                  | Description
| ---         | ---                 | ---                   | ---
|**Inputs:**  | *txs_hashes*        | string list           | List of transaction hashes to look up.
|             | *decode_as_json*    | boolean               | Optional (`false` by default). If set `true`, the returned transaction information will be decoded rather than binary.
|             | *prune*             | boolean               | Optional (`false` by default).
|**Outputs:** | missed_tx           | array of strings      | (Optional - returned if not empty) Transaction hashes that could not be found.
|             | status              |                       | General RPC error code. "OK" means everything looks good.
|             | txs                 |                       | array of structure *entry* as follows:
|             | ..as_hex            | string                | Full transaction information as a hex string.
|             | ..as_json           | json string           |  List of transaction info:
|             | ....version         |                       | Transaction version
|             | ....unlock_time     |                       | If not 0, this tells when a transaction output is spendable.
|             | ....vin             |                       | List of inputs into transaction:
|             | ......key           |                       | The public key of the previous output spent in this transaction.
|             | ........amount      |                       | The amount of the input, in @atomic-units.
|             | ........key_offsets |                       | A list of integer offets to the input.
|             | ........k_image     |                       | The key image for the given input
|             | ....vout            |                       | List of outputs from transaction:
|             | ......amount        |                       | Amount of transaction output, in @atomic-units.
|             | ......target        |                       | Output destination information:
|             | .......key          |                       | The stealth public key of the receiver. Whoever owns the private key associated with this key controls this transaction output.
|             | ....extra           |                       | Usually called the "payment ID" but can be used to include any random 32 bytes.
|             | ....signatures      |                       | List of signatures used in ring signature to hide the true origin of the transaction.
|             | ..block_height      | unsigned int          | block height including the transaction
|             | ..block_timestamp   | unsigned int          | Unix time at chich the block has been added to the blockchain
|             | ..double_spend_seen | boolean               | States if the transaction is a double-spend (`true`) or not (`false`)
|             | ..in_pool           | boolean               | States if the transaction is in pool (`true`) or included in a block (`false`)
|             | ..output_indices    | array of unsigned int | transaction indexes
|             | ..tx_hash           | string                | transaction hash
|             | txs_as_hex          | string                | Full transaction information as a hex string (old compatibility parameter)
|             | txs_as_json         | json string           | (Optional - returned if set in inputs. Old compatibility parameter) List of transaction as in *as_json* above:


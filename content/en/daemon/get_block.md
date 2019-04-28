---
weight: 205
---

## **get_block**

> Look up by height   
> In the following example, block 912345 is looked up by its height. Note that block 912345 does not have any non-coinbase transactions. (See the next example for a block with extra transactions):

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_block","params":{"height":912345}}' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "blob": "0102f4bedfb405b61c58b2e0be53fad5ef9d9731a55e8a81d972b8d90ed07c04fd37ca6403ff786e0600000195d83701ffd9d73704ee84ddb42102378b043c1724c92c69d923d266fe86477d3a5ddd21145062e148c64c5767700880c0fc82aa020273733cbd6e6218bda671596462a4b062f95cfe5e1dbb5b990dacb30e827d02f280f092cbdd080247a5dab669770da69a860acde21616a119818e1a489bb3c4b1b6b3c50547bc0c80e08d84ddcb01021f7e4762b8b755e3e3c72b8610cc87b9bc25d1f0a87c0c816ebb952e4f8aff3d2b01fd0a778957f4f3103a838afda488c3cdadf2697b3d34ad71234282b2fad9100e02080000000bdfc2c16c00",
    "block_header": {
      "block_size": 210,
      "depth": 649772,
      "difficulty": 815625611,
      "hash": "e22cf75f39ae720e8b71b3d120a5ac03f0db50bba6379e2850975b4859190bc6",
      "height": 912345,
      "major_version": 1,
      "minor_version": 2,
      "nonce": 1646,
      "num_txes": 0,
      "orphan_status": false,
      "prev_hash": "b61c58b2e0be53fad5ef9d9731a55e8a81d972b8d90ed07c04fd37ca6403ff78",
      "reward": 7388968946286,
      "timestamp": 1452793716
    },
    "json": "{\n  \"major_version\": 1, \n  \"minor_version\": 2, \n  \"timestamp\": 1452793716, \n  \"prev_id\": \"b61c58b2e0be53fad5ef9d9731a55e8a81d972b8d90ed07c04fd37ca6403ff78\", \n  \"nonce\": 1646, \n  \"miner_tx\": {\n    \"version\": 1, \n    \"unlock_time\": 912405, \n    \"vin\": [ {\n        \"gen\": {\n          \"height\": 912345\n        }\n      }\n    ], \n    \"vout\": [ {\n        \"amount\": 8968946286, \n        \"target\": {\n          \"key\": \"378b043c1724c92c69d923d266fe86477d3a5ddd21145062e148c64c57677008\"\n        }\n      }, {\n        \"amount\": 80000000000, \n        \"target\": {\n          \"key\": \"73733cbd6e6218bda671596462a4b062f95cfe5e1dbb5b990dacb30e827d02f2\"\n        }\n      }, {\n        \"amount\": 300000000000, \n        \"target\": {\n          \"key\": \"47a5dab669770da69a860acde21616a119818e1a489bb3c4b1b6b3c50547bc0c\"\n        }\n      }, {\n        \"amount\": 7000000000000, \n        \"target\": {\n          \"key\": \"1f7e4762b8b755e3e3c72b8610cc87b9bc25d1f0a87c0c816ebb952e4f8aff3d\"\n        }\n      }\n    ], \n    \"extra\": [ 1, 253, 10, 119, 137, 87, 244, 243, 16, 58, 131, 138, 253, 164, 136, 195, 205, 173, 242, 105, 123, 61, 52, 173, 113, 35, 66, 130, 178, 250, 217, 16, 14, 2, 8, 0, 0, 0, 11, 223, 194, 193, 108\n    ], \n    \"signatures\": [ ]\n  }, \n  \"tx_hashes\": [ ]\n}",
    "miner_tx_hash": "c7da3965f25c19b8eb7dd8db48dcd4e7c885e2491db77e289f0609bf8e08ec30",
    "status": "OK",
    "untrusted": false
  }
}
```

> Look up by hash  
> In the following example, block 993056 is looked up by its hash. Note that block 993056 has 3 non-coinbase transactions:

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_block","params":{"hash":"510ee3c4e14330a7b96e883c323a60ebd1b5556ac1262d0bc03c24a3b785516f"}}' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "blob": "0102a3978cb7050ea4af6547c05c965afc8df6d31509ff3105dc7ae6b10172521d77e09711fd6df407000001dcce3c01ffa0ce3c049da8bece070259e9d685b3484886bc7b47c133e6099ecdf212d5eaa16ce19cd58e8c3c1e590a80d88ee16f024c5e2f542d25513c46b9e3b7d40140a22d0ae5314bfcae492ad9f56fff8185f080d0b8e1981a0213dd8ffdac9e6a2f71e327dad65328198dc879a492d145eae72677c0703a351580c0f9decfae010262bda00341681dccbc066757862da593734395745bdfe1fdc89b5948c86a5d4c2b01b691851cf057b9c302a3dbca879e1cba4cc45061ca55aaa6e03cdc67ab9e455002080000000c617fdf160379c6b9f00db027bde151705aafe85c495883aae2597d5cb8e1adb2e0f3ae1d07d715db73331abc3ec588ef07c7bb195786a4724b08dff431b51ffa32a4ce899bb197066426c0ed89f0b431fe171f7fd62bc95dd29943daa7cf3585cf1fdfc99d",
    "block_header": {
      "block_size": 3981,
      "depth": 569068,
      "difficulty": 964985344,
      "hash": "510ee3c4e14330a7b96e883c323a60ebd1b5556ac1262d0bc03c24a3b785516f",
      "height": 993056,
      "major_version": 1,
      "minor_version": 2,
      "nonce": 2036,
      "num_txes": 3,
      "orphan_status": false,
      "prev_hash": "0ea4af6547c05c965afc8df6d31509ff3105dc7ae6b10172521d77e09711fd6d",
      "reward": 6932043647005,
      "timestamp": 1457720227
    },
    "json": "{\n  \"major_version\": 1, \n  \"minor_version\": 2, \n  \"timestamp\": 1457720227, \n  \"prev_id\": \"0ea4af6547c05c965afc8df6d31509ff3105dc7ae6b10172521d77e09711fd6d\", \n  \"nonce\": 2036, \n  \"miner_tx\": {\n    \"version\": 1, \n    \"unlock_time\": 993116, \n    \"vin\": [ {\n        \"gen\": {\n          \"height\": 993056\n        }\n      }\n    ], \n    \"vout\": [ {\n        \"amount\": 2043647005, \n        \"target\": {\n          \"key\": \"59e9d685b3484886bc7b47c133e6099ecdf212d5eaa16ce19cd58e8c3c1e590a\"\n        }\n      }, {\n        \"amount\": 30000000000, \n        \"target\": {\n          \"key\": \"4c5e2f542d25513c46b9e3b7d40140a22d0ae5314bfcae492ad9f56fff8185f0\"\n        }\n      }, {\n        \"amount\": 900000000000, \n        \"target\": {\n          \"key\": \"13dd8ffdac9e6a2f71e327dad65328198dc879a492d145eae72677c0703a3515\"\n        }\n      }, {\n        \"amount\": 6000000000000, \n        \"target\": {\n          \"key\": \"62bda00341681dccbc066757862da593734395745bdfe1fdc89b5948c86a5d4c\"\n        }\n      }\n    ], \n    \"extra\": [ 1, 182, 145, 133, 28, 240, 87, 185, 195, 2, 163, 219, 202, 135, 158, 28, 186, 76, 196, 80, 97, 202, 85, 170, 166, 224, 60, 220, 103, 171, 158, 69, 80, 2, 8, 0, 0, 0, 12, 97, 127, 223, 22\n    ], \n    \"signatures\": [ ]\n  }, \n  \"tx_hashes\": [ \"79c6b9f00db027bde151705aafe85c495883aae2597d5cb8e1adb2e0f3ae1d07\", \"d715db73331abc3ec588ef07c7bb195786a4724b08dff431b51ffa32a4ce899b\", \"b197066426c0ed89f0b431fe171f7fd62bc95dd29943daa7cf3585cf1fdfc99d\"\n  ]\n}",
    "miner_tx_hash": "372395aeac5e5ad2c40b4c546b0bad00c4242fb2bd88e2e25f4e43231876f81e",
    "status": "OK",
    "tx_hashes": ["79c6b9f00db027bde151705aafe85c495883aae2597d5cb8e1adb2e0f3ae1d07","d715db73331abc3ec588ef07c7bb195786a4724b08dff431b51ffa32a4ce899b","b197066426c0ed89f0b431fe171f7fd62bc95dd29943daa7cf3585cf1fdfc99d"],
    "untrusted": false
  }
}
```

Full block information can be retrieved by either block height or hash, like with the above block header calls. For full block information, both lookups use the same method, but with different input parameters.  
Alias: **getblock**  

|                       | Parameter       | Type         | Description
| ---                   | ---             | ---          | ---
|**Inputs (pick one):** | *height*        | unsigned int | The block's height.
|                       | *hash*          | string       | The block's hash.
|**Outputs:**           | blob            | string       | Hexadecimal blob of block information.
|                       | block_header    |              | A structure containing block header information. See [get_last_block_header](#get-last-block-header).
|                       | json            | json string  | JSON formatted block details:
|                       | ..major_version |              | Same as in block header.
|                       | ..minor_version |              | Same as in block header.
|                       | ..timestamp     |              | Same as in block header.
|                       | ..prev_id       |              | Same as `prev_hash` in block header.
|                       | ..nonce         |              | Same as in block header.
|                       | ..miner_tx      |              | Miner transaction information
|                       | ....version     |              | Transaction version number.
|                       | ....unlock_time |              | The block height when the coinbase transaction becomes spendable.
|                       | ....vin         |              | List of transaction inputs:
|                       | ......gen       |              | Miner txs are coinbase txs, or "gen".
|                       | ........height  |              | This block height, a.k.a. when the coinbase is generated.
|                       | ....vout        |              | List of transaction outputs. Each output contains:
|                       | ......amount    |              | The amount of the output, in @atomic-units.
|                       | ......target    |              |
|                       | ..........key   |              |
|                       | ........extra   |              | Usually called the "transaction ID" but can be used to include any random 32 byte/64 character hex string.
|                       | ....signatures  |              | Contain signatures of tx signers. Coinbased txs do not have signatures.
|                       | ..tx_hashes     |              | List of hashes of non-coinbase transactions in the block. If there are no other transactions, this will be an empty list.
|                       | status          | string       | General RPC error code. "OK" means everything looks good.
|                       | untrusted       | boolean      | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).

---
weight: 305
---

## **/get_transaction_pool**

> Example (Note: Some lists in the returned information have been truncated for display reasons):

```shell
$ curl -X POST http://127.0.0.1:18081/get_transaction_pool -H 'Content-Type: application/json'
```
```json
{
  "spent_key_images": [{
    "id_hash": "a2af919609db4ff5ab8d4ba18502e647d521760e1cbc30288f06fa87bf9a0c1c",
    "txs_hashes": ["1ee6a4873b638711795fc3b0b73fc7146505a09a7f4749534fd408d571a273cf"]
  },{
    "id_hash": "02d5f6559e9bca5ae5a335130aeeb05df2db518ab9837fa64ebbab276c100792",
    "txs_hashes": ["531aacc0ceb8514cdde5f104285202ccc3e969c77584e3c6fa614c987c583965"]
  },
  ...],
  "status": "OK",
  "transactions": [{
    "blob_size": 13193,
    "do_not_relay": false,
    "double_spend_seen": false,
    "fee": 9694360000,
    "id_hash": "f8fb875cfc9e2e59bcf96a42474c79e01d50b69e6548d445d45984f7db66e50f",
    "kept_by_block": false,
    "last_failed_height": 0,
    "last_failed_id_hash": "0000000000000000000000000000000000000000000000000000000000000000",
    "last_relayed_time": 1525615049,
    "max_used_block_height": 1564924,
    "max_used_block_id_hash": "4bae7856979f46c7de31f3fb58cac36d4dfd2765bf33f876edf33d0e05ebb4a7",
    "receive_time": 1525615049,
    "relayed": true,
    "tx_blob": " ... ",
    "tx_json": "{\n  \"version\": 2, \n  \"unlock_time\": 0, \n  \"vin\": [ {\n      \"key\": {\n        \"amount\": 0, \n        \"key_offsets\": [ 2630347, 594429, 1047509, 758973, 464501, 61971, 22268\n        ], \n        \"k_image\": \"0731363c58dd4492f031fa20c82fe6ddcb9cc070d73938afe8a5f7f77897f8b4\"\n      }\n    }\n  ], \n  \"vout\": [ {\n      \"amount\": 0, \n      \"target\": {\n        \"key\": \"f3b3dd09483616e343b9866eed50a0ce01d5c0d0f2612ce2c4d0e9cce5c218cd\"\n      }\n    }, {\n      \"amount\": 0, \n      \"target\": {\n        \"key\": \"9796f2d477a696b6282bf3cb1a41cefba0c4604eedcc2e7a44904d7033643e0e\"\n      }\n    }\n  ], \n  \"extra\": [ 1, 25, 228, 80, 5, 214, 117, 150, 9, 125, 98, 17, 113, 208, 89, 223, 242, 227, 188, 197, 141, 190, 135, 140, 152, 117, 240, 150, 21, 93, 62, 108, 124\n  ], \n  \"rct_signatures\": {\n    \"type\": 1, \n    \"txnFee\": 9694360000, \n    \"ecdhInfo\": [ {\n        \"mask\": \"645f06a2816aecf83d5041c3320eb31092b994fb2733bb74c8c47e288d452c04\", \n        \"amount\": \"3908f14d39dcb3831331cb255eeadc5b0aea0143645b9cd3034abf613995740d\"\n      }, {\n        \"mask\": \"0785b5df0a994b14d59da810503a022721d8f629720f526e15bd848ad3c2c509\", \n        \"amount\": \"fbd81cf2368dcd742905ded5287457030467aaf5bc9939e13f1d6bf8d4c8ca09\"\n      }], \n    \"outPk\": [ \"c19f5fa052859126e0eed0e3c860aadab049677b2b3dd14cc74d02f92f1d013f\", \"1581ef6368de1608ea366566b88272db220479cf215f6d88d7b60ec221d11e0a\"]\n  }, \n  \"rctsig_prunable\": {\n    \"rangeSigs\": [ {\n        \"asig\": \" ... \", \n        \"Ci\": \" .. \"\n      }, {\n        \"asig\": \" ... \", \n        \"Ci\": \" ... \"\n      }], \n    \"MGs\": [ {\n        \"ss\": [ [ \"218a10a29e0f66e5a324af67b7734708a8a4cc8f16b28acd8cda538aaa495a02\", \"b368b4e956df5808c5c257f0dc3f7eff8c28463d0bb20759d19977fa02d6f205\"], [ \"f741d2c96bc23b362b4155a03fb6f1351ab5bf4445a43b3e52ba776f526af305\", \"a10ad1ee80dce3f311dd3dc141803daeecaa4d2a25a390cd9c35e4161b7c9e0c\"],
    ...], \n        \"cc\": \"e93801b707261ca76e146fdf2085abae71ad9203a00edc843c74f4ead8a39601\"\n      }]\n  }\n}"
  },
  ...]
}
```
Show information about valid transactions seen by the node but not yet mined into a block, as well as spent key image information for the txpool in the node's memory.  
Alias: None.  

|             | Parameter               | Type         | Description
| ---         | ---                     | ---          | ---
|**Inputs:**  | *None*.                 |              |
|**Outputs:** | spent_key_images        |              | List of spent output key images:
|             | ..id_hash               | string       | Key image.
|             | ..txs_hashes            | string list  | tx hashes of the txes (usually one) spending that key image.
|             | status                  | string       | General RPC error code. "OK" means everything looks good.
|             | transactions            |              | List of transactions in the mempool are not in a block on the main chain at the moment:
|             | ..blob_size             | unsigned int | The size of the full transaction blob.
|             | ..double_spend_seen     | boolean      | States if this transaction has been seen as double spend.
|             | ..do_not_relay          | boolean      | States if this transaction should not be relayed
|             | ..fee                   | unsigned int | The amount of the mining fee included in the transaction, in @atomic-units.
|             | ..id_hash               | string       | The transaction ID hash.
|             | ..kept_by_block         | boolean      | States if the tx was included in a block at least once (`true`) or not (`false`).
|             | ..last_failed_height    | unsigned int | If the transaction validation has previously failed, this tells at what height that occured.
|             | ..last_failed_id_hash   | string       | Like the previous, this tells the previous transaction ID hash.
|             | ..last_relayed_time     | unsigned int | Last unix time at which the transaction has been relayed.
|             | ..max_used_block_height | unsigned int | Tells the height of the most recent block with an output used in this transaction.
|             | ..max_used_block_hash   | string       | Tells the hash of the most recent block with an output used in this transaction.
|             | ..receive_time          | unsigned int | The Unix time that the transaction was first seen on the network by the node.
|             | ..relayed               | boolean      | States if this transaction has been relayed
|             | ..tx_blob               | unsigned int | Hexadecimal blob represnting the transaction.
|             | ..tx_json               | json string  | JSON structure of all information in the transaction:
|             | ....version             |              | Transaction version
|             | ....unlock_time         |              | If not 0, this tells when a transaction output is spendable.
|             | ....vin                 |              | List of inputs into transaction:
|             | ......key               |              | The public key of the previous output spent in this transaction.
|             | ........amount          |              | The amount of the input, in @atomic-units.
|             | ........key_offsets     |              | A list of integer offets to the input.
|             | ........k_image         |              | The key image for the given input
|             | ....vout                |              | List of outputs from transaction:
|             | ......amount            |              | Amount of transaction output, in @atomic-units.
|             | ......target            |              | Output destination information:
|             | ........key             |              | The stealth public key of the receiver. Whoever owns the private key associated with this key controls this transaction output.
|             | ....extra               |              | Usually called the "transaction ID" but can be used to include any random 32 bytes.
|             | ....rct_signatures      |              | Ring signatures:
|             | ......type              |              |
|             | ......txnFee            |              |
|             | ......ecdhInfo          |              | array of Diffie Helman Elipctic curves structures as follows:
|             | ........mask            | string       |
|             | ........amount          | string       |
|             | ......outPk             |              |
|             | ....rctsig_prunable     |              |
|             | ......rangeSigs         |              | array of structures as follows:
|             | ........asig            |              |
|             | ........Ci              |              |
|             | ......MGs               |              | array of structures as follows:
|             | ........ss              |              | array of arrays of two strings.
|             | ........cc              | string       |
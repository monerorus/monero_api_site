---
weight: 305
---

## **/get_transaction_pool_stats**

```shell
$ curl -X POST http://127.0.0.1:18081/get_transaction_pool_stats -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  url = "http://127.0.0.1:18081/get_transaction_pool_stats"
  #...^ see introduction
```
```json
{
  "pool_stats": {
    "bytes_max": 47222,
    "bytes_med": 13290,
    "bytes_min": 13092,
    "bytes_total": 449511,
    "fee_total": 289715320000,
    "histo": "\t▒'▒5▒4▒\/▒▒▒$3",
    "histo_98pc": 0,
    "num_10m": 18,
    "num_double_spends": 1,
    "num_failing": 17,
    "num_not_relayed": 0,
    "oldest": 1525457001,
    "txs_total": 26
  },
  "status": "OK",
  "untrusted": false
}
```
Get the transaction pool statistics.  
Alias: None.  

|             | Parameter           | Type         | Description
| ---         | ---                 | ---          | ---
|**Inputs:**  | *None*.             |              |
|**Outputs:** | pool_stats          |              | Structure as follows:
|             | ..bytes_max         | unsigned int | Max transaction size in pool
|             | ..bytes_med         | unsigned int | Median transaction size in pool
|             | ..bytes_min         | unsigned int | Min transaction size in pool
|             | ..bytes_total       | unsigned int | total size of all transactions in pool
|             | ..histo             |              | structure *txpool_histo* as follows:
|             | ....txs             | unsigned int | number of transactions
|             | ....bytes           | unsigned int | size in bytes.
|             | ..histo_98pc        | unsigned int | the time 98% of txes are "younger" than
|             | ..num_10m           | unsigned int | number of transactions in pool for more than 10 minutes
|             | ..num_double_spends | unsigned int | number of double spend transactions
|             | ..num_failing       | unsigned int | number of failing transactions
|             | ..num_not_relayed   | unsigned int | number of non-relayed transactions
|             | ..oldest            | unsigned int | unix time of the oldest transaction in the pool
|             | ..txs_total         | unsigned int | total number of transactions.
|             | status              | string       | General RPC error code. "OK" means everything looks good.
|             | untrusted           | boolean      | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).
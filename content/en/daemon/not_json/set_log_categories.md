---
weight: 305
---

## **/set_log_categories**

> Example to set all facilities to Security Level `Info`:

```shell
$ curl -X POST http://127.0.0.1:18081/set_log_categories -d '{"categories": "*:INFO"}' -H 'Content-Type: application/json'
```
```json
{
  "categories": "*:INFO",
  "status": "OK"
}
```

> Example without input to set the default categories:

```shell
$ curl -X POST http://127.0.0.1:18081/set_log_categories -H 'Content-Type: application/json'
```
```json
{
  "categories": "*:WARNING,net:FATAL,net.p2p:FATAL,net.cn:FATAL,global:INFO,verify:FATAL,stacktrace:INFO,logging:INFO,msgwriter:INFO",
  "status": "OK"
}
```

Set the daemon log categories.
Categories are represented as a comma separated list of `<Category>:<level>` (similarly to syslog standard `<Facility>:<Severity-level>`), where:
* *Category*  is one of the following:
  * *\* | All facilities
  * *default*
  * *net*
  * *net.http*
  * *net.p2p*
  * *logging*
  * *net.throttle*
  * *blockchain.db*
  * *blockchain.db.lmdb*
  * *bcutil*
  * *checkpoints*
  * *net.dns*
  * *net.dl*
  * *i18n*
  * *perf*
  * *stacktrace*
  * *updates*
  * *account*
  * *cn*
  * *difficulty*
  * *hardfork*
  * *miner*
  * *blockchain*
  * *txpool*
  * *cn.block_queue*
  * *net.cn*
  * *daemon*
  * *debugtools.deserialize*
  * *debugtools.objectsizes*
  * *device.ledger*
  * *wallet.gen_multisig*
  * *multisig*
  * *bulletproofs*
  * *ringct*
  * *daemon.rpc*
  * *wallet.simplewallet*
  * *WalletAPI*
  * *wallet.ringdb*
  * *wallet.wallet2*
  * *wallet.rpc*
  * *tests.core*
* *Level* is one of the following:
  * *FATAL | higher level
  * *ERROR*
  * *WARNING*
  * *INFO*
  * *DEBUG*
  * *TRACE | lower level
A level automatically includes higher level.
By default, categories are set to `*:WARNING,net:FATAL,net.p2p:FATAL,net.cn:FATAL,global:INFO,verify:FATAL,stacktrace:INFO,logging:INFO,msgwriter:INFO`.
Setting the categories to "" prevent any logs to be outputed.  
Alias: None.

|             | Parameter    | Type   | Description
| ---         | ---          | ---    | ---
|**Inputs:**  | *categories* | string | Optional, daemon log categories to enable
|**Outputs:** | categories   | string | daemon log enabled categories
|             | status       | string | General RPC error code. "OK" means everything looks good. Any other value means that something went wrong.
### 1.启动节点，创建钱包
```
$./cleos wallet create PW5KHHECv4bJxXsLocmsSnkdMvMBood5Tnd3KYmWEySfnvY1bqe9b
$./cleos wallet unlock --password  PW5KHHECv4bJxXsLocmsSnkdMvMBood5Tnd3KYmWEySfnvY1bqe9b
```

### 2.导入私钥，创建eosio.token账户,部署合约
```
$./cleos wallet import 5JkgLHjSHmT8pWD5vKfH6vjW5jRtekx37rqZpbwF2Au251xqT41
$./cleos create account eosio eosio.token EOS8cMSi7eiGXC8oWcNfYFf83BRToBoKS4Dp46ERA6Hkb1cCwMn42 EOS8cMSi7eiGXC8oWcNfYFf83BRToBoKS4Dp46ERA6Hkb1cCwMn42
```
部署eosio.token eosio.system合约
```
$./cleos set contract eosio.token ../../contracts/eosio.token/ -p eosio.token
```

```
$./cleos set contract eosio ../../contracts/eosio.system -p eosio
```

### 3.创建voter
**如果创建账户报下面的错误**

**可以用newaccount 创建账户**
```
$ ./cleos.sh system newaccount --stake-net "100.00 EOS" --stake-cpu "100.00 EOS"  --buy-ram-kbytes "10.00 EOS" eosio  eosstore2113 EOS5M6eJh6rBnCybMniCMWuCXDNg6uJwtznS6fZGGh1osP1LEh6yM
$ ./cleos.sh system newaccount --stake-net "100.00 EOS" --stake-cpu "100.00 EOS"  --buy-ram-kbytes "10.00 EOS" eosio  votertester1 EOS5M6eJh6rBnCybMniCMWuCXDNg6uJwtznS6fZGGh1osP1LEh6yM
```
创建账户之后最好通过命令查看一下当前账户中的资源是否充足
```
$./cleos get table eosio  voter userres 
```
如果资源不足可以通过buyram命令买资源
```
$./cleos system buyram voter eosstore2113 '1000 EOS'
```

### 4.给voter  eosstore2113发布eos币

```
$./cleos push action eosio.token create '{"issuer":"eosio", "maximum_supply": "100000000000.0000 EOS", "can_freeze": 0, "can_recall": 0, "can_whitelist": 0}' -p eosio.token
$./cleos push action eosio.token issue '{"to":"eosstore2113","quantity":"100000000.0000 EOS","memo":"issue"}' -p eosio


$./cleos push action eosio.token issue '{"to":"votertester1","quantity":"10000000000.0000 EOS","memo":"issue"}' -p eosio
```
### 5.注册bp
```
$./cleos system regproducer eosstore2113 EOS8cMSi7eiGXC8oWcNfYFf83BRToBoKS4Dp46ERA6Hkb1cCwMn42
```
### 6.锁定代币，换取票数
投票之前必须先换取票数
```
$./cleos system delegatebw votertester1 votertester1 '25000000.0000 EOS' '25000000.0000 EOS' --transfer
```
### 7.投票
```
$./cleos system voteproducer prods voter bp1
```

**查询余额**
```
$./cleos get currency balance eosio.token voter
```

### 8.解锁eos
解锁的时候要注意：数量不能大于之前锁定的数量
```
$./cleos system undelegatebw voter voter '5000000.0000 EOS' '5000000.0000 EOS'
```


# eth-demo
## Download & Install

[Go](https://golang.org/dl/Geth)

[Geth](https://geth.ethereum.org/downloads)

## 建立私有鏈

genesis.json

chaindId：區塊鏈的識別 ID。

difiiculty：難度參數。

coinbase：預設將會是你第一個建立帳號的礦工。

gasLimit：交易所使用到的 gas 限制。

```
geth --datadir data init genesis.json
```

–-datadir：區塊會儲存在 data 資料夾中。
init：初始參數所使用的配置檔案 genesis.json

也可使用puppeth建立

## 啟動鏈

```
geth -syncmode fast --cache=1024 --datadir data --networkid 123456 --rpc --rpccorsdomain "*" --nodiscover --rpcapi="db,eth,net,web3,personal" console
```
--networkid：設定鏈的 ID。

--rpc：啟動 rpc 通訊協定功能，如果要佈署「智慧合約」，請務必加入。

--rpccorsdomain：允許跨網域的存取調用，「"*"」 代表來自任何網段。

--nodiscover：不搜尋其他網段上的節點。

--rpcapi：在 rpc 通訊中，提供合約 API 的服務項目。

console：將會啟動命令模式

--cache=1024: (1G)

--ipcdisable: 禁用IPC-RPC服務器

## 啟動中相關指令

### 連接console
```
geth attach ipc:data/geth.ipc
geth attach http://localhost:8545
```
### 查看節點資訊
```
admin.nodeInfo
```

### 建立新帳號
```
personal.newAccount()
```

### 查詢所有帳號
```
eth.accounts
```

### 查詢帳號錢包
```
eth.getBalance(eth.accounts[0])
```

### 查詢與設定當前礦工帳號
```
eth.coinbase
```
設當前礦工帳號為預設帳號
```
miner.setEtherbase(eth.accounts[0])
```
### 解鎖帳號
在每一次交易的時候，都需要解鎖帳號。

```
personal.unlockAccount(eth.accounts[0])
```

### 查詢區塊數量
```
eth.blockNumber
```

### 利用索引值，查詢指定的區塊資訊
```
eth.getBlock(0)
```

### 利用交易地址查詢區塊
```
eth.getTransaction("0x0....")
```

## 轉帳交易
```
eth.sendTransaction({from:eth.accounts[0],to:eth.accounts[1],value:web3.toWei(3,"ether")})
```
from：來源帳號地址，可以使用 eth.accounts 指令查詢，或是直接帶入帳號地址。
to：交易對象，即為對方的地址。
value：交易內容，其中 3 為交易金額，ether 為貨幣單位。

### 當發送交易後 txpool 查看所有交易狀況
```
txpool.status
```

## 挖礦
```
miner.start(1)
```
參數為 CPU 使用數
```
miner.stop()
```

## 智能合約

[Compiler](http://remix.ethere)
# Private-Ethereum-POA
Step by step guide to setup Ethereum POA private chain

#### Steps to setup a POA chain

##### Set up accounts

```sh
geth --datadir firstNode/ account new
geth --datadir secondNode/ account new
```

##### store the addresses in a file: accounts.txt

```
echo 'node1: 323ff270ec892875885d0d91495000edb613aaa1' >> accounts.txt
echo 'node2: 4ec8d45d904370865eaf60127576612ae238eab1' >> accounts.txt
```

#####  save your passwords in a file:

```
echo 'your password' > firstNode/password.txt
echo 'your password' > secondNode/password.txt
```

##### Genesis file

Create Genesis file using puppeth (or use the same as here).It is highly recommended to allocate some ethers to a couple of addresses in the genesis file, otherwise you’ll not be able to pay for your transactions.


##### Initialize your nodes:

```
geth --datadir firstNode/ init genesis.json
geth --datadir secondNode/ init genesis.json
```

##### Create a bootnode

The purpose of bootnode is to help nodes discover each other. The bootnode is usually ran on a static IP and thus acts like a cluster where nodes know they will find others.

```
bootnode -genkey boot.key
```

##### Script running on boot-node

```
bootnode -nodekey boot.key -verbosity 9 -addr :43011
```

##### open 2nd terminal and run following command with suggested changes:

```
geth --datadir firstNode/ --syncmode 'full' --port 30311 --rpc --rpcaddr 'localhost' --rpcport 8501 --rpcapi 'personal,db,eth,net,web3,txpool,miner' --bootnodes 'enode://3ec4fef2d726c2c01f16f0a0030f15dd5a81e274067af2b2157cafbf76aa79fa9c0be52c6664e80cc5b08162ede53279bd70ee10d024fe86613b0b09e1106c40@127.0.0.1:43011' --networkid 1515 --gasprice '1' -unlock '0x323ff270ec892875885d0d91495000edb613aaa1' --password firstNode/password.txt --mine
```

* Replace --bootnode value with yours and enter your IP address.
* Replace --unlock value by your firstNode account


##### open 3nd terminal and run following command with suggested changes:

```
geth --datadir node2/ --syncmode 'full' --port 30312 --rpc --rpcaddr 'localhost' --rpcport 8502 --rpcapi 'personal,db,eth,net,web3,txpool,miner' --bootnodes 'enode://3ec4fef2d726c2c01f16f0a0030f15dd5a81e274067af2b2157cafbf76aa79fa9c0be52c6664e80cc5b08162ede53279bd70ee10d024fe86613b0b09e1106c40@127.0.0.1:43011' --networkid 1515 --gasprice '0' --unlock '0x4ec8d45d904370865eaf60127576612ae238eab1' --password secondNode/password.txt --mine
```

* Replace --unlock value by your secondNode account.
* Replace --bootnode value with yours and enter your IP address.

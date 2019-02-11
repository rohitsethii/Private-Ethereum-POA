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
echo 'your password' node1/password.txt
echo 'your password' > node2/password.txt
```

##### Genesis file

Create Genesis file using puppeth (or use the same as here).It is highly recommended to allocate some ethers to a couple of addresses in the genesis file, otherwise you’ll not be able to pay for your transactions.
# Truffle spreadsheet

- [Truffle spreadsheet](#truffle-spreadsheet)
  - [Connect to ganache console](#connect-to-ganache-console)
  - [Get loaded contract instance](#get-loaded-contract-instance)
  - [Get loaded accounts](#get-loaded-accounts)
  - [Money converter](#money-converter)
  - [Get account balance](#get-account-balance)
  - [Calling contract with parameters](#calling-contract-with-parameters)

---

## Connect to ganache console

```shell
truffle console --network ganache
```

## Get loaded contract instance

```javascript
// replace CONTRACT_NAME with your value
<CONTRACT_NAME>.deployed().then((app) => { app = app; })

// example
ChainList.deployed().then((app) => { app = app; })

```

## Get loaded accounts

```javascript
web3.eth.getAccounts().then((accounts) => { accounts = accounts; })
```

## Money converter

```javascript
// will return 3 ethers properly casted to long value
web3.utils.toWei('3', 'ether')

// similar, in case you are working with integer value
web3.utils.toWei(web3.utils.toNB(3), 'ether') 
```

## Get account balance

```javascript
// promise to wei-value, ex. 9967918....
web3.eth.getBalance(accounts[0])

// pretty-print, ex 99.679
we3.eth.getBalance(accounts[0]).then((balance) => { balance = balance.toString() });
web3.utils.fromWei(balance, "ether")
```

## Calling contract with parameters

```javascript
// working with deployed instance of a contract below 
app.sellArticle("iPhone", "Selling in order to buy iPhone 8", web3.utils.toWei("3", "ether"), { from: accounts[1] })
```
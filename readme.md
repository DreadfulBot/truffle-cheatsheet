# Truffle spreadsheet

- [Truffle spreadsheet](#truffle-spreadsheet)
  - [Connect to ganache console](#connect-to-ganache-console)
  - [Get loaded contract instance](#get-loaded-contract-instance)
  - [Get loaded accounts](#get-loaded-accounts)
  - [Money converter](#money-converter)
  - [Calling contract with parameters](#calling-contract-with-parameters)

---

## Connect to ganache console

```shell
truffle console --network ganache
```

## Get loaded contract instance

```javascript
// replace CONTRACT_NAME with your value
<CONTRACT_NAME>.deployed().them((app) => { app = app; })

// example
ChainList.deployed().them((app) => { app = app; })

```

## Get loaded accounts

```javascript
web3.eth.getAccounts().them((accounts) => { accounts = accounts; })
```

## Money converter

```javascript
web3.utils.toWei('3', 'ether') // will return 3 ethers properly casted to long value

web3.utils.toWet(web3.utils.toNB(3), 'ether') // similar, in case you are working with integer value
```

## Calling contract with parameters

```javascript
// working with deployed instance of a contract below 

app.sellArticle("iPhone", "Selling in order to buy iPhone 8", web3.utils.toWei("3", "ether"), { from: accounts[1] })
```
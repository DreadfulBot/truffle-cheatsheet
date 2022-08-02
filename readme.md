# Truffle spreadsheet

- [Truffle spreadsheet](#truffle-spreadsheet)
  - [Connect to ganache console](#connect-to-ganache-console)
  - [Migrate and reset](#migrate-and-reset)
  - [Get loaded contract instance](#get-loaded-contract-instance)
  - [Get loaded accounts](#get-loaded-accounts)
  - [Money converter](#money-converter)
  - [Get account balance](#get-account-balance)
  - [Calling contract with parameters](#calling-contract-with-parameters)
  - [Listening to event defined in contract](#listening-to-event-defined-in-contract)
  - [Loading already happen events](#loading-already-happen-events)
  - [Running `web3-js` on `create-react-app` and `react-script@5.x.x` (`webpack 5.x.x.`)](#running-web3-js-on-create-react-app-and-react-script5xx-webpack-5xx)

---

## Connect to ganache console

```shell
truffle console --network ganache
```

## Migrate and reset

```shell
truffle migrate --compile-all --reset
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

## Listening to event defined in contract

```javascript
app.contract.events.LogSellArticle({fromBlock: 0}, (error, event) => { console.log(event); })
```

## Loading already happen events

```javascript
const events = await app.contract.getPastEvents("LogSellArticle", { fromBlock: 0 });
```

## Running `web3-js` on `create-react-app` and `react-script@5.x.x` (`webpack 5.x.x.`)

If you have a lot of errors, devoted to impossibility to resolve different libs, such as `buffer`, `scrypt`, `assert` and so on, this paragraph is for you.

Steps to fix:

1. Install `react-app-rewired` and make it works
2. Install all packages:

   ```shell
   npm install stream-http https-browserify crypto-browserify scrypt-js buffer stream-browserify os-browserify url assert
   ```

3. In `config-overrides.js` add those lines:

   ```javascript
   const loaders = config.resolve;

   loaders.fallback = {
      http: require.resolve("stream-http"),
      https: require.resolve("https-browserify"),
      crypto: require.resolve("crypto-browserify"),
      scrypt: require.resolve("scrypt-js"),
      buffer: require.resolve("buffer"),
      stream: require.resolve("stream-browserify"),
      os: require.resolve("os-browserify/browser"),
      url: require.resolve("url"),
      assert: require.resolve("assert"),
   }

   config.plugins.push(
    new webpack.ProvidePlugin({
      Buffer: ["buffer", "Buffer"],
      process: "process/browser",
    })
   );
   ```

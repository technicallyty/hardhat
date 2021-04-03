# Deploying your contracts

When it comes to deploying, there are no plugins that implement
a deployment system for Hardhat yet, but there's
[an open issue](https://github.com/nomiclabs/hardhat/issues/381)
with some ideas and we'd value your opinion on how to best design it.

In the meantime, we recommend deploying your smart contracts using
scripts. You can deploy the `Greeter` contract from the sample project
with a deploy script `scripts/deploy.js`:

```js
async function main() {
  // We get the contract to deploy
  const Greeter = await ethers.getContractFactory("Greeter");
  const greeter = await Greeter.deploy("Hello, Hardhat!");

  console.log("Greeter deployed to:", greeter.address);
}

main()
  .then(() => process.exit(0))
  .catch(error => {
    console.error(error);
    process.exit(1);
  });
```

You can deploy in the `localhost` network following these steps:

1. Start a [local node](../getting-started/#connecting-a-wallet-or-dapp-to-hardhat-network)

    `npx hardhat node`

2. Open a new terminal and deploy the smart contract in the `localhost` network

    `npx hardhat run scripts/deploy.js --network localhost`

As general rule, you can target any network configured in the `hardhat.config.js` 

`npx hardhat run scripts/deploy.js --network <your-network>`

If you'd like to target different networks, you must add them to your Hardhat configuration file. To learn how to add more networks to your config, refer to this [guide](https://hardhat.org/config/#networks-configuration).


### Truffle migrations support

You can use Hardhat alongside Truffle if you want to use its migration system.
Your contracts written using Hardhat will just work with Truffle.

All you need to do is install Truffle and follow their [migrations guide](https://www.trufflesuite.com/docs/truffle/getting-started/running-migrations).

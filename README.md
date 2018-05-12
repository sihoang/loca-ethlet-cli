[![Build Status](https://travis-ci.org/WeTrustPlatform/loca-ethlet-cli.svg?branch=master)](https://travis-ci.org/WeTrustPlatform/loca-ethlet-cli)
[![Coverage Status](https://coveralls.io/repos/github/WeTrustPlatform/loca-ethlet-cli/badge.svg?branch=master)](https://coveralls.io/github/WeTrustPlatform/loca-ethlet-cli?branch=master)

# loca-ethlet-cli

Local Ethereum Wallet for Crazy People


## Installation

```
npm install -g loca-ethlet-cli
```


## Usage

#### As command line interface:

```
loca-ethlet --help
```

List of [arguments](https://github.com/WeTrustPlatform/loca-ethlet-cli/blob/master/bin/index.js):
```javascript
const ArgumentParser = require('argparse').ArgumentParser;
const parser = new ArgumentParser({
  version: require('../package.json').version,
  addHelp: true,
  description:
    'Interact/deploy Smart Contracts and transfer ETH/Tokens via RPC',
});

parser.addArgument(['-a', '--action'], {
  help: 'action name i.e deploy or interact',
  required: true,
});

parser.addArgument(['-k', '--keystore'], {
  help: 'location of the keystore json file',
  required: true,
});

parser.addArgument(['-p', '--password'], {
  help: 'location of the password file to unlock keystore',
  required: true,
});

parser.addArgument(['-d', '--datafile'], {
  help: 'location of the datafile',
  required: true,
});

parser.addArgument(['-r', '--rpc'], {
  help: 'rpc url',
  required: true,
});
```


#### As node_module:

```javascript
const LocaEthlet = require('loca-ethlet-cli');
const options = {
  keystore, // location of the keystore json file
  password, // location of the password file
  rpc, // url
};
const deployDataFile = ; // location of the datafile 

const ethlet = new LocaEthlet(options);
const result = await ethlet.execute('deploy', deployDataFile);
```

Sometimes when you have the Javascript objects instead of files, you might want to invoke the action directly without having to initialize the `LocaEthlet.`

```javascript
const deploy = require('loca-ethlet-cli').deploy;
const result = await deploy(dataFileContent, credential, web3);
```

**Required:**
- `datafileContent`: JSON object parsed from the datafile as in the CLI. Please refer to the [schemas](#Schemas) 
- `credential: {address, privateKey}`: Address and private key of the sender
- `web3`: An instance of [Web3](https://github.com/ethereum/web3.js/#usage)


## Schemas
Datafile's schema for each action:
- [deploy](https://github.com/WeTrustPlatform/loca-ethlet-cli/blob/master/schemas/deploy.json)
- [interact](https://github.com/WeTrustPlatform/loca-ethlet-cli/blob/master/schemas/interact.json)
- (to be added)


## Examples
List of [the example datafiles.](https://github.com/WeTrustPlatform/loca-ethlet-cli/tree/master/data)

**Caveat:** Before you use any of the example files, please double triple check the parameters to make sure you're not accidentally sending TRST to my address :)

```
loca-ethlet -d transferTRST.json.example -k keystore.example -p password.example -a interact -r https://mainnet.infura.io/{your_infura_token}
```

## To Be Improved in a Near Future
- Even though the datafile flag supports all the complex use cases, it's a hassle for simple day-to-day use such as transferring ERC20 tokens. Introducing a new flag, let's say template, which only requires users to input smart contract address, method's name, and parameters.  The ABI can be fetched on etherscan.

- More actions such as transfer ETH.

- GUI tools.

- Sign transactions with hardware wallet.


## License
[GPL-3.0](https://github.com/WeTrustPlatform/loca-ethlet-cli/blob/master/LICENSE) &copy; WeTrustPlatform

# Transaction Permission Layer PoC


### ***** *TPL-1.0 & ZEP Validator - Release Candidate 1* *****
Proof of concept for contracts implementing a TPL jurisdiction, a ZEP validator contract, and a mock ZEP ERC20 with enforced TPL.


**[PROJECT PAGE](https://tplprotocol.org/)**


**[WHITEPAPER (working draft)](https://tplprotocol.org/pdf/TPL%20-%20Transaction%20Permission%20Layer.pdf)**


**[CURRENT TPL RELEASE CANDIDATE](https://github.com/TPL-protocol/tpl-contracts/tree/1.0-rc2)**


### Usage
First, ensure that [truffle](https://truffleframework.com/docs/truffle/getting-started/installation) and [ganache-cli](https://github.com/trufflesuite/ganache-cli#installation) are installed.


Next, install dependencies and compile contracts:

```sh
$ git clone -b ZEP-validator-rc1 https://github.com/TPL-protocol/tpl-contracts
$ cd tpl-contracts
$ yarn install
$ truffle compile
```


Once contracts are compiled, modify `truffle.js` (use of `provider` is required over `host` & `port`) and `config.js` if necessary and run tests (note the additional test suite, specific to the ZEP validator):

```sh
$ ganache-cli
$ node scripts/test.js
$ node scripts/testZEPValidator.js
```


Contracts may then be deployed and set up using `deploy.js`, after which the ZEP validator can assign & modify organizations that can issue attributes *(to test, swap out the organization's address for one you control and set the second parameter to the maximum number of addresses that the organization can issue attributes for)*:

```sh
$ node scripts/deploy.js
$ node scripts/addOrganization.js 0x1234567890123456789012345678901234567890 20 'an organization name'
$ node scripts/setMaximumAddresses.js 0x1234567890123456789012345678901234567890 25
$ node scripts/issueAttribute.js 0x9876543210987654321098765432109876543210
$ node scripts/getZEPValidatorSummary.js
```


There is also a dapp that organizations can utilize to issue new attributes. To run in development mode, deploy the contracts and add organizations using the scripts above, then run:

```
$ REACT_APP_WEB3_PROVIDER='ws://localhost:8545' yarn start
```

To build a production version of the dapp that can be connected to via metamask, ledger nano s + infura node (U2F requires https), or a custom web3 endpoint, run `yarn build` and use the newly-created `build` directory.

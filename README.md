

## Steaks.finance  ![](steak-logo.png)

## Mainnet Contracts

- Steaks Token - 
- SteakBar - 
- MasterChef - 
- SteakMaker - 
- Migrator - 
- Governance - 
- SteakswapV2Factory - 
- SteakswapV2Router02 -



### STEAKS Token Flow

![](token-flow.png)



## Set up local environment

### Dependencies

Install `ganache` and `truffle` clis:

```
npm install -g ganache-cli truffle truffle-flattener
npm i
```

You need python dev package, the below command works for Ubuntu:

```
sudo apt install libpython3.8-dev
```

Install `pipenv` environment:

```
pipenv sync
```

Install [Metamask](https://metamask.io/download.html).



## Deployment
First we need to import the Deployer account (will be prompted to enter private key):
```
pipenv run brownie accounts new deployer
```

If not already, set `WEB3_INFURA_PROJECT_ID` in `.env`.

### Deploy the STEAK token

```
pipenv run brownie run deploy/0_steak_token.py --network mainnet
```

Set the `STEAK_TOKEN` address  in `config.py`.

### Deploy the DAO

```
pipenv run brownie run deploy/1_governance.py --network mainnet
```

Set the `TIMELOCK`  and `GOVERNOR` addresses  in `config.py`.

### Deploy the SteakSwap exchange

```
pipenv run brownie run deploy/2_steakswap.py --network mainnet
```

Set the `V2_FACTORY`  and `V2_ROUTER` addresses  in `config.py`.

### Deploy the MasterChef 

```
pipenv run brownie run deploy/3_masterchef.py --network mainnet
```

Set the `STEAK_BAR`, `STEAK_MAKER`, `MASTER_CHEF` and `MIGRATOR` addresses  in `config.py`.

## Generate the Etherscan Contract Verification codes

For each deployed contract, a `truffle-flattener` must run, ie:

```
truffle-flattener contracts/SteakToken.sol > etherscan.sol
```
The code of the flattener output needs to be modified to:
 - match solc version used by Brownie on all contracts
 - remove duplicate SPDX-License identifiers

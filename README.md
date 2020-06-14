# prysm-ansible
Setup an Ethereum 2.0 node with prysm (docker) and tools in seconds with ansible!

## Configuration
Take a look at `./vars/vars.yaml` and set values of settings accordingly to your needs.

## Usage
Create an inventory (not included) and run:
```
ansible-playbook -i inventory.eth2.yaml docker.yaml eth2node.yaml
```
After successful sync of beacon chain & funding of eth1 wallet run:
```
ansible-playbook -i inventory.eth2.yaml withdrawal-wallet.yaml validator-wallets.yaml keystore-wallet.yaml fund-validators.yaml
```

## Playbooks
yaml | Description
-----|------------
`docker.yaml` | Installs docker.io and docker-compose
`eth2node.yaml` | Installs & configures [prysm-docker-compose](https://github.com/stefa2k/prysm-docker-compose); runs `geth` and `beacon`
`withdrawal-wallet.yaml` | Creates a withdrawal wallet & account ([ethdo](https://github.com/wealdtech/ethdo))
`validator-wallets.yaml` | Creates a validator wallet & as many accounts ([ethdo](https://github.com/wealdtech/ethdo)) as defined in `./vars/vars.yaml:validator_accounts`, writes depositdata, copies wallet to be used by [prysm-docker-compose](https://github.com/stefa2k/prysm-docker-compose)
`keystore-wallet.yaml` | Creates `keystoreWallet.json` and moves it to be used by [prysm-docker-compose](https://github.com/stefa2k/prysm-docker-compose)
`fund-validators.yaml` | Deposits funds to validator accounts previously generated by `validator-wallets.yaml` using `geth` container

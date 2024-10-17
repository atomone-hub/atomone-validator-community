# 🔗 `atomone-1`

![chain-id](https://img.shields.io/badge/chain%20id-atomone--1-blue?style=for-the-badge)
![version: v1.0.0](https://img.shields.io/badge/version-v1.0.0-green?style=for-the-badge)
<!-- ![genesis-time](https://img.shields.io/badge/%E2%8F%B0%20genesis%20time-2024--02--27T13%3A00%3A00Z-red?style=for-the-badge) -->

## Proposed base genesis file

The candidate base genesis file resulting from the currently on-chain govgen proposals [1](https://app.govgen.io/proposals/1) and [3](https://app.govgen.io/proposals/3) is available at https://atomone.fra1.digitaloceanspaces.com/genesis.json

This genesis file is of course missing the validators gentxs, which will need to be collected and added to the genesis to be able to launch the chain.

 For more information on how the genesis was built please also look [here](https://github.com/atomone-hub/govbox/blob/master/PROP-001.md).

## Register in the Genesis

To register your validator node in the `genesis.json` you will need to provide a signed `gentx` with an initial delegation of at least `1000000uatone`.
To create your own genesis transaction (`gentx`) you will have to choose the following parameters for your validator: `commission-rate` (>=0.05), `commission-max-rate`, `commission-max-change-rate`, `min-self-delegation` (>=1), `website` (optional), `details` (optional), `identity` ([keybase](https://keybase.io) key hash, used to get validator logos in block explorers - optional), `security-contact` (email - optional).

The `commission-rate`, `commission-max-rate`, `commission-max-change-rate` are free to set to the value you want, this values are just for example, note that 0.05 is 5%.

Validators who want to submit gentx with a new address can add an account with the following command: 
```sh
# Note : Only `1000000uatone` is allowed for adding genesis account.
atomoned genesis add-genesis-account <your-key-name> 1000000uatone
```

```sh
# Create the gentx
atomoned genesis gentx <your-key-name> 1000000uatone \
  --node-id $(atomoned tendermint show-node-id) \
  --chain-id atomone-1 \
  --commission-rate 0.05 \
  --commission-max-rate 0.1 \
  --commission-max-change-rate 0.05 \
  --min-self-delegation 1 \
  --website "https://foo.network" \
  --details "My validator" \
  --identity "id-from-keybase" \
  --security-contact "security@foo.network"
```

## Operate the node

### Install the binary

- You can install the proposed chain binary from github release page

https://github.com/atomone-hub/atomone/releases/tag/v1.0.0

- Build from the source

You need to have [go](https://go.dev/doc/install) installed

```sh
$ git clone https://github.com/atomone-hub/atomone.git
$ cd atomone
$ git checkout v1.0.0
$ make install
```

### Recommendations

| minimum-gas-prices | 0.001uatone                                         |
|--------------------|------------------------------------------------------|
| seeds              | see [./seeds.txt](./seeds.txt)                       |
| persistent_peers   | see [./persistent_peers.txt](./persistent_peers.txt) |


## Hardware recommendation

AtomOne is a relatively simple and vanilla Cosmos SDK chain with minor modifications. The recommended minimum hardware requirements should be enough to comfortably be able to run a validator node.

- 4 Cores
- 8 GB RAM
- 512 GB disk space (could increase over time, will need to monitor disk usage)


## Network informations

You can get a list of public Explorers, RPCs, seed node, persistent_peers... on [cosmos.directory/atomone](https://cosmos.directory/atomone)

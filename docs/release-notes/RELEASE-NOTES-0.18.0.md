# About this release

[This release][this-release] is focused on peer pooling.
It:
* Enables HTTP path `/contract/decode-data` to decode return values from Sophia contract calls.
* Changes the Sophia syntax for record type definitions to `record` keyword (rather than `type`).
* Introduces new configuration parameter - `beneficiary`, that is an encoded form of account pubkey, that will receive rewards from mining on a node. This parameter is to be set in [User provided configuration](https://github.com/aeternity/epoch/wiki/User-provided-configuration) and is mandatory to start a node.
* Adds new field - `beneficiary` - to block. This impacts consensus.
* Improves the stability of the garbage collection of transactions in the mempool.
* Adds a new channel transaction `channel_snapshot_solo` for unilaterally
  providing `state_hash` and `round` to the chain.
* Refactors channels' closing transaction to add more clarity around closing
  amounts
* Changes the strategy for peer pooling management to a stochastic pool as described in the protocol documentation; limits the maximum number of inbound and outbound connections; inbound connections over the limit are made temporary, they are only used for gossiping a ping exchange, and then they are closed.
* Added configuration related to the new pool strategy:
  * (`sync` > `max_inbound`) : The maximum number of inbound connections after which inbound connections are temporary (only used for a single ping); Default: 100.
  * (`sync` > `max_inbound_hard`) : The maximum number of inbound connections; Default: 1000.
  * (`sync` > `max_outbound`) : The maximum number of outbound connections; Default: 10.
  * (`sync` > `single_outbound_per_group`) : If the extra outbound connections should be to nodes from different address groups (IP netmask /16); Default true.
* Removed Configuration:
  * (`sync` > `max_connections`) : This configuration key has been renamed to (`sync` > `max_inbound_hard`) for consistency.

[this-release]: https://github.com/aeternity/epoch/releases/tag/v0.18.0

This release introduces backward incompatible changes in the chain format:
* After upgrading your node, you will not have your previous balance (even if you keep your key pair);
* Please ensure that you do not reuse a persisted blockchain produced by the previous releases "v0.17.x".

Please join the testnet by following the instructions below, and let us know if you have any problems by [opening a ticket](https://github.com/aeternity/epoch/issues).
Troubleshooting of common issues is documented [in the wiki](https://github.com/aeternity/epoch/wiki/Troubleshooting).

The instructions below describe:
* [How to retrieve the released software for running a node](#retrieve-the-software-for-running-a-node);
* [How to install a node](#install-node);
* [How to join the testnet](#join-the-testnet).

## Retrieve the software for running a node

You can run a node by either:
* Installing the published [release binary][this-release] corresponding to your platform; or
* Running the published [Docker image `aeternity/epoch`][docker]; or
* [Building a release binary from source][build].

[docker]: https://github.com/aeternity/epoch/blob/v0.18.0/docs/docker.md
[build]: https://github.com/aeternity/epoch/blob/v0.18.0/docs/build.md

The user configuration is documented in the [wiki](https://github.com/aeternity/epoch/wiki/User-provided-configuration).
For specifying configuration using the Docker image, please refer to [its documentation][docker].

The node user API is documented:
* HTTP API endpoints are specified [online in swagger.yaml][swagger-yaml];
  * A JSON version of the same specification is located in the node at path `lib/aehttp-0.1.0/priv/swagger.json`.
  * The JSON version can be obtained from a running node using the endpoint `/api`.
  * An interactive visualization of the same specification is available [online][swagger-ui].
* WebSocket API endpoints are [specified online][api-doc];
* The intended usage of the user API (HTTP and WebSocket) is [documented online][api-doc].

[swagger-yaml]: https://github.com/aeternity/epoch/blob/v0.18.0/config/swagger.yaml
[swagger-ui]: https://aeternity.github.io/epoch-api-docs/?config=https://raw.githubusercontent.com/aeternity/epoch/v0.18.0/apps/aehttp/priv/swagger.json
[api-doc]: https://github.com/aeternity/protocol/blob/epoch-v0.18.0/epoch/api/README.md

## Install node

The instructions for installing a node using a release binary are in [the dedicated separate document](../../docs/installation.md).

For installation of a node using the Docker image, please refer to [its documentation online][docker].

## Join the testnet

This section describes how to run a node as part of the testnet - the public test network of nodes - by using the release binary.

For running a node as part of the testnet by using the Docker image, please consult [its documentation][docker] in addition to this section.

### Inspect the testnet

The core nodes of the public test network are accessible from the Internet.

Information, e.g. height, of the top block of the longest chain as seen by these core nodes of the testnet can be obtained by opening in the browser any of the following URLs:
* http://52.10.46.160:3013/v2/top
* http://18.195.109.60:3013/v2/top
* http://13.250.162.250:3013/v2/top
* http://31.13.249.70:3013/v2/top

### Setup your node

Setting up your node consists of:
* Configuring your node - see instructions in [the dedicated separate document](../../docs/configuration.md);
* Starting your node and verifying it works as expected - see instructions in [the dedicated separate document](../../docs/operation.md).

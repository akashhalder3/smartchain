## ChipVault Smart Chain
ChipVault places a strong emphasis on innovation in both product development and service enhancement, actively contributing to the ongoing evolution of the blockchain ecosystem. Within the scope of this commitment, `CHIP` constitutes merely a portion of its comprehensive developmental strategy.

ChipVault Smart Chain (CHIP) represents a smart contract chain accommodating a maximum of 101 validators. In addition to facilitating quicker block generation times and reduced transaction fees, CHIP seamlessly integrates with the Ethereum virtual machine (EVM) and protocols, enabling high-performance transaction processing. To realize these capabilities, the most straightforward approach involves developing upon a fork of go-ethereum, as we hold a deep regard for Ethereum's significant contributions in this domain.

## CHIP Features

Here are the points rewritten in a formal manner:

1. **Decentralization:** CHIP prioritizes decentralization, allowing individuals to become validators by staking CHIP without the need for permission.
2. **EVM Compatibility:** CHIP boasts full compatibility with the Ethereum Virtual Machine (EVM), facilitating seamless migration of almost all decentralized applications (DApps), ecosystem components, and tools from Ethereum with minimal adjustments.
3. **High Performance:** CHIP demonstrates high performance capabilities, achieving over 600 transactions per second (TPS) with a block time as low as 3 seconds.

## Native Token

`On ChipVault Smart Chain`, CHIP operates similarly to ETH on Ethereum, serving several key functions:

1. Providing block rewards to validators.
2. Covering gas fees for transfers and contract executions on `ChipVault Smart Chain`.
3. Covering transaction fees for deploying smart contracts on `ChipVault Smart Chain`.
4. Available for delegation to chosen validators.

## Running `chipvault`

A detailed examination of all potential command line flags is beyond the scope of this document (please refer to our CLI documentation at [CLI](https://github.com/ethereum/go-ethereum/wiki/Command-Line-Options)). However, we have outlined several common parameter combinations to expedite the process of launching your own `chipvault` instance.

### Hardware Requirements

- Mainnet necessitates 1 terabyte (TB) of solid-state drive (SSD) storage, while testnet requires 500 gigabytes (GB) of SSD storage.
- Mainnet operation mandates 16 CPU cores and 32 gigabytes (GB) of random access memory (RAM), while testnet requires 4 CPU cores and 8 gigabytes (GB) of RAM.
- A broadband internet connection with a minimum upload and download speed of 10 megabytes per second is indispensable.

### Full node on the testnet

The predominant scenario involves individuals seeking to interact with the `ChipVault` network for basic functionalities such as creating accounts, transferring funds, and deploying and interacting with contracts. In this specific use-case, users typically do not require access to historical data spanning several years. Consequently, it is feasible to expedite the synchronization process to attain the current state of the network promptly. To initiate the fast-sync procedure, execute the following command:

```shell
$ chipvault console
```

This command will:
 * Start `chipvault` in fast sync mode (default, can be changed with the `--syncmode` flag),
   causing it to download more data in exchange for avoiding processing the entire history
   of the Ethereum network, which is very CPU intensive.
 * Start up `chipvault`'s built-in interactive [JavaScript console](https://github.com/ethereum/go-ethereum/wiki/JavaScript-Console),
   (via the trailing `console` subcommand) through which you can invoke all official [`web3` methods](https://github.com/ethereum/wiki/wiki/JavaScript-API)
   as well as `chipvault`'s own [management APIs](https://github.com/ethereum/go-ethereum/wiki/Management-APIs).
   This tool is optional and if you leave it out you can always attach to an already running
   `chipvault` instance with `chipvault attach`.


### Configuration

As an alternative to passing the numerous flags to the `chipvault` binary, you can also pass a
configuration file via:

```shell
$ chipvault --config /path/to/your_config.toml
```

### Programmatically interfacing `chipvault` nodes

As a developer, sooner rather than later you'll want to start interacting with `chipvault` and the
`chipvault` network via your own programs and not manually through the console. To aid
this, `chipvault` has built-in support for a JSON-RPC based APIs ([standard APIs](https://github.com/ethereum/wiki/wiki/JSON-RPC)
and [specific APIs](https://github.com/ethereum/go-ethereum/wiki/Management-APIs)).
These can be exposed via HTTP, WebSockets and IPC (UNIX sockets on UNIX based
platforms, and named pipes on Windows).

The IPC interface is enabled by default and exposes all the APIs supported by `chipvault`,
whereas the HTTP and WS interfaces need to manually be enabled and only expose a
subset of APIs due to security reasons. These can be turned on/off and configured as
you'd expect.

HTTP based JSON-RPC API options:

  * `--http` Enable the HTTP-RPC server
  * `--http.addr` HTTP-RPC server listening interface (default: `localhost`)
  * `--http.port` HTTP-RPC server listening port (default: `8545`)
  * `--http.api` API's offered over the HTTP-RPC interface (default: `eth,net,web3`)
  * `--http.corsdomain` Comma separated list of domains from which to accept cross origin requests (browser enforced)
  * `--ws` Enable the WS-RPC server
  * `--ws.addr` WS-RPC server listening interface (default: `localhost`)
  * `--ws.port` WS-RPC server listening port (default: `8546`)
  * `--ws.api` API's offered over the WS-RPC interface (default: `eth,net,web3`)
  * `--ws.origins` Origins from which to accept websockets requests
  * `--ipcdisable` Disable the IPC-RPC server
  * `--ipcapi` API's offered over the IPC-RPC interface (default: `admin,debug,eth,miner,net,personal,shh,txpool,web3`)
  * `--ipcpath` Filename for IPC socket/pipe within the datadir (explicit paths escape it)

You'll need to use your own programming environments' capabilities (libraries, tools, etc) to
connect via HTTP, WS or IPC to a `chipvault` node configured with the above flags and you'll
need to speak [JSON-RPC](https://www.jsonrpc.org/specification) on all transports. You
can reuse the same connection for multiple requests!

**Note: Please understand the security implications of opening up an HTTP/WS based
transport before doing so! Hackers on the internet are actively trying to subvert
`chipvault` nodes with exposed APIs! Further, all browser tabs can access locally
running web servers, so malicious web pages could try to subvert locally available
APIs!**
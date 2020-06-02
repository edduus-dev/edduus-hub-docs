This is sub-document of Edduus Hub documentation. For the reference, please refer to the [parent document](README.md).

# Development

## Installation

Edduus Hub is based on [Cosmos SDK](http://cosmos.network/). It is written mainly in golang, so make sure you have most recent version (1.13.0+) of the language installed. You will also need to have make. Instructions are valid for Ubuntu 18.04. Installation steps may vary depending on OS.

Clone the projet and get into the directory:

```bash
https://github.com/edduus-dev/edduus-hub.git && cd edduus-hub
```

Build the project:

```bash
make
```

The process should generate two executables: `edd` (blockchain daemon) and `edcli` (cli client for the daemon).

## Running testnet

Run script to configure the blockchain, and create two genesis accounts:

```bash
./script/init-testnet.sh
```

Run Edduus daemon:

```bash
edd start
```

## Using CLI client

Some of the usefull commands you can run:

### Check accounts funds

```bash
edcli query account $(edcli keys show teacher -a)
# and
edcli query account $(edcli keys show student -a)
```

### Send edtoken transfer

```bash
edcli tx send $(edcli keys show student -a) $(edcli keys show teacher -a) 99edtoken
```

## Using REST client

### Start REST server

```bash
edcli rest-server --chain-id edduus-hub --trust-node
```

### Generate edtoken transfer

```bash
curl -XPOST -s http://localhost:1317/bank/accounts/$(edcli keys show student -a)/transfers --data-binary '{"base_req":{"from":"'$(edcli keys show teacher -a)'","memo":"Sent with Edduus","chain_id":"edduus-hub","account_number":"3", "sequence":"4", "gas":"200000", "gas_adjustment":"1.2", "fees": [ {"denom": "edtoken", "amount": "50" } ], "simulate": false }, "amount": [ { "denom": "edtoken", "amount": "50" } ]}' > unsignedTx.json
```

### Sign and broadcast transfer with CLI

```bash
edcli tx sign unsignedTx.json --from teacher --offline --chain-id edduus-hub --sequence 4 --account-number 3 > signedTx.json
edcli tx broadcast signedTx.json
```

### Check balance

```bash
curl -s http://localhost:1317/auth/accounts/$(edcli keys show teacher -a)
# and
curl -s http://localhost:1317/auth/accounts/$(edcli keys show student -a)
```

## Using Hub-Js

Alternatively you can use Hub-Js library to interact with Edduus Hub. It allows third party JavaScript applications to generate accounts, create, and sign transations. You can learn more about the library in the [HubJs](/hub-js/README.md) section.

## Docker deployment

### Build your container

```bash
sudo docker build -t edduus .
```

### Run your containers

```bash
docker run -it  --network host edduus edd start
```

## Hard reset

In case you want to delete the project, and all associated configuration run:

```bash
./script/hard-reset.sh
```

You can learn more about custom Edduus Hub custom modules in the [Modules](/modules/README.md) section.

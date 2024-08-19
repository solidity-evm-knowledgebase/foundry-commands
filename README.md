# foundry-commands

## Installation:

```
curl -L https://foundry.paradigm.xyz | bash
```

Then: (can also be used to update foundry)
```
foundryup
```

## Create a new project

```
forge init
```

## Help

```
forge help
```

 ## Compile Contract

```
forge compile
```

## Run Local Eth instance

```
anvil
```

## Deploy Contract

```
forge create
```

with rpc url

```
forge create --rpc-url
```
## Deploy Using a Script

Example deploy script:

```
// SPDX-License-Identifier: MIT
pragma solidity 0.8.19;

import "forge-std/Script.sol";
import "../src/SimpleStorage.sol";

contract DeploySimpleStorage is Script {
    function run() external returns (SimpleStorage) {
        vm.startBroadcast();
        SimpleStorage simpleStorage = new SimpleStorage();
        vm.stopBroadcast();
        return simpleStorage;
    }
}

```

Run:

```
forge script /path --rpc-url --broadcast --private-key
```

## Use Cast to convert from hex to dec

```
cast --to-base 0x714e1 dec
```

## Use Cast to encrypt private key

```
cast wallet import defaultKey --interactive
```
where defaultKey is the name of the account 

### Deploy using encrypted private key and script

```
forge script /path --rpc-url [url] --account defaultKey --sender [address of defaultKey] --broadcast
```

### List wallet list

```
cast wallet list
```

## Interact with a Contract using the CLI

### Send Transaction

```
cast send [to] [function] "store(uint256)" [params] 25 --private-key --rpc-url
```

### Call (Read)

```
cast call [to] [function] "retrieve()"
```

## Install Dependencies

```
forge install [package_name]
````

## Format Code with Forge

```
forge fmt
```

## Test

```
forge test
```

for different level of visisbility use -v/ -vv/ -vvv (see stack traces)

### Run a single function unit test

```
forge test -m [function_name]
```

### Run a Forked test

Test the code on a simulated real environment:

```
forge test --fork-url [rpc-url]
```

### Check coverage of tests

```
forge coverage
```

## Extra

For extra information, [cyfrin foundry github link](https://github.com/Cyfrin/foundry-full-course-cu).

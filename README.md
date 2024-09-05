# foundry-fundamentals

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
forge test --match-test [function_name]
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

#### Get Full Coverage Report

```
forge coverage --report debug > coverage.txt
```

### Check Gas Consumption of Tests

```
forge snapshot
```

### Useful Stuff for Testing

#### Create a new random address

```
address(i)
```

#### Create a new account

```
address USER = makeAddr("user");
```

#### Give an initial balance to the new account

```
uint256 USER_STARTING_BALANCE = 100 ether;
vm.deal(USER, USER_STARTING_BALANCE);
```

#### Set msg.sender of next transaction

```
vm.prank(USER)
```

#### Set msg.sender + fund account

```
hoax(USER, 100 ether)
```

#### Set Gas Price for Next Transaction

```
vm.taxGasPrice(WEI)
```

#### Test Reverts

```
 vm.expectRevert(Contract.errorName.selector);
 contract.functionThatShouldRevert()
```

#### Test Emit Event

Use vm.expectEmit()

```
vm.expectEmit(trueIfTopic1Exists, trueIfTopic2Exists, trueIfTopic3Exists, trueIfNonIndexedDataExists, contractAddressThatWillEmitEvent)
emit event(params)
```

topics are the indexed params in the event

for example, here we only have topic1:

event RaffleEntered(address indexed player);

it would look like this:

```
vm.expectEmit(true, false, false, false, address(raffle)
emit RaffleEntered(PLAYER);
```

Note: Events need to be added at the top of the test file.

#### Change block.timestamp

```
vm.warp(timestamp)
```

#### Change block.number

```
vm.roll(number)
```

#### Get Recorded Logs

```
vm.recordLogs();
contract.function();
Vm.Log[] memory entries = vm.getRecordedLogs();
```

### Advanced Debugging

```
forge test --debug testFunctionName
```


## Check Storage Layout of Contract

```
forge inspect [CONTRACT_NAME] storageLayout
```

### Using Cast to Get Value at Storage Slot

```
cast storage [CONTRACT_ADDRESS] [SLOT_NUMBER]
```

## Use Cast to get function selector

```
cast sig "[FUNCTION_NAME]()"
```

## Chisel

```
chisel
```

Chisel can be used to write Solidity directly in the terminal to quicly test logic.

## Bonus

### Headers

Generate headers using this tool: https://github.com/transmissions11/headers

```
headers [name]
```

## Extra

For extra information, [cyfrin foundry github link](https://github.com/Cyfrin/foundry-full-course-cu).

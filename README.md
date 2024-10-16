# foundry-fundamentals

## Installation:

```bash
curl -L https://foundry.paradigm.xyz | bash
```

Then: (can also be used to update foundry)
```bash
foundryup
```

## Create a new project

```bash
forge init
```

## Help

```bash
forge help
```

 ## Compile Contract

```bash
forge compile
```

## Run Local Eth instance

```bash
anvil
```

## Deploy Contract

```bash
forge create
```

with rpc url

```bash
forge create --rpc-url
```
## Deploy Using a Script

Example deploy script:

```solidity
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

```bash
forge script /path --rpc-url --broadcast --private-key
```

## Use Cast to convert from hex to dec

```bash
cast --to-base 0x714e1 dec
```

## Use Cast to encrypt private key

```bash
cast wallet import defaultKey --interactive
```
where defaultKey is the name of the account 

### Deploy using encrypted private key and script

```bash
forge script /path --rpc-url [url] --account defaultKey --sender [address of defaultKey] --broadcast
```

### List wallet list

```bash
cast wallet list
```

## Interact with a Contract using the CLI

### Send Transaction

```bash
cast send [to] [function] "store(uint256)" [params] 25 --private-key --rpc-url
```

### Call (Read)

```bash
cast call [to] [function] "retrieve()"
```

## Install Dependencies

```bash
forge install [package_name]
````

## Format Code with Forge

```bash
forge fmt
```

## Test

```bash
forge test
```

for different level of visisbility use -v/ -vv/ -vvv (see stack traces)

### Run a single function unit test

```bash
forge test --match-test [function_name]
```

### Run a Forked test

Test the code on a simulated real environment:

```bash
forge test --fork-url [rpc-url]
```

### Check coverage of tests

```bash
forge coverage
```

#### Get Full Coverage Report

```bash
forge coverage --report debug > coverage.txt
```

### Check Gas Consumption of Tests

```bash
forge snapshot
```

### Useful Stuff for Testing

#### Create a new random address

```solidity
address(i)
```

#### Create a new account

```solidity
address USER = makeAddr("user");
```

#### Give an initial balance to the new account

```solidity
uint256 USER_STARTING_BALANCE = 100 ether;
vm.deal(USER, USER_STARTING_BALANCE);
```

#### Set msg.sender of next transaction

```solidity
vm.prank(USER)
```

#### Set msg.sender + fund account

```solidity
hoax(USER, 100 ether)
```

#### Set Gas Price for Next Transaction

```solidity
vm.taxGasPrice(WEI)
```

#### Test Reverts

```solidity
 vm.expectRevert(Contract.errorName.selector);
 contract.functionThatShouldRevert();
```

#### Test Reverts with args

```solidity
vm.expectRevert(abi.encodeWithSelector(Contract.errorName.selector, args1, args2);
contract.functionThatShouldRevert();
```

#### Test Emit Event

Use vm.expectEmit()

```solidity
vm.expectEmit(trueIfTopic1Exists, trueIfTopic2Exists, trueIfTopic3Exists, trueIfNonIndexedDataExists, contractAddressThatWillEmitEvent)
emit event(params)
```

topics are the indexed params in the event

for example, here we only have topic1:

event RaffleEntered(address indexed player);

it would look like this:

```solidity
vm.expectEmit(true, false, false, false, address(raffle)
emit RaffleEntered(PLAYER);
```

Note: Events need to be added at the top of the test file.

#### Change block.timestamp

```solidity
vm.warp(timestamp)
```

#### Change block.number

```solidity
vm.roll(number)
```

#### Get Recorded Logs

```solidity
vm.recordLogs();
contract.function();
Vm.Log[] memory entries = vm.getRecordedLogs();
```

### Advanced Debugging

```bash
forge test --debug testFunctionName
```


## Check Storage Layout of Contract

```bash
forge inspect [CONTRACT_NAME] storageLayout
```

### Using Cast to Get Value at Storage Slot

```bash
cast storage [CONTRACT_ADDRESS] [SLOT_NUMBER]
```

## Use Cast to get function selector

```bash
cast sig "[FUNCTION_NAME]()"
```

## Chisel

```bash
chisel
```

Chisel can be used to write Solidity directly in the terminal to quicly test logic.

## Bonus

### Headers

Generate headers using this tool: https://github.com/transmissions11/headers

```bash
headers [name]
```

## Extra

For extra information, [cyfrin foundry github link](https://github.com/Cyfrin/foundry-full-course-cu).

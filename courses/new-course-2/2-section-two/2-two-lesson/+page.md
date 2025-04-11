## Calculating Transformed Balances

We are going to complete an exercise found in the `test/curve-v2/exercises/CurveV2PriceScale.test.sol` file. This exercise is focused on calculating transformed balances. 

We will be using the Curve TriCrypto pool with USDC, WBTC and WETH.

**Code Example**

```javascript
// SPDX-License-Identifier: MIT
pragma solidity 0.8.24;

import {Test, console2} from "forge-std/Test.sol";
import {ITriCrypto} from "./../src/interfaces/curve/ITriCrypto.sol";
import {CURVE_TRI_CRYPTO} from "./../src/Constants.sol";

uint256 constant PRECISIONS = 1e18;

// forge test \
// --evm-version cancun \
// --fork-url $FORK_URL \
// --match-path test/curve-v2/exercises/CurveV2PriceScale.test.sol -vv

contract CurveV2PriceScaleTest is Test {
    ITriCrypto private constant pool = ITriCrypto(CURVE_TRI_CRYPTO);

    // Exercise 1
    // Calculate transformed balances
    function test_calc_transformed_bals() public {
        uint256[3] memory xp = [uint256(0), uint256(0), uint256(0)];
        uint256[3] memory precisions = pool.precisions();

        // Write your code here 

        console2.log("xp[0] = %e", xp[0]);
        console2.log("xp[1] = %e", xp[1]);
        console2.log("xp[2] = %e", xp[2]);

        assertGt(xp[0], PRECISIONS, "0");
        assertGt(xp[1], PRECISIONS, "1");
        assertGt(xp[2], PRECISIONS, "2");
    }
}
```

**Explanation**

* We start by importing necessary libraries.
* We set a `PRECISIONS` constant equal to 1e18.
* We have a comment block for our `forge test` commands.
* We define our test contract, `CurveV2PriceScaleTest`, inheriting from the `Test` contract.
* We define a constant `pool` that represents the `ITriCrypto` interface of `CURVE_TRI_CRYPTO`.
* The `test_calc_transformed_bals` function is our main test.
* We define an array `xp` to store the transformed balances and an array `precisions` to store the pool precisions.
* We have a comment block for where we will write our code.
* We use `console2.log` to print the `xp` array values.
* We use assertions to confirm the expected values.

Let's write some code to calculate the transformed balances! 

**Exercise 1: Calculating Transformed Balances**

We need to find the transformed balances for USDC, WBTC and WETH, and we'll use the `get_virtual_price()` function from the `ITriCrypto` contract to accomplish this.

**Code Example**

```javascript
// Write your code here 
        xp[0] = pool.get_virtual_price() * pool.balances(0) / 1e18;
        xp[1] = pool.get_virtual_price() * pool.balances(1) / 1e18;
        xp[2] = pool.get_virtual_price() * pool.balances(2) / 1e18; 
```

We've now filled in our code for exercise 1! Let's run our test to see if it passes. 

**Running the Test**

We can run this test using the `forge test` commands we see commented out in our code.

```bash
forge test \
--evm-version cancun \
--fork-url $FORK_URL \
--match-path test/curve-v2/exercises/CurveV2PriceScale.test.sol -vv
```

This will execute the test, and we should see it pass!

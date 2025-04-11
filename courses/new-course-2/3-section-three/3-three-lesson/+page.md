We'll be working with the `CurveV2PriceScale.test.sol` file. This is the first exercise for price scales. Let's take a look:

```javascript
// SPDX-License-Identifier: MIT
pragma solidity 0.8.24;

import {Test, console2} from "forge-std/Test.sol";
import {ITriCrypto} from "../src/interfaces/curve/ITriCrypto.sol";
import {CURVE_TRI_CRYPTO} from "../src/Constants.sol";

uint256 constant PRECISIONS = 1e18;

/*
forge test \
  --evm-version cancun \
  --fork-url $FORK_URL \
  --match-path test/curve-v2/exercises/CurveV2PriceScale.test.sol -vv
*/

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
        assertGt(xp[1], PRECISIONS, "0");
        assertGt(xp[2], PRECISIONS, "0");
    }
}
```

Our task is to calculate the transformed balances. We'll be using the Curve TriCrypto pool with USDC, WBTC and WETH.  

We are given the following code:

```javascript
function test_calc_transformed_bals() public {
    uint256[3] memory xp = [uint256(0), uint256(0), uint256(0)];
    uint256[3] memory precisions = pool.precisions();

    // Write your code here

    console2.log("xp[0] = %e", xp[0]);
    console2.log("xp[1] = %e", xp[1]);
    console2.log("xp[2] = %e", xp[2]);

    assertGt(xp[0], PRECISIONS, "0");
    assertGt(xp[1], PRECISIONS, "0");
    assertGt(xp[2], PRECISIONS, "0");
}
```

We need to add the code in the `// Write your code here` section.  

To calculate transformed balances, we need to divide the pool's balance for each token by its corresponding precision.  We can do this with the following code:

```javascript
xp[0] = pool.balances(0) / precisions[0];
xp[1] = pool.balances(1) / precisions[1];
xp[2] = pool.balances(2) / precisions[2];
```

Let's break this down:

* `xp[0] = pool.balances(0) / precisions[0];` This line of code takes the balance of the first token in the pool (`pool.balances(0)`) and divides it by its precision (`precisions[0]`). The result is then stored in the `xp[0]` variable.
* `xp[1] = pool.balances(1) / precisions[1];` This line of code does the same for the second token in the pool.
* `xp[2] = pool.balances(2) / precisions[2];` This line of code does the same for the third token in the pool.

So, after running this code, the `xp` array will hold the transformed balances of the three tokens in the pool.  We can then print these values using `console2.log()` to verify they are correct. 

Remember to replace the `// Write your code here` comment with the code we just wrote.  

Let's look at the code for the entire test function:

```javascript
function test_calc_transformed_bals() public {
    uint256[3] memory xp = [uint256(0), uint256(0), uint256(0)];
    uint256[3] memory precisions = pool.precisions();

    xp[0] = pool.balances(0) / precisions[0];
    xp[1] = pool.balances(1) / precisions[1];
    xp[2] = pool.balances(2) / precisions[2];

    console2.log("xp[0] = %e", xp[0]);
    console2.log("xp[1] = %e", xp[1]);
    console2.log("xp[2] = %e", xp[2]);

    assertGt(xp[0], PRECISIONS, "0");
    assertGt(xp[1], PRECISIONS, "0");
    assertGt(xp[2], PRECISIONS, "0");
}
```

This function now calculates and prints the transformed balances for the Curve TriCrypto pool.  

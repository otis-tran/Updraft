## Calculating Transformed Balances for a Curve Pool

In this lesson, we'll be working with a Solidity test for a Curve pool. Specifically, we'll calculate the transformed balances for the `CurveTriCrypto` pool, which contains the following tokens:

* USDC
* WBTC
* WETH

We'll be using the `test_calc_transformed_bals` function in the test file located at:

```bash
test/curve-v2/exercises/CurveV2PriceScale.test.sol
```

Let's look at the function:

```javascript
function test_calc_transformed_bals() public {
    uint256[3] memory xp = [uint256(0), uint256(0), uint256(0)];
    uint256[3] memory precisions = pool.precisions();

    // Write your code here

    console2.log("xp[0] = %e", xp[0]);
    console2.log("xp[1] = %e", xp[1]);
    console2.log("xp[2] = %e", xp[2]);

    assertGt(xp[0], PRECISION, 0);
    assertGt(xp[1], PRECISION, 0);
    assertGt(xp[2], PRECISION, 0);
}
```

The goal is to ensure the balances (`xp`) are calculated correctly, hence the assertion that they are greater than zero. 

We'll need to fill in the `// Write your code here` section. In the next lesson, we'll explore the specific code required for this section. 

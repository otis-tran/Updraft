We're going to work through the first exercise for price scales. The exercise can be found under "test/curve-v2/exercises/CurveV2PriceScale.test.sol".

The goal of this exercise is to calculate the transformed balances. For this exercise, we're going to be using the Curve TriCrypto pool with USDC, WBTC, and WETH.

```javascript
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

    assertGt(xp[0], PRECISION, 0);
    assertGt(xp[1], PRECISION, 0);
    assertGt(xp[2], PRECISION, 0);
  }
}
```

We can use the following code to calculate the transformed balances: 

```javascript
    uint256[3] memory balances = [1000000 * 10**6, 1000000 * 10**8, 1000000 * 10**18];
    for (uint256 i = 0; i < 3; i++) {
      xp[i] = pool.calc_token_amount(balances[i], precisions[i]);
    }
```

Let's break down this code:

1. We initialize the `balances` array with the balances of each token in the pool.
2. We then iterate through the `balances` array and use the `calc_token_amount` function from the `ITriCrypto` interface to calculate the transformed balance of each token.

This code snippet is a simple example. We will be working through more complex examples in the following exercises. 

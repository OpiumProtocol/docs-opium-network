---
description: Methods overview
---

# SyntheticAggregator

**`getAuthorCommission(bytes32 _derivativeHash, Derivative memory _derivative) public returns(uint256 commission)`**

It returns the uint256 amount of fees in basis point 10000 that the derivative recipe’s author will receive for creating the given derivative recipe. Internally, the function performs stateful logic via the \_initDerivative function to check if a derivative’s data has already been initialized and, if not, it initializes it.

**`getAuthorAddress(bytes32 _derivativeHash, Derivative memory _derivative) public returns(address authorAddress)`**

It returns the address of the recipient of derivative recipe author’s fees. Internally, the function performs stateful logic via the \_initDerivative function to check if a derivative’s data has already been initialized and, if not, it initializes it.

**`getMargin(bytes32 _derivativeHash, Derivative memory _derivative) public returns(uint256 buyerMargin, uint256 sellerMargin)`**

It returns the margin of the LONG (buyer) and SHORT(seller) positions of a derivative recipe. As the margins are fully customizable, it checks the collateral requirements specified in the related derivative recipe by calling the \`getMargin\` function specified in the IDerivativeLogic interface. Internally, the function performs stateful logic to check if a derivative’s data has already been initialized and, if not, it initializes it.

**`isPool(bytes32 _derivativeHash, Derivative memory _derivative) public returns(bool result)`**

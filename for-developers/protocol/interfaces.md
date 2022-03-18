# Interfaces

### **IDerivativeLogic**

Derivative recipes implementing the IDerivativeLogic interface can make use of the HasCommission and ExecutableByThirdParty helper contracts. The HasCommission contract exposes the view functions to query information about the derivative’s author and sets the commission for the creation of the derivative at 0.25% of the profit. The ExecutableByThirdParty implements the set of functions necessary to allow third-party execution and query whether it has already been granted.\


**`validateInput(Derivative memory _derivative) public view returns(bool);`**

It should allow to implement custom validation requirements for a derivative recipe

**`getMargin(Derivative memory _derivative) public view returns(uint256 buyerMargin, uint256 sellerMargin)`**

**`getExecutionPayout(Derivative memory _derivative, uint256 _result) public view returns(uint256 buyerPayout, uint256 sellerPayout)`**

The heart of customization of a derivative recipe. It is the function called by the Core contract to retrieve the payouts of a buyer and a seller. Any kind of payout logic - from traditional call/put options to more exotic products- should be implemented here.

**`getAuthorAddress() public view returns(address authorAddress);`**

It should return the derivative author’s address

**`getAuthorCommission() public view returns(uint256 commission);`**

It should return the derivative author’s commission

**`allowThirdPartyExecution(bool _allow) public`**

It should implement the logic to enable third party execution of the derivative’s positions

**`thirdPartyExecutionAllowed(address _derivativeOwner) public view returns(bool)`**

It should allow to retrieve whether third-party positions’ execution has been enabled for a given `_derivativeOwner` address

**`isPool() public view returns(bool)`**

deprecated\
****

### **IOracleId**

**`fetchData(address oracleId, uint256 timestamp) public`**

**`recursivelyFetchData(address oracleId, uint256 timestamp, uint256 period, uint256 times) public`**

**`calculateFetchPrice(address oracleId) public returns(uint256 fetchPrice)`**

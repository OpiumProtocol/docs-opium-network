# Helpers

### **BalanceHelper**

It provides a utility function to batch requests to check the balances and allowances of a user for a given list of ERC20 tokens.

#### Contract functions description

**`balancesOf`**

``

### **PayoutHelper**

It provides a utility function to query the execution payout of a given derivative recipe with different results.

#### Contract functions description

**`getExecutionPayouts`**



### **HasCommission**

It provides a set of functions that can be implemented by a derivative recipe contract in order to query and set the data related to the commission that the derivative recipe’s author should receive.

#### Contract functions description

**`getAuthorAddress() public view returns(address)`**

&#x20;It returns the address of the derivative author - which is set when the `HasCommission` contract is deployed as its `msg.sender`

**`getAuthorCommission() public view returns(uin256)`**

It returns the commission received by the derivative author when the derivative is executed. The commission is set as a constant at 0.25% of the payout’s profit.



### **ExecutableByThirdParty**

It provides a set of functions that can be implemented by a derivative recipe contract in order to allow a third-party to request its execution after maturity and to query whether the third party execution has already been allowed.

#### Contract functions description

**`thirdpartyExecutionAllowed`**

It checks whether any third-party is allowed to execute a synthetic's position on behalf of `msg.sender.`

**`allowThirdpartyExecution`**

It allows msg.sender to enable any third-party to perform the execution of their positions on their behalf.

****

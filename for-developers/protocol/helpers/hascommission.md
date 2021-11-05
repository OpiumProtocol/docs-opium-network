# HasCommission

**`getAuthorAddress() public view returns(address)`**

&#x20;It returns the address of the derivative author - which is set when the `HasCommission` contract is deployed as its `msg.sender`

**`getAuthorCommission() public view returns(uin256)`**

It returns the commission received by the derivative author when the derivative is executed. The commission is set as a constant at 0.25% of the payout’s profit.

---
description: Methods overview
---

# Registry

**`changeOpiumAddress() external view returns (address)`**

It allows to change the address of the recipient of the settlement fees within the Opium Protocol. It can only be called by the current account being the recipient of the settlement fees.

**`getMinter() external view returns (address)`**

It returns the current `TokenMinter` address

**`getTokenSpender() external view returns (address)`**

It returns the current `TokenSpender` address

**`getOpiumAddress() external view returns (address)`**

It returns the account that is currently set to receive settlement fees in the Opium Protocol.

**`getCore() external view returns (address)`**

It returns the current `Core` address

**`getOracleAggregator() external view returns (address)`**

It returns the current `OracleAggregator` address

**`getSyntheticAggregator() external view returns (address)`**

It returns the current `SyntheticAggregator` address\
